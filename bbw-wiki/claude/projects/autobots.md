# Autobots — AI Native Operator Dashboard

상태: backend UP (healthy, 5h) | hermes-dashboard UP | ai-ops-ui UP | web_caddy UP | db_postgres UP | storage_seaweedfs UP | 봇 9/9 active | hermes Slack WebSocket DEGRADED
갱신: 2026-06-20T21:31Z (autobots-scheduler 위키-동기화)

## runtime_providers 상태 (2026-06-20T21:21Z 동기화)
| ID | 상태 |
|----|------|
| claude | healthy |
| codex | healthy |
| agy | healthy |
| obsidian-mcp | healthy |
| run-gemini | unavailable |

## 배포 워크플로
- **프론트 변경**: `pnpm build` → 재시작 불필요
- **백엔드 코드 변경**: `docker compose build backend && docker compose up -d backend`
- **env var만 변경**: `docker compose up -d backend`
- ⚠️ `backend/*.ts` 수정 후 `up -d`만 하면 구 이미지 실행 — 변경 미반영

## 서버 인프라
- Caddy → autobots_backend:9200
- 정적파일: UI_DIR=/home/bbw/ai-ops/autobots/frontend/out
- Caddyfile: /opt/web-infra/Caddyfile

## 스택
- Backend: Fastify 5 + SQLite (node:sqlite) + tsx, Docker port 9200
- Frontend: Next.js 15 정적빌드 + Tailwind 4 + shadcn/ui + Zustand 5

## 프로젝트 워크스페이스 활동 (DB 기준, 2026-06-20 21:01 UTC)
| 프로젝트 | 최근 활동 | Obsidian 연동 |
|---------|-----------|--------------|
| autobots | 2026-06-20 20:02 UTC | synced |
| hnedu-erp | 2026-06-20 16:24 UTC | synced |
| hnedu-auth | 2026-06-19 12:02 UTC | synced |
| bbw-ebook | 2026-06-18 05:03 UTC | synced |
| hnedu-crm | 2026-06-15 21:51 UTC | synced |
| pdf-to-html | 2026-06-12 23:51 UTC | synced |
| firecrawl | 2026-06-11 12:00 UTC | synced |



## 봇 로스터 (DB 기준, 2026-06-20 21:21 UTC)
| ID | 이름 | 상태 | 모델 | 최근 갱신 |
|----|------|------|------|---------|
| arthur | 아서 | active | gpt-5.5 | 2026-06-20T19:33Z |
| dex | 덱스 | active | claude-sonnet-4-6 | 2026-06-20T18:18Z |
| haeri | 해리 | active | claude-sonnet-4-6 | 2026-06-20T18:16Z |
| kiel | 키엘 | active | claude-sonnet-4-6 | 2026-06-20T19:16Z |
| lian | 리안 | active | gemini-3.5-flash | 2026-06-20T19:04Z |
| rina | 리나 | active | gemini-3.5-flash | 2026-06-20T18:33Z |
| roun | 로운 | active | gpt-5.5 | 2026-06-20T19:02Z |
| snow | 눈꽃 | active | gemini-3.5-flash | 2026-06-20T19:46Z |
| stellina | 스텔리나 | active | claude-sonnet-4-6 | 2026-06-20T19:06Z |

## 프로파일 동기화 최근 결과 (2026-06-20T21:21Z)
- Bot 상태: 9/9 active
- Runtime: claude:healthy | codex:healthy | agy:healthy | obsidian-mcp:healthy | run-gemini:unavailable
- Findings: 변경 없음 — 9 bots all at correct status
- 프로파일 변경: 0개 updated / 9개 skipped
- DB 직접 조회 기준 (autobots_backend Docker Up 5h+ healthy, localhost:9200 호스트 미노출 환경)