# Autobots — AI Native Operator Dashboard

상태: backend UP (healthy, 26min) | hermes-dashboard UP | ai-ops-ui UP | web_caddy UP | db_postgres UP | storage_seaweedfs UP | 봇 9/9 active
갱신: 2026-06-21T04:01Z (autobots-scheduler 위키-동기화)

## runtime_providers 상태 (2026-06-21T03:59Z 검증)
| ID | 상태 |
|----|------|
| agy | healthy |
| claude | healthy |
| codex | healthy |
| obsidian-mcp | healthy |
| run-gemini | unavailable |

## 배포 워크플로
- 프론트 변경: pnpm build -> 재시작 불필요
- 백엔드 코드 변경: docker compose build backend && docker compose up -d backend
- env var만 변경: docker compose up -d backend
- 주의: backend/*.ts 수정 후 up -d만 하면 구 이미지 실행 — 변경 미반영

## 서버 인프라
- Caddy -> autobots_backend:9200
- 정적파일: UI_DIR=/home/bbw/ai-ops/autobots/frontend/out
- Caddyfile: /opt/web-infra/Caddyfile

## 스택
- Backend: Fastify 5 + SQLite (node:sqlite) + tsx, Docker port 9200
- Frontend: Next.js 15 정적빌드 + Tailwind 4 + shadcn/ui + Zustand 5

## 프로젝트 워크스페이스 활동 (DB 기준, 2026-06-21T04:01Z)
| 프로젝트 | 최근 활동 | Obsidian 연동 |
|---------|-----------|--------------|
| autobots | 2026-06-21 03:35 UTC | synced |
| hnedu-erp | 2026-06-20 22:11 UTC | synced |
| hnedu-auth | 2026-06-19 12:02 UTC | synced |
| bbw-ebook | 2026-06-18 05:03 UTC | synced |
| hnedu-crm | 2026-06-15 21:51 UTC | synced |
| pdf-to-html | 2026-06-12 23:51 UTC | synced |
| firecrawl | 2026-06-11 12:00 UTC | synced |

## 봇 로스터 (DB 기준, 2026-06-21T04:01Z)
| ID | 이름 | gateway | 상태 | 모델 |
|----|------|---------|------|------|
| arthur | 아서 | Codex | active | gpt-5.5 |
| dex | 덱스 | Claude Code | active | claude-sonnet-4-6 |
| haeri | 해리 | Claude Code | active | claude-sonnet-4-6 |
| kiel | 키엘 | Claude Code | active | claude-sonnet-4-6 |
| lian | 리안 | Antigravity | active | gemini-3.5-flash |
| rina | 리나 | Antigravity | active | gemini-3.5-flash |
| roun | 로운 | Codex | active | gpt-5.5 |
| snow | 눈꽃 | Antigravity | active | gemini-3.5-flash |
| stellina | 스텔리나 | Claude Code | active | claude-sonnet-4-6 |

## 위키 동기화 최근 결과 (2026-06-21T04:01Z)
- Bot 상태: 9/9 active (변경 없음)
- Runtime: agy healthy | claude healthy | codex healthy | obsidian-mcp healthy | run-gemini unavailable
- runtime_providers last_verified_at: 2026-06-21 03:59:08
- 신규 커밋 (03:41Z 이후): a834631 fix(autobots): sudo 승인/거부 인가를 네트워크 출처 게이트로 전환
- DB 조회 기준: SQLite WAL checkpoint (Python sqlite3 직접 조회)
