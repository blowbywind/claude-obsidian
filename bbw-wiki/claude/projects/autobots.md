# Autobots — AI Native Operator Dashboard

상태: autobots_backend UP (healthy) | 봇 9/9 active | hermes-docker down (deprecated)
갱신: 2026-06-27T01:01Z

## 최근 변경
- 2026-06-27: 독립 `Tasks` 제품 표면을 제거하고 작업 생성·승인·실행 추적을 `Pipelines`로 통합. `[[TASK]]` 디렉티브는 인박스 카드가 아니라 `pipeline_runs`를 생성한다. 결정 기록: [[2026-06-27-autobots-tasks-to-pipelines]]

## runtime_providers 상태 (DB 기준, 2026-06-24T23:40Z 검증)
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

## 프로젝트 워크스페이스 활동 (DB 기준, 2026-06-24 23:45 UTC)
| 프로젝트 | 최근 활동 | Obsidian 연동 |
|---------|-----------|--------------|
| autobots | 2026-06-24 23:18 UTC | synced |
| hnedu-erp | 2026-06-24 08:54 UTC | synced |
| hnedu-auth | 2026-06-19 12:02 UTC | synced |
| bbw-ebook | 2026-06-18 05:03 UTC | synced |
| hnedu-crm | 2026-06-15 21:56 UTC | synced |
| pdf-to-html | 2026-06-12 23:51 UTC | synced |
| firecrawl | 2026-06-11 12:00 UTC | synced |

## 봇 로스터 (DB 기준, 2026-06-24T23:40Z)
| ID | 이름 | gateway | 상태 | 모델 |
|----|------|---------|------|------|
| arthur | 아서 | Codex | active | gpt-5.5 |
| dex | 덱스 | Claude Code | active | claude-opus-4-8 |
| haeri | 해리 | Claude Code | active | claude-opus-4-8 |
| kiel | 키엘 | Claude Code | active | claude-opus-4-8 |
| lian | 리안 | Antigravity | active | gemini-3.5-flash |
| rina | 리나 | Antigravity | active | gemini-3.5-flash |
| roun | 로운 | Codex | active | gpt-5.5 |
| snow | 눈꽃 | Claude Code | active | claude-opus-4-8 |
| stellina | 스텔리나 | Claude Code | active | claude-opus-4-8 |

## 위키 동기화 최근 결과 (2026-06-24T23:31Z)
- Bot 상태: 9/9 active | Runtime: agy=healthy | claude=healthy | codex=healthy | obsidian-mcp=healthy | run-gemini=unavailable
- Vault: 1122 md (-61 since 1183) | session-log: 4412라인 (+229 since 4183) | 90-agent-logs: 607 md (daily:598) | claude/: 49 md (=)
- wiki/: 372 md (concepts:181, entities:37, sources:32, queries:2)
- 무결성 스캔: 깨진 wikilink 17고유/36총, frontmatter 누락 0, 고아 노트 8 -> `90-agent-logs/weekly/integrity-2026-W26.md`
- ai-ops git: 305a950 | docker: 현재 실행 환경에 없음

## 프로파일 동기화 최근 결과 (2026-06-24T23:40Z)
- Bot 상태: 9/9 active | Runtime: agy=healthy | claude=healthy | codex=healthy | obsidian-mcp=healthy | run-gemini=unavailable
- Runtime: agy=healthy, claude=healthy, codex=healthy, obsidian-mcp=healthy
- Findings: 변경 없음 — 9 bots all at correct status
- 프로파일 변경: 0개 updated / 9개 skipped
- agent-status.json 기준: 2026-06-24T23:37:23Z
