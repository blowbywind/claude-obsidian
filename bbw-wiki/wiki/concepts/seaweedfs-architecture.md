---
title: SeaweedFS 아키텍처 — Needle·Volume·Filer·S3 레이어
type: concept
tags: [seaweedfs, object-storage, distributed-storage, s3, needle, volume, filer]
created: 2026-06-12
updated: 2026-06-12
sources: [2026-06-12-seaweedfs-docs]
---

## 정의

SeaweedFS의 내부 구조는 Facebook Haystack 논문을 기반으로 한 **3계층 스택**이다.

```
레이어 3: API        S3    FUSE   WebDAV   Hadoop   Iceberg REST
레이어 2: Filer    경로 추상화 + 메타데이터 스토어
레이어 1: Blob     Master Server ←→ Volume Server(s)
```

각 레이어는 독립 배포 가능. 하위 레이어 없이 상위 레이어 단독 운용 불가.

## 레이어 1: Blob Storage (Master + Volume)

### Master Server

| 항목 | 내용 |
|---|---|
| 기본 HTTP 포트 | 9333 |
| gRPC 포트 | 19333 (HTTP + 10000 규칙) |
| 합의 프로토콜 | Raft (리더 선출, 홀수 개 구성 필수) |
| 주요 역할 | 파일 ID 할당, 볼륨 배치 결정, Volume 헬스체크 |

Volume Server로부터 heartbeat를 수신해 클러스터 상태를 유지.
업로드 요청이 들어오면 사용 가능한 Volume의 위치와 파일 ID를 발급.

### Volume Server

| 항목 | 내용 |
|---|---|
| 기본 HTTP 포트 | 8080 |
| gRPC 포트 | 18080 |
| 기본 볼륨 크기 상한 | **30GB** |
| 초기 볼륨 수 | 8개 (기본) |
| RAM 사용량 | 2-4 GB/서버 |

#### Volume 물리 파일 구조

```
/data/
  1.dat   ← 실제 Needle 데이터 (슈퍼블록 + 순차 추가)
  1.idx   ← 고정 16바이트 인덱스 (NeedleId 8B + Offset 4B + Size 4B)
  2.dat
  2.idx
  ...
```

`.idx` 파일 덕분에 파일 조회가 O(1). NeedleMap은 인메모리 유지 (파일당 16바이트만 소비).

## Needle — 핵심 저장 단위

파일 1개 = Needle 1개. **불변·추가 전용(Append-only)**.

```
┌─────────────────────────────────────┐
│  Cookie (4B) | Needle ID (8B)       │
│  Size (4B)   | DataSize (4B)        │
│  Flags (1B)  | LastModified (5B)    │
│  Checksum CRC32 (4B)               │
│  AppendAtNs (8B)                    │
│  ──────────────── ≈ 45B 오버헤드 ──│
│  실제 파일 데이터 (가변 크기)       │
│  파일명, MIME 타입 (가변)           │
└─────────────────────────────────────┘
```

- 파일 업데이트: 기존 Needle에 `deleted` 플래그 → 볼륨 끝에 새 Needle 추가
- 공간 회수: `weed compact` 또는 자동 압축으로 삭제된 Needle 제거
- 수십억 파일도 파일당 45바이트 오버헤드만 → 소형 파일에 극히 효율적

## Erasure Coding (EC)

Reed-Solomon **RS(10,4)** 방식:

```
30GB 볼륨
  → 10개 데이터 샤드 (각 3GB)
  + 4개  패리티 샤드 (각 3GB)
  = 14개 EC 샤드 총합
```

| 파일 확장자 | 설명 |
|---|---|
| `.ec00`~`.ec09` | 데이터 샤드 |
| `.ec10`~`.ec13` | 패리티 샤드 |
| `.ecx` | EC 인덱스 |
| `.ecj` | EC 저널 |

- **4개 샤드 손실까지 복구 가능**
- 볼륨 단위 적용 (파일 단위 아님)
- 쓰기 성능 희생 → 웜/콜드 데이터 적합
- v4.33: per-shard 체크섬으로 비트롯(bitrot) 감지 추가

## 레이어 2: Filer (경로 추상화)

Blob Storage 위에 사람이 인식할 수 있는 파일 경로를 제공하는 계층.

| 항목 | 내용 |
|---|---|
| 기본 HTTP 포트 | 8888 |
| gRPC 포트 | 18888 |

### 파일 업로드 흐름

```
클라이언트 PUT /path/to/file
        ↓
Filer가 Master에서 (Volume ID + Needle ID) 획득
        ↓
실제 데이터 → Volume Server에 직접 스트리밍
        ↓
경로 ↔ 파일 ID 매핑 → 메타데이터 스토어에 저장
```

