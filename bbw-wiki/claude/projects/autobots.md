# Autobots — AI Native Operator Dashboard

상태: autobots_backend UP (healthy) | 봇 9/9 active | hermes-docker down (deprecated)
갱신: 2026-06-21T22:30Z (autobots-scheduler 위키-동기화)

## runtime_providers 상태 (2026-06-21T22:30Z 검증)
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

## 프로젝트 워크스페이스 활동 (DB 기준, 2026-06-21 14:01 UTC)
| 프로젝트 | 최근 활동 | Obsidian 연동 |
|---------|-----------|--------------|
| autobots | 2026-06-21 08:18 UTC | synced |
| hnedu-erp | 2026-06-21 11:09 UTC | synced |
| hnedu-auth | 2026-06-19 12:02 UTC | synced |
| bbw-ebook | 2026-06-18 05:03 UTC | synced |
| hnedu-crm | 2026-06-15 21:51 UTC | synced |
| pdf-to-html | 2026-06-12 23:51 UTC | synced |
| firecrawl | 2026-06-11 12:00 UTC | synced |

## 봇 로스터 (DB 기준, 2026-06-21T13:52Z)
| ID | 이름 | gateway | 상태 | 모델 |
|----|------|---------|------|------|
| arthur | 아서 | Codex | active | gpt-5.5 |
| dex | 덱스 | Claude Code | active | claude-sonnet-4-6 |
| haeri | 해리 | Claude Code | active | claude-sonnet-4-6 |
| kiel | 키엘 | Claude Code | active | claude-sonnet-4-6 |
| lian | 리안 | Antigravity | active | gemini-3.5-flash |
| rina | 리나 | Antigravity | active | gemini-3.5-flash |
| roun | 로운 | Codex | active | gpt-5.5 |
| snow | 눈꽃 | Claude Code | active | claude-sonnet-4-6 |
| stellina | 스텔리나 | Claude Code | active | claude-sonnet-4-6 |


## 위키 동기화 최근 결과 (2026-06-21T13:52Z)
- Bot 상태: 9/9 active (마지막 확인: 2026-06-21T13:52Z)
- Runtime: agy/claude/codex/obsidian-mcp=healthy | run-gemini=unavailable | hermes-docker down (deprecated)
- Vault: 762 md (+3 since 13:42Z) | session-log: 23274라인 (+208) | 90-agent-logs: 275 md (+3) | claude/: 37 md (=)
- ai-ops 최신 커밋: 94aeb81 (auto-save), 신규 커밋 없음


## 프로파일 동기화 최근 결과 (2026-06-21T13:52Z)
- Bot 상태: 9/9 active
- Runtime: agy/claude/codex/obsidian-mcp healthy | run-gemini unavailable | hermes-docker down (deprecated)
- WARN: autobots_backend 재시작 감지 (Up 32s at sync) — 이후 healthy 복귀
- Findings: 변경 없음 -- 9 bots all active
- 프로파일 변경: 0개 updated / 9개 skipped
- agent-status.json 기준: 2026-06-21T13:52Z