# 봇 상태 로그 - 2026-06-22

> autobots-scheduler가 5분 간격으로 자동 기록

| 시각 | autobots_backend | hermes-dashboard | ai-ops-ui | web_caddy | 비고 |
|------|-----------------|-----------------|-----------|-----------|------|
| 03:25 | healthy (Up 5h) | Up 7d WARN | Up 7d | Up 15h | 봇 9/9 active, /health failures:0 — hermes: Slack WebSocket Session closed 지속(자동재시도, 재시작 0회), run-gemini unavailable(예정), sudo job polling 200 |
| 03:31 | healthy (Up 5h) | Up 7d | Up 7d | Up 15h | 봇 9/9 active, /health ok — runtimes: agy/claude/codex/obsidian-mcp healthy, run-gemini unavailable(계속) |
| 04:46 | healthy (Up 15m) | Up 7d WARN | Up 7d | Up 16h | 봇 9/9 active, /health failures:0 — **backend 재시작 감지**(이전 Up 5h→현재 Up 15m), hermes: RuntimeError Session is closed 지속(자동재시도), run-gemini unavailable(예정) |
| 07:45 | healthy (Up 3h) | Up 7d WARN | Up 7d | Up 19h | 에이전트 16/16 active, /health ok failures:0 — hermes: RuntimeError Session is closed 지속(재시작 0회, 자동재시도), image-agent 마지막 실행 2026-06-20, 나머지 15개 에이전트 미실행 |
| 08:06 | healthy (Up 4h) | Up 7d | Up 7d | Up 19h | 봇 9/9 active, /health ok — runtimes: agy/claude/codex/obsidian-mcp healthy, run-gemini unavailable(계속), sudo polling 정상 |
- 2026-06-22 08:31 KST | health=HEALTHY | total=9 | active=9 | inactive=0 | ALL OK
| 일일점검 | healthy (Up 4h) | Up 7d WARN | Up 7d | Up 20h | 봇 9/9 active — run-gemini unavailable(2026-06-19 14:02, 3일째), hermes: Session closed 지속(자동재시도), backend 재시작 4회 누적, 디스크 18%/메모리 7.2G/14G 정상 |

| 00:01 UTC | healthy (Up 5h) | Up 7d WARN | Up 7d | Up 20h | 봇 9/9 active — runtimes: agy/claude/codex/obsidian-mcp healthy, run-gemini unavailable(72h+) / 415 Unsupported Media Type 반복 / ERR_HTTP_HEADERS_SENT 2건 / disk 18% |
- 2026-06-22 00:01 UTC | health=WARN | total=9 | active=9 | inactive=0 | issues: run-gemini unavailable(72h+), 415 errors, ERR_HTTP_HEADERS_SENT
- 2026-06-22 00:16 UTC | health=OK | total=9 | active=9 | inactive=0 | backend Up 5h healthy, runtimes: agy/claude/codex/obsidian-mcp healthy, run-gemini unavailable(ongoing)