### 파일 조회 흐름

```
클라이언트 GET /path/to/file
        ↓
Filer 메타데이터 스토어에서 경로 → (Volume ID, Needle ID) 조회
        ↓
Volume Server로 리다이렉트 또는 프록시 응답
```

### 메타데이터 백엔드

| 유형 | 옵션 |
|---|---|
| 로컬 임베디드 (기본) | LevelDB, RocksDB, SQLite |
| 원격/분산 | PostgreSQL, MySQL, Redis, Cassandra, etcd, TiDB, MongoDB, ElasticSearch 등 |

**⚠️ 중요**: Filer 메타데이터가 손실되면 Volume 데이터가 있어도 파일 경로를 복구할 수 없다.
메타데이터 DB 파일을 별도 백업에 포함해야 한다.

### Filer 기능

- POSIX 속성, 심볼릭 링크, 소유자/권한 지원
- AES256-GCM 투명 암호화
- FUSE 마운트 (`weed mount`) → 로컬 파일시스템처럼 사용
- Hadoop HDFS 호환 API

## 레이어 3: API 게이트웨이

### S3 API Gateway

```
S3 클라이언트
    ↓  (S3 프로토콜)
S3 게이트웨이 (:8333)   ← 상태 비저장
    ↓  (내부 gRPC)
Filer (:8888)
    ↓
Volume Server
```

| 항목 | 내용 |
|---|---|
| 기본 포트 | 8333 |
| 의존성 | Filer 필수 (단독 실행 불가) |
| 인증 | 기본 공개 / `s3.json`으로 IAM 설정 |
| 버킷 경로 매핑 | `/buckets/<bucket_name>` → Filer 경로 |

**지원 기능**: 버킷 CRUD, 오브젝트 CRUD, 멀티파트 업로드, 범위 요청, 버저닝,
Presigned URL, IAM/STS, OIDC, 버킷 정책

**미지원**: S3 Express One Zone, SelectObjectContent, Object Lambda, 웹사이트 호스팅

### WebDAV (포트 7333)

Filer에 연결된 WebDAV 서버. Windows 네이티브 드라이브 마운트, macOS Finder 등에서 직접 접근 가능.

## 운용 모드

### weed server (BBW 현재 사용)

```bash
# 모든 컴포넌트를 단일 프로세스로 통합
weed server -dir=/data -s3 -s3.port=8333

# -s3 플래그가 -filer도 자동 활성화
# 명시적으로 모두 지정하면:
weed server -dir=/data -filer -s3 -ip.bind=0.0.0.0 \
  -master.volumeSizeLimitMB=1024 \
  -s3.port=8333
```

### weed mini (개인 서버 추천)

```bash
weed mini
# 모든 컴포넌트 + 볼륨 자동 튜닝 (64-1024MB)
# Admin UI, Iceberg REST, 유지보수 워커 포함
# 가장 단순하게 시작하는 방법
```

### 풀 클러스터 (프로덕션 HA)

```bash
# Master (3개 이상, 홀수)
weed master -ip=master1 -ip.bind=0.0.0.0 -peers=master2:9333,master3:9333

# Volume (n개, 수평 확장)
weed volume -ip=vol1 -master=master1:9333 -ip.bind=0.0.0.0

# Filer
weed filer -ip=filer1 -master=master1:9333

# S3
weed s3 -filer=filer1:8888 -ip.bind=0.0.0.0
```

## AWS SDK 연동 패턴

```python
# Python boto3
import boto3
s3 = boto3.client('s3',
    endpoint_url='http://seaweedfs:8333',
    aws_access_key_id='access_key',
    aws_secret_access_key='secret_key',
    region_name='us-east-1'  # 임의 값 필요
)

# 버킷 생성
s3.create_bucket(Bucket='my-bucket')

# 파일 업로드
s3.upload_file('/local/file.txt', 'my-bucket', 'path/file.txt')

# Presigned URL 생성 (1시간)
url = s3.generate_presigned_url(
    'get_object',
    Params={'Bucket': 'my-bucket', 'Key': 'path/file.txt'},
    ExpiresIn=3600
)
```

## 관련 개념

- [[wiki/concepts/caddy|Caddy]] — S3 엔드포인트 역방향 프록시
- [[wiki/concepts/kt-hairpin-nat|KT hairpin NAT]] — 외부 접근 구성

## 관련 엔티티

- [[wiki/entities/seaweedfs|SeaweedFS]] — 소프트웨어 엔티티 (버전, 설치 현황)
- [[wiki/entities/caddy|Caddy]] — 역방향 프록시

## 출처

- [[wiki/sources/2026-06-12-seaweedfs-docs]]
