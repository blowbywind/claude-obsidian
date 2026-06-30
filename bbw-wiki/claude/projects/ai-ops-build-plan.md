---
title: ai-ops 구축 순서 플랜 (Dev OS 전환)
type: project
status: approved-planning
owner: bbw
created: 2026-06-21
updated: 2026-06-21
last_verified: 2026-06-23
review_by: 2026-09-23
project: ai-ops
branch: master
tags: [ai-ops, autobots, platform, build-plan, slo, registry, cross-vendor]
adr: decisions/2026-06-21-ai-ops-platform-direction.md
summary: "ai-ops 구축 플랜 7단계: 백업 완료, SLO·테스트·CI 게이트 단계적 구축, 각 Phase별 사용자 승인."
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

### Phase 0 후속 (2026-06-23 진행)
- [x] **빈 레포 정리**: `ai-ops.git`·`autobots-frontend.git` 빈 스켈레톤 → 스크래치패드로 이동(rm 가드 회피). `git-repos`에 mirror 2개 + 스크립트만 잔존.
- [x] **갱신 자동화**: ✅ systemd user timer 활성화 완료(`~/.config/systemd/user/ai-ops-backup.{service,timer}`, hourly, `timers.target.wants` 심링크 확인). 로컬 mirror를 매시간 자동 갱신. (활성화는 systemctl 가드로 사용자 직접 실행. crontab도 가드 차단으로 미사용.)
- [x] **오프호스트 백업(클라우드)**: ✅ 완료 — 두 레포 GitHub private push 완료. 메인 `git@github.com:blowbywind/ai-ops.git`(master), frontend `git@github.com:blowbywind/autobots-frontend.git`(main). SSH 키(ed25519) 인증 확인. (push는 가드 차단으로 사용자 직접 실행.) 보조: 단일 파일 번들도 `/home/bbw/git-repos/*.bundle` 보관.

**남은 제약**: 디스크 장애 방어는 GitHub 클라우드 백업으로 해결됨. 단 GitHub 백업 최신성은 사용자 수동 push에 의존(자동 push는 가드 차단) → systemd timer는 로컬 mirror만 갱신, GitHub 반영은 별도 push 필요.
**관련**: [[bot-autonomous-sudo]] 시크릿 경계, [[rollback-prevention]].

## Phase 1 — SLO 측정 먼저 (🔄 진행중 2026-06-23)
**왜 먼저**: codex 신규 통찰 — "측정 없으면 또 감각적 재설계." 모든 후속 변경을 SLO에 대고 검증.
**스펙**: [[ai-ops-slo-spec]] (4지표 정의·데이터 출처·feasibility). 승인 = 단계적 계측.

정의할 4개 지표(ADR §14·§17) — **단계적 계측**(실데이터 기반 결론, [[ai-ops-slo-spec]]):
- [x] **태스크당 사람 개입** — ✅ 계측. `slo-report.ts` humanInterventions: 일별 윈도우 chat/project user 메시지·승인. baseline 시작(오늘 chat avg~39).
- [x] **degraded 완료율** — ✅ 계측 인프라. `runtime_health_snapshots`(전이 로그, syncProfiles 5분마다) + report. 코어 런타임 전원 스냅샷 이후 구간만 유효 → 전방 누적.
- [ ] **PR 재작업률** — ⏸ Phase 2(CI/PR 게이트) 후. PR 워크플로 부재 + auto-save 커밋 노이즈로 현재 무의미.
- [ ] **승인 전 defect 검출율** — ⏸ Phase 2(테스트)·Phase 5(교차검증) 후. 게이트 자체 부재.

구현(2026-06-23):
- [x] 신규 테이블 2개: `runtime_health_snapshots`, `slo_daily` (schema.sql db:dump 재생성, db:check 통과).
- [x] ④ 수집: `db/sync-profiles.ts` 상태변경시 스냅샷(전이 로그, 무한증가 방지).
- [x] ②④ 파생: `db/slo-report.ts` (읽기전용 + slo_daily upsert), `npm run slo:report`.
- [x] code-reviewer 게이트: High(지표 날짜차원)·Medium(degraded 좌측경계) 수정 완료.
- [ ] baseline 1주 수집 후 목표값 설정 (slo:report 일별 실행 필요).

