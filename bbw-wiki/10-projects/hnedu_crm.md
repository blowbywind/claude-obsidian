---
title: "hnedu_crm — 교사 CRM"
id: "P-02"
status: "기획중"
phase: "Phase 1"
stack: [Next.js, Fastify, PostgreSQL, Python, Docker]
created: 2026-06-13
updated: 2026-06-15
summary: "전국 41,264명 교사 관계 정보 통합 관리 및 교과서 채택률 향상을 목표하는 Phase 1 프로토타입(Next.js/Fastify/PostgreSQL + hnedu_auth 의존)."
---

## 현재 상태

- **Phase**: Phase 1 — 프로토타입 운영 중 (Phase 2 개발 준비)
- **진행 상황**: 전국 41,264명 교사 관계 정보 통합 관리, 교과서 채택률 향상 목적

## 서버 / 인프라

| 항목 | 값 |
|------|-----|
| 프로토타입 | `frontend/prototype/index.html` (Vanilla HTML SPA) |
| Phase 2+ | Docker Compose (PostgreSQL 17, Redis) |
| DB | PostgreSQL + TimescaleDB |
| 인증 의존 | hnedu_auth (JWT RS256) |

## 스택

- 언어/프레임워크: Next.js 15 (frontend), Fastify (backend), Python (AI 서비스)
- DB: PostgreSQL 17 + TimescaleDB, Redis
- 인증: hnedu_auth JWT 검증

## 에이전트 허용 범위

| 에이전트 | 허용 | 금지 |
|---------|------|------|
| Claude Code | 설계·검토·문서화 | credential 파일 읽기 |
| Codex | `/home/bbw/projects/hnedu_crm/` 수정 | .env 읽기 |
| agy | 리서치만 | 코드 수정 불가 |

## Dev Gate

```bash
cd /home/bbw/projects/hnedu_crm
cd frontend && pnpm install
cd ../backend && pnpm install
cd ../ai-service && python3 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt
cd ../infra && docker compose up -d
```

## 위험 구역

- hnedu_auth JWT 공개키 의존 → auth 변경 시 반드시 동기화
- 교사 개인정보 포함 — 로그에 식별 정보 출력 금지

## 자주 쓰는 명령

```bash
# 프로토타입 확인
open frontend/prototype/index.html

# Docker 인프라
cd infra && docker compose up -d

# 기획서 확인
cat docs/PLAN.md
```

## 최근 작업

- 기획 중 (Phase 1)

## 다음 작업

- [ ] Phase 2 스택 확정

<!-- night-learn-status -->
> 자동 상태 요약 (2026-06-15): 
