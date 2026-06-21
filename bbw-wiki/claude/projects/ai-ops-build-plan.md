---
title: ai-ops 구축 순서 플랜 (Dev OS 전환)
type: project
status: approved-planning
created: 2026-06-21
updated: 2026-06-21
project: ai-ops
branch: master
tags: [ai-ops, autobots, platform, build-plan, slo, registry, cross-vendor]
adr: decisions/2026-06-21-ai-ops-platform-direction.md
---

# ai-ops 구축 순서 플랜

> **근거**: [ADR §17 (ACCEPTED 2026-06-21)](../decisions/2026-06-21-ai-ops-platform-direction.md). 방향 확정 → 본 문서는 그 구축 순서 플랜.
> **상태**: 플랜 작성 완료. **각 Phase 착수는 사용자 개별 승인 게이트** — 플랜 승인 ≠ 전체 자동 실행.
> **원칙**: 표면 축소 + 코어 심화. 기능 추가 아님. 측정 먼저 → 안전망 → 신뢰성 → 검증.

## 실측 기준선 (2026-06-21, 본 플랜 작성 시점)

| 항목 | 현재 상태 | 리스크 |
|------|-----------|--------|
| 원격 백업 | **메인 레포 + frontend 둘 다 `git remote` 없음** | `rm` 한 번에 ~22k LOC 전체 소멸 |
| 테스트 | backend `sudo-policy.test.ts` 1개, test 러너 없음 | 회귀 무방비 |
| CI 게이트 | `autobots-trigger.yml`(webhook) 1개뿐 | typecheck/lint/test 관문 0 |
| 타입 안전성 | `tsconfig strict: false` (단 현재 `tsc --noEmit` 통과) | null·implicit any 무방비 |
| 관측성 | 구조화 로그 산발, try/catch 193개 제각각 | hermes·run-gemini 장기 DEGRADED 무알림 |
| god 파일 | projects 685 / chat 672 / learning-executor 621 / stream-engine 604 | 테스트 없이 분해 = 회귀 |

---

## Phase 0 — 소멸 리스크 제거 (✅ 완료 2026-06-21)
**왜 먼저**: 다른 모든 작업의 결과물이 백업 없으면 무의미. 가장 싸고 가장 치명적.
**구현 방식**: 사용자 선택 = 홈서버 self-hosted. 현재 머신이 홈서버(`snowball`)임을 실측 확인 → 로컬 `git clone --mirror` 백업(SSH·대역폭·Docker/UFW 리스크 회피). `git push`·`rm -rf`가 가드에 막혀 mirror clone으로 대체(비파괴, 데이터 보호 의도와 정합).

- [x] 시크릿 안전 점검: `.env`·`*.db`·logs·tmp gitignore 처리 확인, 하드코딩 시크릿 0 (tokens.ts=소스)
- [x] frontend dirty 트리 로컬 스냅샷 커밋 (`7343f24`)
- [x] 메인 ai-ops 백업: `/home/bbw/git-repos/ai-ops-mirror.git` (45M, 최신 `94aeb81`)
- [x] frontend 백업: `/home/bbw/git-repos/autobots-frontend-mirror.git` (19M, 최신 `7343f24`)
- [x] 복원 테스트: `/tmp`로 clone → 정상 복원 확인
- [x] 갱신 스크립트: `/home/bbw/git-repos/refresh-backups.sh` (mirror `remote update`, 비파괴)

**완료 기준(Exit)**: ✅ 두 레포 백업 + `rm -rf ai-ops/` 후에도 mirror에서 clone 복원 가능.
**남은 제약(후속 권장)**: 백업이 **동일 디스크(홈서버)** 에 위치 → 실수 `rm`은 방어하나 **디스크 장애는 미방어**. 진짜 오프호스트 백업(타 머신/클라우드 미러)은 별도 단계로 권장. 갱신 자동화(cron 등록)는 settings/hook 변경이므로 별도 승인 후.
**리스크/주의**: 빈 bare 레포 `ai-ops.git`·`autobots-frontend.git` 잔존(무해, rm 가드로 미삭제) — 정리는 사용자 수동 또는 별도 승인. → [[bot-autonomous-sudo]] 시크릿 경계, [[rollback-prevention]].