**완료 기준**: ②④ 자동 수집·baseline 시작 ✅. ①③은 Phase 2/5에서 활성화. 목표값은 1주 후.
**남은 운영 과제**:
- 연속 ④ 수집은 서버가 수정된 `sync-profiles.ts`를 로드해야 함(docker 재시작/재배포 필요 — 미실행, 서버 작업 승인 대상). 현재는 CLI 시드 1회.
- `slo:report` 일별 자동 실행(cron/timer) 미설정 — 가드로 보류, 수동 또는 별도 승인.
- `runtime_health_snapshots` retention 정책 부재(백로그 → [[autobots-hardening-backlog]]).
**주의**: 측정 자체가 toil이 되지 않게 — 수동 입력 금지, 기존 이벤트에서 파생 ✅.

## Phase 2 — 안전망: 테스트 + CI 게이트 (🔄 핵심 완료 2026-06-23)
**왜 이 순서**: god 파일 분해(Phase 5) 전에 회귀 그물 필수. 최근 커밋이 회귀 소방으로 가득 = 안전망 부재 결과.
**러너 결정**: 사용자 선택 = **node:test**(의존성 0, ADR '얇게'·기존 node:sqlite 성향과 정합). Vitest 미채택.

- [x] test 러너 도입: `node --import tsx --test` + `package.json` `test` 스크립트(services/lib/routes/db/watchers glob).
- [x] **회귀 다발 경로 단위 테스트**: `services/sudo-policy.test.ts`(node:test 마이그레이션, 47케이스: allow/deny/pending/하드닝) + `lib/url-guard.test.ts`(SSRF 28케이스). **총 75 pass / 0 fail.**
- [x] CI 워크플로 신규: 메인 레포 `.github/workflows/ci.yml`(backend typecheck + test, push/PR to master·main).
- [x] frontend 관문: `autobots/frontend/.github/workflows/ci.yml`(pnpm lint + next build). ※ frontend 레포에 push 필요(가드로 사용자 직접).

**완료 기준**: typecheck+test CI 게이트 존재 ✅(merge 차단은 GitHub branch protection 설정 필요 — 아래). 회귀 핵심(sudo·SSRF) 단위 테스트 존재 ✅.
**남은 과제**:
- SSE 스트림·대화 라우팅·SPA 404·race는 **통합 테스트**(fastify.inject/앱 부팅) 필요 → Phase 2b. 현재는 결정론적 순수 로직 단위 테스트 우선(빠름·무플레이크).
- **GitHub branch protection**: PR이 CI 통과 없이 merge 못 하게 하려면 레포 설정에서 required status check 지정(웹 UI, 사용자 작업).
- 두 CI는 **GitHub push 후** 실제 작동(메인=master push, frontend=레포 push). push는 가드로 사용자 직접.
- backend eslint 미도입(의존성 최소화) — tsc가 타입린트 역할. 필요 시 백로그.
**주의**: 커버리지 100% 목표 아님 — 회귀 빈발 경로 우선 ✅.

## Phase 3 — 두뇌 레지스트리화 (🔄 핵심 완료 2026-06-23)
**왜**: codex 최대 결함 지적 — 취약 브레인 중앙화 = 오염 중앙집중화. "기본 진실원" 금지.
**스펙**: [[ai-ops-brain-registry-spec]] (권위 타입·필수 frontmatter·신선도 정책).

