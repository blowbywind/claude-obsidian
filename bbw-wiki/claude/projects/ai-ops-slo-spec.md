---
title: ai-ops SLO 측정 스펙 (Phase 1)
type: spec
status: implemented-baseline-collecting
created: 2026-06-23
updated: 2026-06-23
last_verified: 2026-06-23
review_by: 2026-09-23
project: ai-ops
owner: bbw
adr: decisions/2026-06-21-ai-ops-platform-direction.md
parent: projects/ai-ops-build-plan.md
tags: [ai-ops, slo, measurement, phase-1, spec]
---

# ai-ops SLO 측정 스펙 (Phase 1)

> **목적**: 모든 후속 변경(Phase 2~7)을 SLO에 대고 검증하기 위한 기준선. "측정 없으면 또 감각적 재설계"(codex 교차검증).
> **원칙**: 기존 이벤트에서 파생, **수동 입력 금지**. 대시보드는 나중, 수집부터.
> **상태**: 초안 — 스키마 추가 승인 대기. 실데이터(2026-06-23 라이브 DB) 기준 작성.

## 데이터 기반 (라이브 DB 실측, 2026-06-23)
`backend/db/autobots.db` 5.4MB. 주요 테이블 행수: event_logs 16,449 · bot_chat_outcomes 167(success 163/error 4) · chat_messages 197(user 90/assistant 107) · project_messages 103 · sudo_requests 44 · pipeline_runs 9(success 2/error 4/cancelled 3) · approval_history 5(approved 2/rejected 3) · runtime_providers 5 · security_events 3.

## 4개 SLO 지표 정의

### ② 태스크당 사람 개입 횟수 — ✅ 즉시 측정 가능
- **정의**: 한 태스크(대화/프로젝트) 완료까지 사용자가 보낸 메시지 + 승인/거부 액션 수. 낮을수록 좋음(목표=반복 명령 감소).
- **출처**: `chat_messages WHERE role='user' GROUP BY conversation_id` + `project_messages WHERE role='user' GROUP BY project_id` + `approval_history GROUP BY task_id`.
- **공식**: `(태스크별 user 메시지 수 + 승인액션 수)`의 중앙값/평균. 태스크 = conversation 또는 project_id 또는 pipeline_run.
- **현 스냅샷**: user 90msg / 3 대화 ≈ 30/대화(표본 작음, 노이즈 큼). baseline은 1주 수집 후.
- **수집**: 파생 쿼리만 — **스키마 추가 불필요**.

### ④ degraded 완료율 — ⚠️ 소형 스키마 추가 필요
- **정의**: 벤더/런타임이 degraded·unavailable인 동안에도 완료된 태스크 비율. 높을수록 좋음(fail-safe 입증).
- **출처(완료)**: `pipeline_runs.status='success'` + `bot_chat_outcomes.outcome='success'`.
- **출처(degraded 판정)**: `runtime_providers.status` — 현재 claude/codex/run-gemini=unavailable, agy/obsidian=healthy.
- **갭**: `runtime_providers`는 **현재 상태만** 저장(이력 없음). "완료 시점에 어떤 런타임이 degraded였나"를 알려면 상태 이력이 필요.
- **제안**: `runtime_health_snapshots(runtime_id, status, observed_at)` 신규 테이블 — 기존 헬스체크(last_verified_at 갱신 지점, [[bot-heartbeat]])에서 1행/체크 append. 수동입력 0.
- **공식**: `완료 태스크 중 (그 시간대 1개 이상 런타임 degraded) 비율`.

### ① PR 재작업률 — ⏸ Phase 2 후 유효
- **정의**: merge된 변경이 짧은 기간 내 같은 영역에서 재수정되는 비율. 낮을수록 좋음(완성도).
- **출처**: git log(두 레포). 파일별 재-touch 간격.
- **갭**: ① PR 워크플로 부재(CI=webhook 1개), ② 현재 커밋 대부분 `chore(auto-save)` → 노이즈로 "재작업" 신호 오염. 의미 있는 측정 불가.
- **결론**: **Phase 2(CI/PR 게이트) 도입 후 계측.** 그 전까지 N/A. (auto-save 커밋과 실작업 커밋 분리가 선결.)

### ③ 승인 전 defect 검출율 — ⏸ Phase 2/5 후 유효
- **정의**: 사람 승인 전에 게이트(테스트·교차검증)가 잡은 결함 / 전체 결함. 높을수록 좋음(안전망).
- **출처**: 게이트 실행 결과 — **현재 게이트 자체가 없음**(테스트 1개, 교차검증 미구현).
- **약한 프록시**: `approval_history.action='rejected'`(현 3건)=사람이 승인 단계에서 거른 것(게이트 아닌 사람). `bot_chat_outcomes.outcome='error'`=사후 발생(승인 전 아님).
- **결론**: **Phase 2(테스트 게이트)·Phase 5(교차검증) 도입 후 계측.** 그 전까지 N/A.

## 설계 결론 (승인 필요 사항)
1. **단계적 계측**: 지금 ②(즉시) + ④(소형 스키마 추가)부터, ①③은 Phase 2/5에서 활성화. → Phase 1을 "4개 전부 baseline"이 아니라 "측정 인프라 + 가능한 2개 baseline"으로 조정.
2. **신규 테이블 2개 제안** (DB 스키마 변경 → 승인 대상):
   - `runtime_health_snapshots(id, runtime_id, status, observed_at)` — ④용 런타임 상태 이력.
   - `slo_daily(date, metric, value, sample_n, computed_at)` — 일별 파생값 캐시(파생 쿼리 결과 저장, 대시보드/추세용). 선택사항.
3. **수집 지점**: 신규 이벤트 발생 코드 추가 없이 — ④는 기존 헬스체크 루프에 snapshot insert 1줄, ①②③은 읽기 전용 파생 쿼리(배치/온디맨드).
4. **baseline 기간**: ②④ 1주 수집 후 목표값 설정. ①③은 Phase 2/5 착수 시 정의.

## 미결(사용자 승인 게이트)
- [ ] 위 단계적 계측 방향 동의?
- [ ] 신규 테이블 2개(`runtime_health_snapshots`, `slo_daily`) 추가 승인? (DB 스키마 변경)
- [ ] ④ 수집을 기존 헬스체크 루프에 붙이는 것 vs 별도 cron?

## 관련
[[ai-ops-build-plan]] · [[ai-ops-platform-direction]] · [[bot-heartbeat]] · [[autobots-hardening-backlog]]
