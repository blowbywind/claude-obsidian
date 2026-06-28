# 일일 토큰 사용량 집계 — 2026-06-23

> 집계 시각: 2026-06-22T16:00Z (= 2026-06-23 01:00 KST) | 집계 주체: autobots-scheduler (token-usage-export)

## 개요

Claude Code 팀 요금제 기준 — 실제 토큰 수 대신 API 호출 횟수·이벤트 기반 집계.
(tokens_in/out 미수집: tokens_source=event_log/missing)

---

## 2026-06-22 KST 전일 집계 (UTC 15:00 ~ +24h)

| 항목 | 값 | 비고 |
|------|-----|------|
| chat_success | **8건** | 봇 대화 완료 |
| learning_done | **9건** | 봇 자가학습 완료 (06-21T18~19Z) |
| learning_start | **9건** | 대응 시작 이벤트 |
| tool_use | **6건** | 봇 도구 사용 |
| bot_routed | **9건** | 봇 라우팅 이벤트 |
| cron_start | **523건** | — |
| cron_success | **226건** | 성공률 43.2% (전일 대비 급감) |
| cron_error | **297건** | 56.8% (에러 발생 빈도 대폭 증가) |
| sudo_pending | **0건** | 사용자 승인 요청 |
| sudo_user_denied | **0건** | 사용자 거부 |
| sudo_auto | **0건** | 자동 승인 |
| sudo_approved | **0건** | 수동 승인 |
| wiki_modify | **1,568건** | Obsidian 편집 |
| wiki_create | **223건** | 신규 파일 |
| wiki_delete | **45건** | 삭제 |
| runtime_exhausted | **2건** | 런타임 소진 경고 |

### 자가학습 이벤트 (2026-06-21T18~19Z)

9봇 학습 완료 — 18:16~19:47Z 구간, 봇별 약 2~3분 소요
(해리, 덱스, 리나, 로운, 리안, 스텔리나, 키엘, 아서, 눈꽃 자가학습 완료)

### sudo 요청 분석 (2026-06-22)

| 타입 | 건수 |
|------|------|
| sudo_pending | 0 |
| sudo_user_denied | 0 |
| sudo_auto | 0 |
| sudo_approved | 0 |
| sudo_denied | 0 |

---

## 2026-06-23 KST 오늘 (00:00~01:00 KST)

| 항목 | 값 |
|------|-----|
| cron_start | **22건** |
| cron_success | **0건** (0.0%) |
| cron_error | **22건** |
| wiki_modify | **24건** |
| wiki_create | **0건** |
| chat_success | **0건** |
| token_usage 레코드 | **0건** (DB 미삽입 지속) |

---

## 7일 추세

| 날짜 (KST) | chat | learning | cron_ok | cron_err | tool_use |
|------------|------|---------|---------|---------|---------|
| 2026-06-18 | 0 | 0 | 360 | 247 | 0 |
| 2026-06-19 | 3 | 14 | 577 | 1 | 0 |
| 2026-06-20 | 45 | 14 | 559 | 0 | 7 |
| 2026-06-21 | 45 | 9 | 507 | 0 | 259 |
| 2026-06-22 | **8** | **9** | **226** | **295** | **6** |
| 2026-06-23 (부분) | 0 | 0 | 0 | 22 | 0 |

> chat 추세: 0→3→45→45→8 (소폭 감소)
> learning 재개: 9건 완료
> cron_err: 247→1→0→0→295 (급격한 증가, 디버깅 필요)

---

## token_usage DB 현황

| date | calls | tokens_in | tokens_out | source |
|------|-------|-----------|------------|--------|
| 2026-06-20 | 3 | 0 | 0 | event_log |
| 2026-06-19 | 20 | 0 | 0 | event_log |
| 2026-06-22 | 0 | — | — | 미삽입 |

> tokens_in/out: NULL (팀 요금제 개별 토큰 계측 미지원)
> 활성 봇: 2/2 (리나, 리안) | 런타임: claude/codex/agy=healthy, run-gemini=unavailable

---

## 특이사항

- cron_err 295건(56.8%): 전일 0건 대비 대폭 증가하여 대부분의 크론 작업이 실패함 — 즉각적인 원인 조사 요망
- wiki 활동: wiki_modify 1,568건으로 안정적인 활동량 기록
- token_usage INSERT 파이프라인 미복구 지속