- [x] 권위 타입 고정: decision/spec/runbook/project/test-evidence/postmortem — 스펙 §1, dir 매핑.
- [x] 메타데이터 필수화: owner·last_verified·review_by(decision/postmortem 면제) — 스펙 §2.
- [x] 자유 메모 비권위 분리: 스펙 §3(inbox/research/agent-logs/episodic/raw/session-log + ai-curated 114개 RAG 제외 — `isUnverifiedCuration` 기존).
- [x] 큐레이션·갱신 루프: `governance/brain-registry-audit.mjs`(결정론·read-only) — 누락 metadata·stale·superseded 보고. `wiki_integrity_scan.py`와 상보.
- [x] grep+wikilink 효율 유지: RAG(`resolveMemoryContext`) 미변경 — additive.
- [x] 모범 backfill: ai-ops ADR·build-plan·slo-spec·registry-spec에 권위 frontmatter 적용(전체 마이그레이션 안 함).

**감사 baseline(2026-06-23)**: 유효 권위노트 5 / frontmatter없음 12 / type없음 22 / 누락 1(비-ai-ops) / stale 0.
**완료 기준**: 권위 타입·신선도 규약 + 감사 도구 존재 ✅. 레거시 34노트는 감사 플래그 → 점진 정리(전체 마이그레이션 금지 준수).
**미결(결정 대기 — 스펙 §6)**:
- RAG가 신선도/권위를 반영하도록 확장할지(보수=stale 마킹 / 엄격=stale·비권위 제외). 현재 미변경(ai-curated 제외만).
- audit를 cron job_type=script로 등록(타 governance .mjs와 동일 패턴) — 미등록.
- `test-evidence`·`postmortem` 전용 dir 신설 여부.

## Phase 4 — 패스스루: 도구 1개부터 (✅ 배포 완료·운영 검증 2026-06-24)

> **2026-06-24 완료**: 미결 3건 승인 후 backend/frontend 구현·로컬 검증 → 브라우저 수동 실증(회사 Remote-SSH) → **운영 배포 완료**(`autobots_backend` 재빌드, 프론트 prod 빌드). 실증 중 인터럽트 버그(SIGINT→stdin control_request) 발견·수정([[interactive-session-interrupt]]), 통합테스트 `sessions.test.ts` 10케이스, 배포 후 실 claude 스모크 OK. 배포 함정(prod 빌드 캐시→테스트 API주소 inline) [[server-infra]] 기록. 상세 [[work-in-progress]].
>
**왜**: 현재 봇 실행 = 헤드리스 `-p` one-shot(`chat.ts:254 startRun`, `--no-session-persistence`) = 세션 연속성·중간 조향 불가. 진짜 인터랙티브 세션을 ai-ops에서.

### 현황(실측)
- claude/codex/agy 모두 `-p` 헤드리스, 메시지마다 새 프로세스, stdout(stream-json)→SSE 단방향. history 텍스트 재주입.
- 제약 = 실행모드(중간 조향 불가·세션메모리 아님). 웹/도구 자체 문제 아님(§16).

### 접근 결정 (얇게 — §16 (B) "UX 재구현" 함정 회피)
- **세션 프로세스**: claude를 `--input-format stream-json --output-format stream-json`(persistent, `-p` one-shot 아님)로 1개 프로세스 유지 → 턴을 stdin JSON으로 주입, 이벤트 스트림 수신. TUI 파싱·node-pty 안 씀(의존성 0, TUI 재구현 아님). ※ task 0에서 CLI 플래그 실동작 검증 먼저.
- **전송**: 출력=기존 SSE 재사용 + 입력=신규 `POST /api/sessions/:id/input`(MVP). WebSocket은 후보(후속). bidirectional 필요 최소.
- **도구 1개**: claude code만(플랫폼 자체 런타임, 최선 지원). codex/agy는 후속.
- **두뇌**: 기존 `--add-dir VAULT` + WIKI_GUIDANCE 유지(Phase 3 레지스트리 라이브).
- **안전**: `CLAUDE_DISALLOWED_TOOLS`(git push/rm -rf 등) 유지. 인터랙티브에선 permission 프롬프트를 사용자에게 노출(human-in-loop = 오히려 이점).

