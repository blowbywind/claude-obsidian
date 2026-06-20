---
date: 2026-06-20T02:21Z
task: Autobots 프로파일 상태 동기화
agent: autobots-scheduler
---

## 실행 결과

- **소스**: `/home/bbw/ai-ops/logs/health/agent-status.json` (updated: 2026-06-20T01:26Z)
- **대상**: `bot_profiles` (8개) + `runtime_providers` (4개)
- **결과**: 수정 0개 / 스킵 8개 - 이미 동기화된 상태

## 런타임 상태 (agent-status.json → runtime_providers)

| runtime | status | last_verified_at |
|---------|--------|------------------|
| claude | healthy | 2026-06-20 02:21:09 |
| codex | healthy | 2026-06-20 02:21:09 |
| agy | healthy | 2026-06-20 02:21:09 |
| obsidian-mcp | healthy | 2026-06-20 02:21:09 |
| run-gemini | unknown | 2026-06-19 14:02:00 (미체크 유지) |
| hermes-docker | - | DB에 없음 (드롭됨, 정상) |

## 인프라 상태

| 서비스 | 상태 |
|--------|------|
| autobots_backend:9200 | UP |
| hermes_dashboard:19119 | DOWN |
| ai_ops_ui:7771 | DOWN |

## 봇 프로파일 상태 (bot_profiles)

| 봇 | gateway | status |
|----|---------|--------|
| 눈꽃 (snow) | Antigravity | active |
| 로운 (roun) | Codex | active |
| 리나 (rina) | Antigravity | active |
| 키엘 (kiel) | Claude Code | active |
| 해리 (haeri) | Claude Code | active |
| 덱스 (dex) | Claude Code | active |
| 아서 (arthur) | Codex | active |
| 리안 (lian) | Antigravity | active |

모든 봇 `active` - 변경 없음.
