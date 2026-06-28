---
title: SeaweedFS — 분산 오브젝트 스토리지 종합 문서
type: source
tags: [seaweedfs, object-storage, s3, distributed-storage, docker, go]
created: 2026-06-12
updated: 2026-06-12
origin: https://github.com/seaweedfs/seaweedfs/wiki (+ DeepWiki + Docker Hub + 벤치마크 아티클)
author: Chrislu (핵심 개발자) / 커뮤니티
date_published: 2026-06-12
summary: "SeaweedFS(Go, Apache-2.0) 분산 오브젝트 스토리지 — S3·FUSE·WebDAV 지원, 소형파일 O(1) 접근 설계, BBW 서버 v4.23 Docker(`storage_seaweedfs`) 단일"
---

## 요약

SeaweedFS는 Go로 작성된 Apache-2.0 오픈소스 분산 오브젝트 스토리지.
Facebook Haystack 논문에서 영감을 받아 수십억 개의 소형 파일을 O(1) 디스크 접근으로 처리하도록 설계됐다.
S3 호환 API·POSIX 파일시스템(FUSE)·WebDAV·Hadoop HDFS를 모두 지원하며,
GitHub 32,900 stars, Docker Hub 10M+ pulls의 활발한 오픈소스 프로젝트다.

BBW 서버에서는 v4.23이 Docker 컨테이너(`storage_seaweedfs`)로 운용 중이며,
`weed server -dir=/data -s3 -s3.port=8333` 명령으로 Master + Volume + Filer + S3가 통합 실행된다.

## 핵심 주장

- SeaweedFS는 단일 바이너리(`weed`)로 오브젝트·파일·S3·WebDAV·Hadoop을 모두 제공
- 볼륨 패킹(Volume Packing): 소형 파일을 큰 볼륨 파일로 집약 → 파일당 약 45바이트 오버헤드만 발생
- S3 게이트웨이는 상태 비저장 브리지 — Filer 메타데이터 스토어와 Volume Server 조합으로 S3 시맨틱 구현
- Filer 메타데이터가 손실되면 볼륨 데이터가 있어도 파일 경로 매핑 복구 불가 → 백업 필수
- MinIO AGPL 대비 Apache-2.0 라이선스로 상용 제약 없음; RAM 2-4GB로 홈서버에 적합

## 프로젝트 정보

| 항목 | 값 |
|---|---|
| GitHub | https://github.com/seaweedfs/seaweedfs |
| 라이선스 | Apache-2.0 |
| 언어 | Go 83.3%, Rust 6.2%, Templ 3.5%, Java 2.5% |
| 최신 버전 | 4.33 (2026-06-11 릴리즈) |
| BBW 운용 버전 | 4.23 |
| GitHub Stars | 32,900 |
| Docker Hub | `chrislusf/seaweedfs` (10M+ pulls, ~100MB 이미지) |
| 릴리즈 주기 | 거의 매주 |

## 아키텍처 — 3개 레이어

```
[Object Storage API]   S3 API Gateway   WebDAV   FUSE
                              ↓            ↓       ↓
[File Storage Layer]        Filer (경로 추상화 + 메타데이터)
                              ↓
[Blob Storage Layer]   Master Server ←→ Volume Server(s)
```

### Master Server (기본 포트: 9333 / gRPC: 19333)

- 클러스터 조정 허브. Raft 합의 프로토콜로 리더 선출.
- 역할: 파일 ID 할당, 볼륨 배치 결정, Volume Server 헬스체크.
- 클러스터 구성 시 홀수 개(1, 3, 5...) 필수.

### Volume Server (기본 포트: 8080 / gRPC: 18080)

- 실제 데이터 저장. 파일들을 큰 볼륨 파일로 패킹.
- 기본 볼륨 크기 상한: **30GB** (`-master.volumeSizeLimitMB`로 조절).
- 각 볼륨 = `.dat` (데이터) + `.idx` (16바이트 고정 인덱스 → O(1) 룩업).
- 초기화 시 기본 8개 볼륨 생성. 볼륨당 약 2-4GB RAM 사용.

### Filer Service (기본 포트: 8888 / gRPC: 18888)

- Blob Storage 위에 파일시스템 경로 추상화 제공.
- S3 버킷 → Filer 경로 `/buckets/<bucket_name>` 매핑.
- 메타데이터 백엔드: SQLite·LevelDB·RocksDB (로컬) / PostgreSQL·MySQL·Redis 등 15종+ (분산).
- AES256-GCM 투명 암호화 지원.

### S3 API Gateway (기본 포트: 8333)

- 상태 비저장 브리지. Filer 없이 독립 실행 불가.
- 주요 지원: 버킷 CRUD, 오브젝트 CRUD, 멀티파트 업로드, 버저닝, Presigned URL, IAM/STS, OIDC.
- 미지원: S3 Express One Zone, SelectObjectContent, Object Lambda, 웹사이트 호스팅 설정.

### WebDAV (기본 포트: 7333)

- Filer에 연결된 WebDAV 프로토콜 지원.

## BBW 운용 설정

### docker-compose.yml

```yaml
seaweedfs:
  image: chrislusf/seaweedfs
  container_name: storage_seaweedfs
  restart: unless-stopped
  command: "server -dir=/data -s3 -s3.port=8333"
  volumes:
    - ./data/seaweedfs:/data
```

- 포트: 노출(expose)만, 호스트 바인딩 없음 → Docker 내부 네트워크 전용
- `-s3` 플래그가 `-filer`도 자동 활성화
- S3 엔드포인트: `172.18.0.5:8333` (Docker 브리지 네트워크 내부 IP)