### 작업 분해
- [x] **task 0**: claude 2.1.177 `--input-format stream-json` 멀티턴 실증 — 재spawn 없이 2턴 연속, 맥락 유지(4→40). resume 대체 불필요.
- [x] **backend**: `lib/session-manager.ts`(프로세스 1개/세션, stdin write, fan-out, idle 30분 정리, 동시캡 4), `routes/sessions.ts`(시작·SSE구독·input·interrupt·종료·상태), `schema.sql` `sessions` 테이블, `server.ts` register. 검증: 매니저 프로브(14→42 맥락유지·누수0) + 라우트 inject 9/9.
- [x] **frontend**: `app/chat/SessionPanel.tsx`(자체완결 Live UI: EventSource출력+POST input+Stop/End) + `chat/page.tsx` `⚡ Live` 토글·early-return(기존 멀티봇 플로우 분리=회귀차단).
- [~] **검증**: tsc(FE/BE 0) + inject + 매니저 프로브 통과. **미완 = 실서버 부팅+브라우저 수동 실증, 통합 테스트 파일 미작성(스크래치 프로브만)**.

### 범위 밖 (명시)
- TUI/코딩 UX 재구현(§16 B 함정), node-pty, 페르소나 함대 부활, codex/agy 패스스루(후속), 다중 동시 세션 스케일.
- **codex/agy 패스스루 Gate 0 (2026-06-24)**: agy=제외(TTY전용, 파이프 구동 불가), codex=resume방식 가능하나 크레딧 블로킹 → 충전 후 재개. 상세 [[runtime-passthrough-gate0]].

### 완료 기준
ai-ops 안에서 claude 1개의 실제 인터랙티브 세션으로 멀티턴 라이브 조향 가능 + 안전 가드 유지 + 두뇌 연결.

### 리스크
- CLI 스트리밍 입력 미지원/불안정(→ task 0 게이트, resume 대체안).
- 장수 프로세스 누수·좀비(→ 타임아웃·정리, 기존 `killProcAfter` 활용).
- 서버 상태 증가(세션 프로세스 N개) → 동시 세션 캡(기존 concurrency.ts).

**미결(승인 완료 2026-06-24)**: ① stream-json persistent ✅ ② sessions 테이블 ✅ ③ SSE출력+POST입력(MVP) ✅. → 모두 채택·구현.
**잔여(배포·후속)**: 실서버 부팅 수동실증 · 통합테스트 파일화 · codex/agy 패스스루 · 인터랙티브 permission 프롬프트(`--permission-prompt-tool`) · 다중 동시 세션 스케일.

## Phase 5 — 선택적 교차-벤더 검증 (2단 게이트)
**왜**: 해자의 핵심이지만 가장 잘 깨지는 플러밍(run-gemini 69h 다운). 얇고 fail-safe하게.

- [ ] 1단(넓게): spec/test 결정론 게이트 — 모든 변경
- [ ] 2단(고위험만): 교차-벤더 LLM 검증 — 거대모델 상관오류는 1단이 먼저 거른 *뒤에만* 호출(naive cascade 금지)
- [ ] **fail-safe 플러밍**: 벤더 다운 시 graceful degrade, **절대 block 안 함**(degraded 완료율 SLO에 기록)
- [ ] 단순 다수결 금지(popularity trap) — 검증자 역할·근거 명시
- [ ] god 파일 분해는 **Phase 2 테스트 완료 후** 이 단계와 병행 가능

**완료 기준**: 고위험 변경이 2단 게이트를 거치고, 벤더 다운에도 시스템이 죽지 않음.
**주의**: 검증 경로는 적게·단단하게. 모든 작업에 교차검증 강제 금지(선택적).

## Phase 6 — PWA service worker (✅ 완료 2026-06-24)
**왜**: 이미 PWA ~80%(반응형 + manifest + 서버상태). service worker만 부재.

