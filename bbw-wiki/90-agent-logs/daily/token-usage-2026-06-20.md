# 일일 토큰 사용량 집계 — 2026-06-20

> 집계 시각: 2026-06-20T01:03Z | 집계 주체: autobots-scheduler (token-usage-export)

## 개요

Claude Code 팀 요금제 기준 — 실제 토큰 수 대신 API 호출 횟수·이벤트 기반 집계.
(tokens_in/out 미수집: tokens_source=event_log)

---

## 2026-06-19 (어제) 집계

| 항목 | 값 | 비고 |
|------|-----|------|
| chat_success | 11건 | claude 런타임 채팅 완료 |
| learning_done | 9건 | 봇 9마리 자가학습 완료 |
| cron_success | 593건 | 성공률 98.8% (619건 중) |
| cron_error | 1건 | 비율 0.16% |
| cron_start | 619건 | |

### 봇별 자가학습 (2026-06-19)

| 봇 | 학습 완료 UTC |
|----|--------------|
| 해리 | 18:17 |
| 덱스 | 18:17 |
| 리나 | 18:32 |
| 로운 | 19:02 |
| 리안 | 19:02 |
| 키엘 | 19:17 |
| 아서 | 19:32 |
| 눈꽃 | 19:48 |

---

## 2026-06-20 (오늘, 부분 00:00~01:30 UTC)

| 항목 | 값 | 비고 |
|------|-----|------|
| chat_success | 2건 | 아서 챗 (00:31, 00:37 UTC) |
| learning_done | 1건 | 리나 자가학습 (00:09~00:11 UTC) |
| cron_success | 24건 | 에러 0건 |

---

## 7일 추세

| 날짜 | chat | learning | cron_ok | cron_err |
|------|------|---------|---------|---------|
| 2026-06-17 | 0 | 0 | 101 | 383 |
| 2026-06-18 | 0 | 13 | 527 | 66 |
| 2026-06-19 | 11 | 9 | 593 | 1 |
| 2026-06-20 (부분) | 2 | 1 | 24 | 0 |

---

## token_usage DB 업데이트

| date | agent | pipeline | calls |
|------|-------|---------|-------|
| 2026-06-19 | claude | chat | 11 |
| 2026-06-19 | claude | learning | 9 |
| 2026-06-20 | claude | chat | 2 |
| 2026-06-20 | claude | learning | 1 |

> tokens_in/out: NULL (팀 요금제 — 개별 토큰 계측 미지원)

---

## 특이사항

- 아서 봇 자정 직후 채팅 2건 처리 (00:31, 00:37 UTC)
- 리나 자가학습: Tailwind v4 Container Queries + WCAG 2.2 인사이트 2건 applied
- cron 에러 0건 (2026-06-19 대비 안정화)
- bot_evolutions: 리나 high insight 1건 pending (Base UI 도입 검토)
