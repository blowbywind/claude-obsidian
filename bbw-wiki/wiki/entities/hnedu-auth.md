---
title: hnedu-auth
type: entity
tags: [project, hnedu, auth, fastify, nextjs, service]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-hnedu-auth-project]
---

## 개요

해냄에듀 사내 **통합 인증 서비스**. 직원 계정·부서·직급·시스템별 역할을 단일 서비스에서 관리하고 JWT(RS256)를 발급한다. ERP·CRM 등 사내 시스템은 이 서비스의 공개키로 토큰을 검증한다.

## 인프라

| 항목 | 값 |
|------|-----|
| 서버 IP | 192.168.0.221 (LAN) |
| SSH 별칭 | `hnedu-server` |
| 서버 경로 | `/var/web-infra/hnedu_auth/` |
| 외부 도메인 | `auth.snowball.me.kr` |
| 백엔드 포트 | 3100 (Fastify) |
| 관리자 UI 포트 | 3200 (Next.js 15, 로컬 개발 시) |
| DB | PostgreSQL PG17 (Docker `db_postgres`) |
| 프로세스 관리 | Docker Compose (`hnedu_auth` 컨테이너) |

## 스택

| 영역 | 기술 |
|------|------|
| 백엔드 | Node.js 20 + Fastify + Prisma ORM |
| 인증 | JWT RS256 / bcrypt(cost 12) / Refresh Token(SHA-256 해시) |
| PII 보호 | AES-256-GCM (pgcrypto) — 전화번호 |
| 관리자 UI | Next.js 15 App Router + Tailwind CSS + Zustand |
| 디자인 시스템 | Warp 다크 테마 (`docs/DESIGN.md`) |

## 아키텍처 규칙

- **수정 대상**: `admin-ui/` (Next.js 소스)
- **절대 금지**: `public/admin/` 직접 편집 — 빌드 시 전체 교체됨
- `/admin/*` 라우트: `requireAdmin` 미들웨어 필수
- 권한 분기: `systems.*` 배열만 사용, `job_title`·`department_path`는 표시 전용
- 역할·상태 변경 시 해당 직원 refresh_tokens 전체 revoke

## 배포 절차

```bash
# 1. 빌드
cd admin-ui && pnpm build

# 2. 서버 업로드
scp -r public/admin hnedu-server:/var/web-infra/hnedu_auth/public/

# 3. 상태 확인
ssh hnedu-server "docker logs hnedu_auth --tail 10"
```

## 현재 상태 (2026-06-05 기준)

- Phase 1~11 완료, 실서비스 연동 대기
- admin-ui: Next.js 15로 리빌드 진행 중 (Phase 11은 Vanilla JS SPA였음)
- 잔여: ERP·CRM 실제 엔드포인트 통합 테스트

## 주요 연결

- [[wiki/concepts/hnedu-auth-deploy|배포 워크플로우]]
- [[wiki/concepts/jwt-rs256|JWT RS256 패턴]]
- [[wiki/entities/hnedu-erp|hnedu-erp]]
- [[wiki/entities/hnedu-crm|hnedu-crm]]

## 출처

- [[wiki/sources/2026-06-05-hnedu-auth-project]]