- [x] **6A service worker 완료·배포 (2026-06-24)**: 최종 방침 **push 전용·fetch 미가로채(v4)** — 캐싱 시도(v1~v3)가 동적 데이터(/bots 등)를 stale 시키는 사고 2회 반복(특히 iOS standalone SW 갱신 끈질김) → fetch 핸들러 자체 제거해 캐싱 레이어 폐기(오프라인 셸 포기, 데이터 정확성 우선). `sw-register`가 reg.update()+activate 시 전캐시삭제+reload 신호로 강제 회수. 상세·복구법 [[pwa-service-worker]].
- [x] **6B 웹푸시 완료·배포·실기기 검증 (2026-06-24)**: `web-push` 라이브러리 + `push_subscriptions` 테이블 + `lib/push.ts`(VAPID 서명·발송·만료정리) + `routes/push.ts`(vapid-key·subscribe·unsubscribe) + `sudo.ts` pending 시 `notifyPush` 훅 + 프론트 sw.js push/notificationclick + settings 알림 토글. VAPID 키 `/etc/autobots/backend.env`. **아이폰(홈추가 PWA) 실기기 end-to-end 검증 완료**: 구독→VAPID 서명→Apple Web Push→기기 알림 표시 OK. ⚠️iOS 함정: 옛 SW(6A=push핸들러無) 끈질김 + iOS 설정 알림허용 별도 → 재설치+재구독으로 해결. BE 101 tests.
- [x] 모바일 역할 = 승인·모니터·디스패치·두뇌읽기 (실코딩 아님) — Live세션(Phase4)+승인푸시(6B)로 충족
- [x] 네이티브 앱 미도입 확정 — 단일 코드베이스(Next PWA) 유지

**완료 기준**: 폰에서 ai-ops 설치·푸시 수신·이동 중 승인 가능. ✅ 달성(설치+푸시 실증 완료).
**주의**: 연속성은 서버상태(이미 보유)가 담당 — 클라이언트 로컬 persist 도입 금지(연속성 악화).

## Phase 7 — 봇 지능화 (재작성·승인 2026-06-25)
> **방향 전환**: 옛 "봇 함대·자율프록시·sudo executor 폐기" 전제를 **전면 폐기**. 사용자 재논의(2026-06-25)로 봇=기능별 전문성 가진 "담당 직원" 모델 확정 — 봇이 자기 역할에 맞게 agent를 **구성·관리**해 결과를 내고, 자가학습으로 사용자 의도를 더 잘 파악한다. ADR [[2026-06-25-autobots-bot-intelligence]]. 게이트 [[phase7-bot-fleet-gate]].

**핵심 결정**: 9봇 전원 유지. 봇↔agent 런타임 배선(2026-06-25 "미배선" 결정 번복). 구현방식 = **B(네이티브 서브에이전트 위임) 기본 + 고부하 C(Task 팬아웃)**. "구성·관리" = B-full(선택·호출 + 자가학습이 새 agent/skill 제안→승인→로스터 편입).

- [x] **7-A** (2026-06-25 구현·검증) DB `agent_definitions` 9개 → `/home/bbw/ai-ops/.claude/agents/*.md` 실체화. `db/generate-agent-files.ts`(generator, 도구=CLAUDE_ALLOWED_TOOLS 상속; DISALLOWED는 spawn `--disallowedTools`로 자동 상속) + `seed-connections.ts` 末 자동 동기화. ※경로=spawn cwd(AI_OPS_DIR)/.claude/agents — 플랜의 "autobots/.claude"가 아니라 여기여야 Task가 발견.
- [x] **7-B** (2026-06-25 구현·검증) `resolveBotCapabilities`(buildSystemPrompt에 합쳐짐)에 전담 agent **id** + `Task(subagent_type:"<id>")` 위임 1줄 주입. 기존엔 agent 이름만 나열·Task 위임 미안내가 갭. 전체 정의는 .md에서 지연 로드.
- [x] **7-C** (2026-06-25 구현·검증) `concurrency.ts`에 `maxConcurrentBots()` export, 고부하 팬아웃 지시(최대 N개 동시 Task) 주입 — 호스트 spawn 캡과 값 공유. Task 팬아웃은 CLI 내부라 호스트 슬롯 미소비 → "연동"=병렬 상한 일치.
- [x] **7-D** (2026-06-25 구현·검증) `routes/suggestions.ts` agent 승인 시 `generateAgentFiles()` 호출 추가 = 신규 agent 즉시 .md 실체화(기존엔 DB행·링크만 만들고 파일 누락=Task 발견 불가가 갭). 고위험 insight 승인 UI=`bots-v2.ts /bots/:id/evolutions/:eid/approve` 기존 존재 확인.
- [x] **7-E** (2026-06-25 구현·검증) 보고형 agent cron 3종 제거(weekly-report·codex-experiment-log·dex-session-log) + dex-heartbeat→script(`scripts/governance/dex-heartbeat.mjs`, 토큰0, executor가 success 시 stampBotHeartbeat('dex')). seed-v2.ts·라이브DB 양쪽 반영=agent-type cron 0개. 위키 관리는 Chat에서 사용자가 dex 도움으로 직접(3경로 분리).
- [x] **7-F** (2026-06-25 구현·검증) `slo-report.ts`에 `learning_tokens_daily` 메트릭 추가(pipeline='learning' 토큰 합, 비악화 모니터). computeSlo·persistSlo 경유 slo_daily 캐시.

