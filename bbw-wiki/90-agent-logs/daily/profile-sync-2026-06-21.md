---
date: 2026-06-21
time: "17:54 UTC"
task: profile-sync
scheduler: autobots-scheduler
---

## 결과

봇 수정: 0개 / 스킵: 9개

## bot_profiles

| id | 이름 | gateway | status |
|----|------|---------|--------|
| arthur | 아서 | Codex | active |
| dex | 덱스 | Claude Code | active |
| haeri | 해리 | Claude Code | active |
| kiel | 키엘 | Claude Code | active |
| lian | 리안 | Antigravity | active |
| rina | 리나 | Antigravity | active |
| roun | 로운 | Codex | active |
| snow | 눈꽃 | Antigravity | active |
| stellina | 스텔리나 | Claude Code | active |

## runtime_providers

| 런타임 | 상태 | last_verified_at |
|--------|------|-----------------|
| claude | healthy | 2026-06-21 17:54 UTC |
| codex | healthy | 2026-06-21 17:54 UTC |
| agy | healthy | 2026-06-21 17:54 UTC |
| obsidian-mcp | healthy | 2026-06-21 17:54 UTC |
| run-gemini | unavailable | 2026-06-19 14:02 UTC |

## findings

- bot_profiles: 9/9 active - 변경 없음 (all runtimes healthy)
- run-gemini: unavailable 유지 (agent-status 미등록)
- stellina: 신규 봇 (6-20 추가) 정상 동기화됨

## 비고

- node:sqlite (Node.js v22 experimental) WAL 호환 이슈 감지
  - npx tsx sync-profiles.ts 실행 시 DB 데이터 0행으로 읽힘
  - Python sqlite3로 WAL checkpoint(PASSIVE) 후 동기화 수행
  - autobots_backend 컨테이너(9200) 현재 미가동 상태
