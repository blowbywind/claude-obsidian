# 일일 토큰 사용량 집계 — 2026-06-21

> 집계 시각: 2026-06-20T16:00Z | 집계 주체: autobots-scheduler (token-usage-export)

## 개요

Claude Code 팀 요금제 기준 — 실제 토큰 수 대신 API 호출 횟수·이벤트 기반 집계.
(tokens_in/out 미수집: tokens_source=event_log)

---

## 2026-06-20 (어제, 전일 KST 집계)

| 항목 | 값 | 비고 |
|------|-----|------|
| chat_success | 2건 | 아서 챗 (UTC 00:31, 00:37) |
| learning_done | 1건 | 리나 자가학습 (UTC 00:09~00:11) |
| cron_success | 136건 | 에러 0건 (성공률 100%) |
| cron_error | 0건 | 전날(06-19) 1건 대비 개선 |
| profile_sync | 31건 | health JSON 기준 |
| memory_stats_update | 27건 | memory-stats-2026-06-20-01 ~ 27 |

### 봇별 활동 (2026-06-20)

| 봇 | 활동 |
|----|------|
| 아서 | chat 2건 (UTC 00:31, 00:37) |
| 리나 | learning 1건 — Tailwind v4 + WCAG 2.2 인사이트 2건 applied |
| 기타 7봇 | active 유지, 별도 이벤트 없음 |

### Vault 종료 상태 (2026-06-20 KST 23:47 = UTC 14:47)

| 항목 | 값 |
|------|-----|
| vault total md | 489 |
| vault total all | 533 |
| session-log | 7,064라인 |
| ai-ops memory | 11파일, 992라인 |

---

## 2026-06-21 (오늘, 부분 집계 00:00~01:00 KST)

| 항목 | 값 | 비고 |
|------|-----|------|
| chat_success | 0건 | - |
| learning_done | 0건 | - |
| cron_success | 16건 | 에러 0건 |
| cron_error | 0건 | - |
| profile_sync | 3건 | UTC 15:11, 15:52, 15:53 |
| memory_stats_update | 2건 | UTC 15:17, 15:35 |

### 인프라 상태 (2026-06-21 00:56 KST = UTC 15:56)

| 서비스 | 상태 | 비고 |
|--------|------|------|
| autobots_backend:9200 | UP (healthy) | 15:30Z 일시 DOWN -> 15:51Z 복귀 |
| hermes_dashboard:19119 | UP | Up 6d |
| ai_ops_ui:7771 | UP | Up 6d |
| web_caddy | UP | Up 6d |
| db_postgres | UP | Up 6d |
| storage_seaweedfs | UP | Up 6d |

봇 상태: 9/9 active (아서/덱스/해리/키엘/리안/눈꽃/로운/리나/스텔리나)

---

## 7일 추세

| 날짜 | chat | learning | cron_ok | cron_err |
|------|------|---------|---------|---------|
| 2026-06-17 | 0 | 0 | 101 | 383 |
| 2026-06-18 | 0 | 13 | 527 | 66 |
| 2026-06-19 | 11 | 9 | 593 | 1 |
| 2026-06-20 | 2 | 1 | 136 | 0 |
| 2026-06-21 (부분) | 0 | 0 | 16 | 0 |

> cron_err 추세: 383 -> 66 -> 1 -> 0 (연속 이틀 0건, 안정화)

---

## token_usage DB 업데이트

| date | agent | pipeline | calls |
|------|-------|---------|-------|
| 2026-06-20 | claude | chat | 2 |
| 2026-06-20 | claude | learning | 1 |
| 2026-06-20 | autobots-scheduler | cron | 136 |
| 2026-06-21 (부분) | autobots-scheduler | cron | 16 |

> tokens_in/out: NULL (팀 요금제 — 개별 토큰 계측 미지원)

---

## 특이사항

- autobots_backend:9200 15:30Z 일시 DOWN -> 15:51Z 자동 복귀 (약 21분, 재시작 추정)
- 2026-06-20: cron_error 0건 — 3일 연속 안정화 추세 확립
- 2026-06-20: learning 이벤트 미미 (1건), 자가학습 봇 활성화 필요 검토
- profile_sync 31건 (06-20 KST 전일): 정상 범위 (시간당 약 1.3건)