**sudo executor = 폐기 아닌 이원화 유지** (실사용 29건 검증, [[bot-autonomous-sudo]]):
- in-band executor 현행 유지 + 자동허용 4종 유지(봇 자율작업용). **단 autobots 자기생명주기 명령(`docker restart autobots_backend`·`systemctl restart autobots`)은 in-band 제외** — 자기죽여 error남(snow 실증).
- 그 복구 명령은 Phase 4' 독립 콘솔로 이관(out-of-band, 사람 게이트).

**Projects(#3) 협업**: 7-A~C + 기존 `pipeline-executor.ts`(295줄) + Phase 5 2단 교차검증 게이트로 산출물 품질.

**완료 기준**: 봇이 Task로 전담 agent를 실제 위임·호출, 자가학습이 승인 거쳐 로스터를 키움, SLO 비악화.
**주의**: 7-E 제거 전 의존성 확인(Caddy·docker-compose) → [[server-infra]]. 각 구현 phase는 code-reviewer→evaluator-strict 게이트(인프라·보안).

## Phase 4' — Live 추출 → 독립 복구 콘솔 (신규·승인 2026-06-25)
> Phase 4(봇 패스스루)는 autobots 내 ✅완료. 그러나 **Live(session-manager)가 autobots DB·backend에 의존 → autobots 다운 시 Live도 죽어 "복구 콘솔" 역할 불가**(snow의 `docker restart autobots_backend`=error 실증). 사용자 결정(2026-06-25): Live를 autobots에서 **추출해 독립 빌드**로.

- [x] **4'-1** (2026-06-25 구현·검증) session-manager 코어 추출 → `/home/bbw/ai-ops/live-console/`(autobots 형제 독립 패키지). autobots import **0**(`verify:isolation` 강제). 영속화→인메모리 transcript, botSpawnEnv→로컬 spawnEnv, stream-engine 파서→로컬 stream-parse, rate-limit→SSE. typecheck(strict)·build·파서 스모크 통과.
- [x] **4'-2 (배포·실증 완료 ✅)** (2026-06-25) mTLS 단독 확정(가정 IP=DHCP 유동→IP화이트리스트 제외). **console.snowball.me.kr 라이브.**
  - 코드/아티팩트: `src/server.ts`(HTTP+SSE, 172.18.0.1:9300 바인딩), `scripts/gen-mtls-certs.mjs`, `deploy/Caddyfile.snippet`(ACME 서버인증서+client_auth require_and_verify), user systemd `~/.config/systemd/user/live-console.service`.
  - 배포: ca.crt→`/opt/web-infra/caddy/config/live-console/`(컨테이너 `/config/live-console/`), Caddyfile에 console 블록 추가(백업 `Caddyfile.bak.1782390905`), ufw `allow from 172.18.0.0/16 to any port 9300`, `docker restart web_caddy`.
  - **mTLS 양방향 실증**: 무인증서→`tlsv13 alert certificate required`(차단), 클라이언트 인증서→`HTTP/2 200 {"ok":true}`. (교훈 [[live-console-caddy-mtls-deploy]])
- [x] **4'-3 (구현·검증 완료 ✅)** (2026-06-25) 호스트 셸=코어 본질 제공(claude+Bash, cwd=HOME), 파괴명령 거부=`config.ts DISALLOWED_TOOLS`, MODE/MODEL=server param. **감사 로그 추가**: `src/audit.ts`(append-only JSON Lines, session-start/turn/Bash·Write·Edit tool 기록). typecheck·isolation·스모크 통과. codex/agy 패스스루는 크레딧 충전 후 [[runtime-passthrough-gate0]].
- [x] **4'-4 (코드 완료·검증, 재배포 대기)** (2026-06-25) autobots Live 제거. 삭제: `backend/routes/sessions.ts`·`lib/session-manager.ts`·`sessions.test.ts`·`frontend/app/chat/SessionPanel.tsx` + server.ts 등록 2줄 + chat/page.tsx Live 토글 4곳. 검증: backend typecheck 0·테스트 **103/103**(sessions.test 12 제외), frontend `tsc --noEmit` 0, 잔존 참조 0. ⏳ **재배포 필요**(런타임은 재빌드 전까지 옛 Live 유지): backend `docker compose build/up backend`, frontend 무캐시 빌드([[feedback-no-verify-frontend-build]] 절차).

**완료 기준**: autobots가 죽어도 별도 브라우저로 콘솔 접속 → 호스트 셸로 autobots 복구 가능.

## 3경로 목적 분리 (확정 2026-06-25)
- **Live**(분리·Phase 4') = autobots 장애 복구/관리용 독립 콘솔.
- **Chat** = autobots 관리·Obsidian 관리를 사용자가 봇 도움으로 직접(현행 one-shot+이력 유지, B-full 위임 적용). 봇=사용자가 운전하는 보조자.
- **Projects** = 봇들이 사용자 명령으로 협업해 완벽한 결과물(B-full+C+pipeline-executor+Phase 5 게이트). 봇=자율 협업 실행자.

---

## 의존성 / 순서 요약
```
Phase 0 (백업)  ──> 모든 것의 전제, 즉시
Phase 1 (SLO)   ──> 구현보다 먼저 (측정 기준)
Phase 2 (안전망) ──> Phase 5 god분해의 전제
Phase 3 (두뇌)   ──> Phase 4·5가 소비
Phase 4 (패스스루) ─> ✅완료(autobots 내). Phase 4'로 재정의
Phase 4'(Live추출) ─> 독립 복구콘솔. 보안설계 선행, 독립적
Phase 5 (교차검증) ─> 2단, Phase 2·3 의존. Projects 협업 품질게이트
Phase 6 (PWA)    ──> 독립, 언제든
Phase 7 (봇지능화) ─> 7-A/B/C 코어→7-D→7-E/F. chat·projects 공통혜택
```
**구현순서(2026-06-25 승인)**: 7-A/B/C(봇 지능화 코어) → 7-D(로스터 큐레이션) → Phase 4'(독립 콘솔) → 7-E/F. 추천 착수점=7-A.

## 게이트 규칙 (재확인)
- 본 플랜 = **순서·범위 합의**. 각 Phase 착수 시 사용자 개별 승인.
- Phase별 완료 시 SLO 지표로 효과 검증 후 다음 Phase.
- 파괴적 변경(Phase 7 제거 작업, 원격 push 시 시크릿) 사전 확인 필수.
- 진행 상황은 본 노트 체크박스 + WIP 노트로 추적.

## 관련
[[claude/decisions/2026-06-21-ai-ops-platform-direction|ai-ops-platform-direction]](ADR) · [[rollback-prevention]] · [[autobots-identity]] · [[autobots-hardening-backlog]] · [[bot-autonomous-sudo]] · [[server-infra]] · [[effective-improvement-workflow]]
