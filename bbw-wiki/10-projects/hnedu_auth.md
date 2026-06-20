---
title: "hnedu_auth — 통합 인증 서비스"
id: "P-01"
status: "개발중"
phase: "Phase 1"
stack: [Fastify, Node.js, Prisma, PostgreSQL, JWT-RS256, Docker]
created: 2026-06-13
updated: 2026-06-18
---

## 현재 상태

- **Phase**: Phase 1 — 개발 중
- **진행 상황**: 직원 계정·부서·직급·역할 통합 관리 + JWT(RS256) 발급 서비스

## 서버 / 인프라

| 항목 | 값 |
|------|-----|
| SSH 별칭 | `hnedu-server` |
| 서버 IP | 192.168.0.221 (LAN) |
| 서버 경로 | `/var/web-infra/hnedu_auth/` |
| 외부 도메인 | `auth.snowball.me.kr` |
| 헬스체크 URL | `https://auth.snowball.me.kr/health` |
| DB | PostgreSQL (TimescaleDB PG17, Docker `db_postgres`) |
| 배포 | Docker Compose (`hnedu_auth` 컨테이너) |

## 스택

- 언어/프레임워크: Node.js 20, Fastify
- ORM: Prisma
- DB: PostgreSQL 17 (TimescaleDB)
- 인증: JWT RS256
- 배포: Docker Compose

## 에이전트 허용 범위

| 에이전트 | 허용 | 금지 |
|---------|------|------|
| Claude Code | 설계·검토·문서화 | credential 파일 읽기 |
| Codex | `/home/bbw/projects/hnedu_auth/` 수정 | .env·keys/*.pem 읽기 |
| agy | 리서치만 | 코드 수정 불가 |

## Dev Gate

```bash
cd /var/web-infra/hnedu_auth
pnpm install --allow-build=@prisma/client,@prisma/engines,bcrypt,esbuild,prisma
# 키 생성 (최초 1회)
openssl genrsa -out keys/private.pem 2048
openssl rsa -in keys/private.pem -pubout -out keys/public.pem
node_modules/.bin/prisma migrate dev --name init
pnpm db:seed
```

## 위험 구역

- JWT 키 로테이션: hnedu_crm, hnedu_erp 모두 영향
- 공개키 변경 시 → hnedu_crm·hnedu_erp 동기 업데이트 필수
- API 스펙 변경 → auth-change-policy.md 확인

## 자주 쓰는 명령

```bash
# Docker Compose 재시작
cd /var/web-infra && docker compose restart hnedu_auth

# 마이그레이션
cd /var/web-infra/hnedu_auth && pnpm prisma migrate dev

# 로그
docker logs hnedu_auth --tail=50 -f
```

## 최근 작업

- **2026-06-11**: 보안 감사 (ultracode Workflow) — INJ 10개 + JWT-007 + XSS 파일 제거 (총 13개 취약점 패치)
- **2026-06-11**: admin-ui 관리자 무한 루프 버그 수정 (`isAdminToken()` 추가)
- **2026-06-11**: 서버 배포 완료 (`docker compose restart hnedu-auth` 정상 확인)

## 보안 현황 (2026-06-11 기준)

- 패치 완료: INJ 10개 + JWT-007(15m TTL) + XSS 파일 제거
- 수용된 미구현: JWT-009 블랙리스트 (JWT-007 15m TTL로 실질적 완화)
- 잔여: 실서비스 연동 후 ERP/CRM 통합 테스트

## 다음 작업

- [ ] hnedu_auth 배포 런북 작성 (PM-2)
- [ ] hnedu_auth 의존 관계 영향 분석 (PM-3)
- [ ] JWT-009 블랙리스트 구현 검토 (실서비스 연동 후)
