---
date: 2026-06-19
time: "07:51 UTC"
task: 프로파일 상태 동기화
scheduler: autobots-scheduler
---

# Autobots 프로파일 상태 동기화 — 2026-06-19

## 결과 요약

- **봇 수정**: 0개 (모두 이미 active 상태)
- **스킵**: 8개 (변경 불필요)

## agent-status.json (2026-06-19T07:11Z)

| Runtime | 상태 |
|---------|------|
| claude | healthy |
| codex | healthy |
| agy | healthy |
| hermes-docker | down (DB에 없음 — 제거됨) |
| obsidian-mcp | healthy |

## bot_profiles 최종 상태

| id | 이름 | gateway | status |
|----|------|---------|--------|
| snow | 눈꽃 | Antigravity | active |
| roun | 로운 | Codex | active |
| rina | 리나 | Antigravity | active |
| kiel | 키엘 | Claude Code | active |
| haeri | 해리 | Claude Code | active |
| dex | 덱스 | Claude Code | active |
| arthur | 아서 | Codex | active |
| lian | 리안 | Antigravity | active |

## runtime_providers 최종

| id | status | last_verified |
|----|--------|---------------|
| agy | healthy | 2026-06-19 07:51:02 |
| claude | healthy | 2026-06-19 07:51:02 |
| codex | healthy | 2026-06-19 07:51:02 |
| obsidian-mcp | healthy | 2026-06-19 07:51:02 |
| run-gemini | unknown | 2026-06-19 07:01:37 |

## 비고

- hermes-docker: docker stop hermes (2026-06-14 P0-A 완료) — DB에서 제거됨
- run-gemini: agent-status.json에 없음 → status unknown 유지

---

## 08:20 UTC 재실행 결과 (autobots-scheduler)

- **Backend**: UP (9200)
- **봇**: 8/8 active (변경 없음)
- **Runtime healthy**: agy / claude / codex / obsidian-mcp
- **Runtime unknown**: run-gemini (유지)
- **last_verified_at**: 2026-06-19 08:10:54 UTC
- **인프라**: 9200 UP | 19119 DOWN | 7771 DOWN

---

## 11:12 UTC 재실행 결과 (autobots-scheduler)

- **Backend**: UP (9200 /health OK)
- **봇**: 8/8 active (변경 없음)
- **Runtime healthy**: agy / claude / codex / obsidian-mcp
- **Runtime unknown**: run-gemini (유지, agent-status.json 미포함)
- **hermes-docker**: DB에 없음 (SKIP)
- **last_verified_at**: 2026-06-19 11:12:48 UTC
- **봇 수정**: 0개 / **스킵**: 8개

---

## 12:12 UTC 재실행 결과 (autobots-scheduler)

- **Backend**: UP (9200)
- **봇**: 8/8 active (변경 없음)
- **Runtime healthy**: agy / claude / codex / obsidian-mcp
- **Runtime unknown**: run-gemini (유지)
- **hermes-docker**: DB에 없음 (SKIP)
- **last_verified_at**: 2026-06-19
- **봇 수정**: 0개 / **스킵**: 8개
- **agent_definitions 변경**: 0개