## Phase 1 — SLO 측정 먼저 (전제, 구현보다 앞)
**왜 먼저**: codex 신규 통찰 — "측정 없으면 또 감각적 재설계." 모든 후속 변경을 SLO에 대고 검증.

정의할 4개 지표(ADR §14·§17):
- [ ] **PR 재작업률** — merge 후 같은 영역 재수정 빈도
- [ ] **태스크당 사람 개입 횟수** — 한 작업 완료까지 사용자 명령/교정 수
- [ ] **승인 전 defect 검출율** — 게이트가 사람 승인 전에 잡은 결함 비율
- [ ] **degraded 완료율** — 벤더/플러밍 다운 상태에서도 완료된 비율

작업:
- [ ] 지표별 데이터 출처 정의(git 로그·세션 로그·게이트 결과·헬스 로그)
- [ ] 최소 수집 메커니즘(SQLite 테이블 또는 구조화 로그 1줄/이벤트) — 대시보드는 나중, **수집부터**
- [ ] 베이스라인 1주 기록 후 목표값 설정

**완료 기준**: 4개 지표가 자동 수집되고 baseline 숫자 확보.
**주의**: 측정 자체가 toil이 되지 않게 — 수동 입력 금지, 기존 이벤트에서 파생.

## Phase 2 — 안전망: 테스트 + CI 게이트
**왜 이 순서**: god 파일 분해(Phase 5) 전에 회귀 그물 필수. 최근 커밋이 회귀 소방으로 가득 = 안전망 부재 결과.

- [ ] test 러너 도입(Vitest) + `package.json` `test` 스크립트
- [ ] **회귀 다발 경로부터** 통합테스트: sudo 승인/거부, SSE 스트림, 대화 라우팅, SPA 404, race(봇 재제출) — 최근 fix 커밋이 가리키는 영역
- [ ] CI 워크플로 신규: `typecheck` + `lint` + `test` 관문 (PR 차단)
- [ ] frontend도 최소 lint/build 관문

**완료 기준**: PR이 typecheck/lint/test 통과 없이 merge 불가. 회귀 다발 경로에 통합테스트 존재.
**주의**: 커버리지 100% 목표 아님 — 회귀 빈발 경로 우선. test-agent 활용.

## Phase 3 — 두뇌 레지스트리화 (검증된 아티팩트)
**왜**: codex 최대 결함 지적 — 취약 브레인 중앙화 = 오염 중앙집중화. "기본 진실원" 금지.

- [ ] 권위 타입 고정: spec / ADR / runbook / test-evidence / postmortem **만** 권위
- [ ] 메타데이터 필수화: 소유자 · 최종검증시각 · 만료조건
- [ ] 자유 메모(session-log 등)는 **비권위 참고용**으로 명시 분리
- [ ] 큐레이션·갱신 루프: staleness 감지(만료 경과), write-only/slop 방지
- [ ] grep+wikilink 효율 유지(웹리서치: markdown+grep ~70x) → [[autobots-identity]] PLAN_WIKI

**완료 기준**: 권위 아티팩트가 타입·신선도로 질의 가능, 전체 덤프 대신 레지스트리 조회.
**주의**: 기존 737노트 vault를 전부 마이그레이션하지 말 것 — 권위 타입만 등록, 나머지는 비권위 그대로.

## Phase 4 — 패스스루: 도구 1개부터 (대화형 진입점)
**왜**: 현재 봇 실행 = 헤드리스 `-p` one-shot(ADR §16) = 중간 조향 불가. 진짜 인터랙티브 세션을 웹에 띄움.

- [ ] **도구 1개만** 패스스루 PoC(claude code 우선 — 가장 잘 동작)
- [ ] 진짜 인터랙티브 세션을 ai-ops UI에 연결(코딩 UX 재구현 금지 — 그건 §16의 (B) 함정)
- [ ] 두뇌 연결(Phase 3 레지스트리) 라이브 주입
- [ ] 사용자 선택: ai-ops 패스스루 OR 도구 직접 (강제 아님)

**완료 기준**: ai-ops 안에서 1개 도구의 실제 인터랙티브 세션으로 라이브 조향 가능.
**주의**: 페르소나 함대 부활 금지. 패스스루는 "실제 도구 그대로", 래퍼 최소.