### 실제 실행 포트 (docker inspect 기준)

| 서비스 | 내부 포트 | gRPC 포트 | 비고 |
|---|---|---|---|
| Master | 9333 | 19333 | 클러스터 조정 |
| Volume | 8080 | 18080 | 데이터 저장 |
| Filer | 8888 | 18888 | 경로 메타데이터 |
| S3 | **8333** | - | 외부 접근 대상 |
| WebDAV | 7333 | - | |

### Caddy 연결 (외부 접근)

```caddyfile
snowball.me.kr {
    handle_path /s3* { reverse_proxy 172.18.0.5:8333 }
}
```

`https://snowball.me.kr/s3/` → SeaweedFS S3 API로 라우팅.

## 데이터 저장 구조 — Needle & Volume

### Needle (기본 저장 단위)

파일 1개 = Needle 1개. **불변(Immutable), 추가 전용(Append-only)**.

| 필드 | 크기 |
|---|---|
| Cookie (보안 토큰) | 4 bytes |
| Needle ID | 8 bytes |
| Size | 4 bytes |
| DataSize | 4 bytes |
| Flags | 1 byte |
| LastModified | 5 bytes |
| Checksum (CRC32) | 4 bytes |
| AppendAtNs (v3) | 8 bytes |
| 가변 필드 (파일명, MIME 등) | 가변 |

**고정 오버헤드: 약 45바이트/파일** → 수십억 파일도 효율적.

업데이트 시 기존 Needle에 deleted 플래그 → 볼륨 끝에 새 Needle 추가 (단편화 없음).
공간 회수: `weed compact` 명령으로 볼륨 압축.

### Erasure Coding (EC)

- Reed-Solomon RS(10,4): 10개 데이터 샤드 + 4개 패리티 샤드
- 30GB 볼륨 → 14개 EC 샤드 (각 3GB)
- 4개 샤드 손실까지 복구 가능
- 웜(warm) 스토리지, 콜드 데이터에 최적 (쓰기 성능 희생)
- 4.33 기준: per-shard 체크섬으로 비트롯(bitrot) 감지 지원

## 운용 모드

| 모드 | 명령 | 적합 용도 |
|---|---|---|
| `weed mini` | `weed mini` | 개인 홈서버·학습·프로토타이핑 (가장 간단) |
| `weed server` | `weed server -dir=/data -filer -s3` | 단일 노드 운영 수준 설정 |
| 풀 클러스터 | 컴포넌트 별도 기동 | HA 프로덕션 (Master 3개+ 필요) |

BBW는 `weed server` 모드 단일 노드로 운용.

## S3 인증 설정

S3 게이트웨이는 기본적으로 인증 없이 공개 접근. 인증 설정 시 JSON 파일 필요:

```json
{
  "identities": [
    {
      "name": "admin_user",
      "credentials": [{
        "accessKey": "your_access_key",
        "secretKey": "your_secret_key"
      }],
      "actions": ["Admin", "Read", "Write", "List", "Tagging"]
    }
  ]
}
```

```bash
weed server -s3.config=/etc/seaweedfs/s3.json
```

## AWS SDK 연동

```python
import boto3
s3 = boto3.client('s3',
    endpoint_url='http://seaweedfs-host:8333',
    aws_access_key_id='your_access_key',
    aws_secret_access_key='your_secret_key'
)
```

모든 S3 호환 클라이언트 그대로 사용 가능. 엔드포인트만 SeaweedFS 주소로 변경.
Presigned URL 완전 지원 (TTL 설정 가능).

## SeaweedFS vs MinIO 비교

| 항목 | SeaweedFS | MinIO |
|---|---|---|
| 라이선스 | **Apache-2.0** | AGPL-3.0 (상용 제한) |
| 설계 모델 | Master-Volume (Haystack 계열) | 분산 서버 풀 |
| 소형 파일 성능 | **매우 우수** (볼륨 패킹) | 상대적으로 취약 |
| S3 호환 범위 | 핵심 기능 지원, 일부 고급 기능 미지원 | **가장 포괄적** |
| RAM 요구량 | **2-4 GB**/볼륨서버 | 4-32 GB/노드 |
| 추가 프로토콜 | FUSE, WebDAV, Hadoop | S3 전용 집중 |
| 라이선스 추세 | 안정적 오픈소스 | 2025년 커뮤니티 Web UI 제거 등 제한 강화 |
| 홈서버 적합성 | **높음** | 중간 (AGPL·최소 4드라이브 요구) |

## 연결된 개념

- [[wiki/concepts/seaweedfs-architecture|SeaweedFS 아키텍처]]
- [[wiki/concepts/caddy|Caddy]] — SeaweedFS S3 엔드포인트의 역방향 프록시

## 연결된 엔티티

- [[wiki/entities/seaweedfs|SeaweedFS]] — 소프트웨어 엔티티
- [[wiki/entities/caddy|Caddy]] — 역방향 프록시

## 메모

- **중요**: Filer 메타데이터 DB(기본: LevelDB, `/data/` 아래)가 손실되면 파일 경로 복구 불가. `backup.sh`에 SeaweedFS 데이터 디렉토리 포함 여부 확인 필요.
- BBW의 `weed server` 명령에 `-ip.bind` 미설정 → Docker 내부 기본값으로 바인딩됨 (외부 노출 없음, 문제없음).
- SeaweedFS를 `weed server`로 실행하면 S3 플래그가 Filer도 자동 활성화함 (명시적 `-filer` 불필요).
- `weed mini`는 BBW 홈서버에 더 적합할 수 있음 (볼륨 크기 자동 튜닝 64-1024MB, 전체 컴포넌트 통합).
