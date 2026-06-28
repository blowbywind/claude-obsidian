---
title: SeaweedFS
type: entity
tags: [product, object-storage, s3, open-source, go]
created: 2026-06-12
updated: 2026-06-12
sources: [2026-06-12-seaweedfs-docs]
summary: "소형 파일 최적화 분산 오브젝트 스토리지로 S3·FUSE·WebDAV·Hadoop을 지원하는 Apache-2.0 오픈소스."
---

## 개요

Go로 작성된 Apache-2.0 오픈소스 분산 오브젝트 스토리지. Facebook Haystack 논문에서 영감을 받아
수십억 개의 소형 파일을 O(1) 디스크 접근·45바이트 오버헤드만으로 처리하도록 설계됐다.
단일 바이너리(`weed`)로 S3 API·POSIX 파일시스템(FUSE)·WebDAV·Hadoop HDFS·Data Lakehouse(Iceberg)를 모두 제공.

| 항목 | 값 |
|---|---|
| GitHub | https://github.com/seaweedfs/seaweedfs |
| 라이선스 | Apache-2.0 |
| 최신 버전 | 4.33 (2026-06-11) |
| GitHub Stars | 32,900 |
| Docker Hub | `chrislusf/seaweedfs` (10M+ pulls) |

## BBW 운용 현황

| 항목 | 값 |
|---|---|
| 컨테이너 | `storage_seaweedfs` |
| 버전 | v4.23 |
| 실행 명령 | `server -dir=/data -s3 -s3.port=8333` |
| 데이터 경로 | `/opt/web-infra/data/seaweedfs/` |
| S3 내부 엔드포인트 | `172.18.0.5:8333` (Docker 내부망) |
| 외부 접근 | `https://snowball.me.kr/s3/` (Caddy 역프록시) |
| 인증 | 미설정 (내부 전용) |

**포트 (expose only, 호스트 바인딩 없음)**:

| 서비스 | HTTP | gRPC |
|---|---|---|
| Master | 9333 | 19333 |
| Volume | 8080 | 18080 |
| Filer | 8888 | 18888 |
| S3 | 8333 | - |
| WebDAV | 7333 | - |

## 핵심 아키텍처

```
S3 API / FUSE / WebDAV / Hadoop
            ↓
        Filer (경로 메타데이터)
            ↓
  Master ←→ Volume Server(s)
 (조정·ID 할당)  (실제 데이터)
```

- **Master**: Raft 합의, 파일 ID 할당, 볼륨 배치 결정
- **Volume**: Needle 패킹으로 소형 파일 집약 (30GB 기본 볼륨)
- **Filer**: 경로↔파일ID 매핑 메타데이터 관리 (SQLite, PostgreSQL 등)
- **S3 게이트웨이**: 상태 비저장 브리지 (Filer 필요)

→ 상세: [[wiki/concepts/seaweedfs-architecture|SeaweedFS 아키텍처]]

## 주요 특징

- **소형 파일 최적화**: 파일당 약 45바이트 오버헤드, 볼륨 패킹으로 소형 파일 수십억 개 처리
- **Apache-2.0**: MinIO AGPL 대비 상용 제약 없음
- **저사양 운용**: RAM 2-4GB/볼륨서버로 충분 (MinIO는 4-32GB/노드)
- **S3 호환**: AWS SDK 그대로 사용, Presigned URL·멀티파트·버저닝 지원
- **Erasure Coding**: RS(10,4) — 4개 샤드 손실 허용 (콜드 데이터용)
- **Filer 메타데이터 백엔드**: SQLite~PostgreSQL~Redis 등 15종+ 교체 가능

## SeaweedFS vs MinIO

| 항목 | SeaweedFS | MinIO |
|---|---|---|
| 라이선스 | Apache-2.0 ✅ | AGPL-3.0 (상용 제한) |
| 소형 파일 | **최강** | 취약 |
| S3 호환 범위 | 핵심 지원 | 가장 포괄적 |
| RAM 요구량 | **2-4 GB** | 4-32 GB |
| 홈서버 적합성 | **높음** | 중간 |

## 주의사항

- **Filer 메타데이터 백업 필수**: 메타데이터 손실 시 볼륨 데이터가 있어도 파일 경로 복구 불가
- S3 인증 미설정 시 공개 접근 가능 → 내부 네트워크 전용이면 문제 없음
- `weed server` + `-s3` 플래그 → Filer 자동 활성화 (명시적 `-filer` 불필요)

## 주요 연결

- [[wiki/concepts/seaweedfs-architecture|SeaweedFS 아키텍처]] — 레이어별 상세 구조
- [[wiki/entities/caddy|Caddy]] — S3 엔드포인트 역방향 프록시
- [[wiki/sources/2026-06-12-hermes-external-access|web-infra 설정]] — Docker Compose 운용 환경

## 출처

- [[wiki/sources/2026-06-12-seaweedfs-docs]] — 종합 문서 (GitHub Wiki + DeepWiki + 벤치마크)
