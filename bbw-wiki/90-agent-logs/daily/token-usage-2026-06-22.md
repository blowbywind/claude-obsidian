# 일일 토큰 사용량 집계 — 2026-06-22

> 집계 시각: 2026-06-21T16:04Z (= 2026-06-22 01:04 KST) | 집계 주체: autobots-scheduler (token-usage-export)

## 개요

Claude Code 팀 요금제 기준 — 실제 토큰 수 대신 API 호출 횟수·이벤트 기반 집계.
(tokens_in/out 미수집: tokens_source=event_log/missing)

---

## 2026-06-21 KST 전일 집계 (UTC 15:00 ~ +24h)

| 항목 | 값 | 비고 |
|------|-----|------|
| chat_success | **45건** | 봇 대화 완료 |
| learning_done | **9건** | 봇 자가학습 완료 (06-20T18~19Z) |
| learning_start | **9건** | 대응 시작 이벤트 |
| tool_use | **259건** | 봇 도구 사용 |
| bot_routed | **15건** | 봇 라우팅 이벤트 |
| cron_start | **523건** | — |
| cron_success | **507건** | 성공률 96.9% |
| cron_error | **16건** | 3.1% (전일 대비 소폭 증가) |
| sudo_pending | **28건** | 사용자 승인 요청 |
| sudo_user_denied | **24건** | 사용자 거부 (86%) |
| sudo_auto | **5건** | 자동 승인 |
| sudo_approved | **2건** | 수동 승인 |
| wiki_modify | **2,537건** | Obsidian 편집 |
| wiki_create | **330건** | 신규 파일 |
| wiki_delete | **53건** | 삭제 |
| runtime_exhausted | **3건** | 런타임 소진 경고 |
| skill_suggested | **5건** | 역량 제안 |

### 자가학습 이벤트 (2026-06-20T18~19Z)

9봇 학습 완료 — 18:15~19:46Z 구간, 봇별 약 2~3분 소요

### sudo 요청 분석 (2026-06-21)

| 타입 | 건수 |
|------|------|
| sudo_pending | 28 |
| sudo_user_denied | 24 (86%) |
| sudo_auto | 5 |
| sudo_approved | 2 |
| sudo_denied | 2 |

---

## 2026-06-22 KST 오늘 (00:00~01:04 KST)

| 항목 | 값 |
|------|-----|
| cron_start | **26건** |
| cron_success | **25건** (96.2%) |
| cron_error | **0건** |
| wiki_modify | **114건** |
| wiki_create | **8건** |
| chat_success | **0건** |
| token_usage 레코드 | **0건** (DB 미삽입 지속) |

---

## 7일 추세

| 날짜 (KST) | chat | learning | cron_ok | cron_err | tool_use |
|------------|------|---------|---------|---------|---------|
| 2026-06-17 | 0 | 0 | 101 | 384 | 0 |
| 2026-06-18 | 0 | 13 | 527 | 83 | 0 |
| 2026-06-19 | 11 | 9 | 593 | 26 | 0 |
| 2026-06-20 | 56 | 0 | 524 | 13 | 0 |
| 2026-06-21 | **45** | **9** | **507** | **16** | **259** |
| 2026-06-22 (부분) | 0 | 0 | 25 | 0 | 0 |

> chat 추세: 0→0→11→56→45 (활성화 유지)
> learning 재개: 06-20 미실시 후 06-21 9건 재개
> cron_err: 384→83→26→13→16 (소폭 증가, 모니터링 필요)

---

## token_usage DB 현황

| date | calls | tokens_in | tokens_out | source |
|------|-------|-----------|------------|--------|
| 2026-06-20 | 3 | 0 | 0 | event_log |
| 2026-06-19 | 20 | 0 | 0 | event_log |
| 2026-06-22 | 0 | — | — | 미삽입 |

> tokens_in/out: NULL (팀 요금제 개별 토큰 계측 미지원)
> 활성 봇: 9/9 | 런타임: claude/codex/agy=healthy, run-gemini=unavailable

---

## 특이사항

- cron_err 16건(3.1%): 전일 13건(2.5%) 대비 소폭 증가 — 원인 파악 필요
- runtime_exhausted 3건: 06-20T16Z 단기 스파이크, 이후 회복
- sudo_user_denied 86%: 저위험 sudo 자동승인 기준 재검토 고려
- wiki 활동 활발: wiki_modify 2,537건 (1시간당 약 106건)
- token_usage INSERT 파이프라인 미복구: 06-21 이후 미기록 지속
- run-gemini: 2026-06-19T14:02 이후 unavailable 지속
