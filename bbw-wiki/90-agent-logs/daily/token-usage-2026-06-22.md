# 일일 토큰 사용량 집계 -- 2026-06-22

> 집계 시각: 2026-06-22T00:00Z | 집계 주체: autobots-scheduler (daily-token-aggregation)

## 개요

Claude Code 팀 요금제 기준 -- 실제 토큰 수 대신 API 호출 횟수·이벤트 기반 집계.
(tokens_in/out 미수집: tokens_source=event_log)

---

## 2026-06-21 (어제) 전일 집계

| 항목 | 값 | 비고 |
|------|-----|------|
| chat_success | 26건 | 5개 봇 활동 |
| learning_done | 0건 | 자가학습 없음 |
| tool_use | 29건 | snow:16, kiel:13 |
| cron_success | 334건 | start 350건 대비 성공률 95.4% |
| cron_error | 16건 | 실패율 4.6% |
| profile_sync | 58건 | autobots-profile-sync 크론 |
| memory_stats_update | 41건 | memory-stats-update 크론 |
| bot_status_check | 190건 | 최다 실행 크론 |
| obsidian_sync | 28건 | obsidian-sync 크론 |
| project_activity_scan | 14건 | project-activity-scan 크론 |
| token_usage_export | 1건 | 이 집계 포함 |

### 봇별 chat_success (2026-06-21)

| 봇 | 건수 | 활동 시간대 (UTC) |
|----|------|----------------|
| 키엘 (kiel) | 10 | 00:00, 04:00 |
| 로운 (roun) | 10 | 08:00~11:00 |
| 아서 (arthur) | 2 | 06:00 |
| 리나 (rina) | 2 | 07:00, 11:00 |
| 눈꽃 (snow) | 2 | 00:00, 08:00 |

### sudo 요청 (2026-06-21)

| 타입 | 건수 |
|------|------|
| sudo_pending | 28 |
| sudo_user_denied | 24 |
| sudo_auto | 5 |
| sudo_approved | 2 |
| sudo_denied | 2 |

### 위키 활동 (2026-06-21)

| 타입 | 건수 |
|------|------|
| wiki_modify | 1,669 |
| wiki_create | 158 |
| wiki_lint_warn | 158 |
| wiki_delete | 12 |

---

## 2026-06-22 (오늘, 집계 기준 00:00Z)

| 항목 | 값 | 비고 |
|------|-----|------|
| chat_success | 0건 | 미집계 |
| cron_success | 0건 | DB 갱신 전 |
| token_usage 레코드 | 0건 | -- |

> DB 마지막 이벤트: 2026-06-21T16:00Z. 오늘 데이터는 다음 집계 시 반영.

---

## 7일 추세

| 날짜 | chat | learning | cron_ok | cron_err |
|------|------|---------|---------|---------|
| 2026-06-17 | 0 | 0 | 101 | 384 |
| 2026-06-18 | 0 | 13 | 527 | 83 |
| 2026-06-19 | 11 | 9 | 593 | 26 |
| 2026-06-20 | 56 | 0 | 524 | 13 |
| 2026-06-21 | 26 | 0 | 334 | 16 |

> chat 추세: 0->0->11->56->26 (활성화 지속)
> cron 안정화: 384->83->26->13->16 (안정 구간 진입)

---

## token_usage DB 상태

| date | agent | pipeline | calls |
|------|-------|---------|-------|
| 2026-06-20 | claude | chat | 2 |
| 2026-06-20 | claude | learning | 1 |
| 2026-06-19 | claude | chat | 11 |
| 2026-06-19 | claude | learning | 9 |
| 2026-06-21 ~ 22 | -- | -- | 0 (미삽입) |

> tokens_in/out: NULL (팀 요금제 -- 개별 토큰 계측 미지원)
> 2026-06-21 이후 token_usage INSERT 자동화 중단 상태 (이벤트 로그는 정상 축적)

---

## 특이사항

- 자가학습(learning_done) 2일 연속 0건 -- 봇 자가학습 스케줄러 점검 필요
- sudo_user_denied 24건 (pending 28건 중 86%) -- 사용자 승인 필요 sudo 요청 다수 대기
- profile_sync 58건 정상 (시간당 약 2.4건)
- token_usage INSERT 파이프라인 복구 필요 (06-21 이후 미기록)