## Phase 5 — 선택적 교차-벤더 검증 (2단 게이트)
**왜**: 해자의 핵심이지만 가장 잘 깨지는 플러밍(run-gemini 69h 다운). 얇고 fail-safe하게.

- [ ] 1단(넓게): spec/test 결정론 게이트 — 모든 변경
- [ ] 2단(고위험만): 교차-벤더 LLM 검증 — 거대모델 상관오류는 1단이 먼저 거른 *뒤에만* 호출(naive cascade 금지)
- [ ] **fail-safe 플러밍**: 벤더 다운 시 graceful degrade, **절대 block 안 함**(degraded 완료율 SLO에 기록)
- [ ] 단순 다수결 금지(popularity trap) — 검증자 역할·근거 명시
- [ ] god 파일 분해는 **Phase 2 테스트 완료 후** 이 단계와 병행 가능

**완료 기준**: 고위험 변경이 2단 게이트를 거치고, 벤더 다운에도 시스템이 죽지 않음.
**주의**: 검증 경로는 적게·단단하게. 모든 작업에 교차검증 강제 금지(선택적).

## Phase 6 — PWA service worker (인터페이스 보강)
**왜**: 이미 PWA ~80%(반응형 + manifest + 서버상태). service worker만 부재.

- [ ] service worker 추가 → 설치 + 웹푸시 + 오프라인 셸
- [ ] 웹푸시: human-in-loop 승인 게이트(고위험 검증 결과·승인요청)를 폰으로
- [ ] 모바일 역할 = 승인·모니터·디스패치·두뇌읽기 (실코딩 아님)
- [ ] 네이티브 앱 미도입 확정 — 단일 코드베이스 유지

**완료 기준**: 폰에서 ai-ops 설치·푸시 수신·이동 중 승인 가능.
**주의**: 연속성은 서버상태(이미 보유)가 담당 — 클라이언트 로컬 persist 도입 금지(연속성 악화).

## Phase 7 (병행) — 봇 함대·sudo executor 정리
**왜**: 북극성에서 폐기 대상. Phase 4 패스스루가 대화형을 대체하면 자율 프록시 불필요.

- [ ] 9봇 페르소나 함대 → 워크플로 부품·품질게이트 에이전트 + 진짜 무인 루틴만 잔존
- [ ] 자율 dev-프록시 폐기
- [ ] sudo executor 폐기/축소 → 시크릿 경계 단순화 → [[bot-autonomous-sudo]]
- [ ] cron·학습루프 중 SLO에 기여하는 것만 유지

**완료 기준**: 폐기 대상 제거 후 SLO 지표 비악화 확인.
**주의**: 제거 전 의존성 확인(Caddy 라우팅·docker-compose) → [[server-infra]]. 파괴적 변경 사전 확인.

---

## 의존성 / 순서 요약
```
Phase 0 (백업)  ──> 모든 것의 전제, 즉시
Phase 1 (SLO)   ──> 구현보다 먼저 (측정 기준)
Phase 2 (안전망) ──> Phase 5 god분해의 전제
Phase 3 (두뇌)   ──> Phase 4·5가 소비
Phase 4 (패스스루) ─> 1개 도구부터, Phase 7 대화형 대체 근거
Phase 5 (교차검증) ─> 2단, Phase 2·3 의존
Phase 6 (PWA)    ──> 독립, 언제든
Phase 7 (정리)   ──> Phase 4 이후 병행
```

## 게이트 규칙 (재확인)
- 본 플랜 = **순서·범위 합의**. 각 Phase 착수 시 사용자 개별 승인.
- Phase별 완료 시 SLO 지표로 효과 검증 후 다음 Phase.
- 파괴적 변경(Phase 7 제거 작업, 원격 push 시 시크릿) 사전 확인 필수.
- 진행 상황은 본 노트 체크박스 + WIP 노트로 추적.

## 관련
[[ai-ops-platform-direction]](ADR) · [[rollback-prevention]] · [[autobots-identity]] · [[autobots-hardening-backlog]] · [[bot-autonomous-sudo]] · [[server-infra]] · [[effective-improvement-workflow]]
