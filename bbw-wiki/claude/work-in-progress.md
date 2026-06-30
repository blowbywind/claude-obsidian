---
updated: 2026-06-30 (hnedu_erp 연차·휴가 프론트 오류 UX 및 생일휴가 신청 UX 보강 완료, 웹 클라이언트 프론트엔드 미완성 항목 잔여)
project: hnedu_erp
branch: feat/web-client-auth
---

# [활성] hnedu_erp — 백엔드 P0~P9 완료·운영 배포 완료 / 웹 클라이언트 프론트엔드 미완성

> updated 2026-06-30 KST · 최신 커밋 `c384458` · 연차·휴가 잔여/API 연결, YYYY-04 기간 키, 생일휴가 당일 검증 및 프론트 오류 UX 보강 완료, 웹 클라이언트 프론트엔드 3개 항목 미완성

## 완료
- [x] KST 기준선 커밋 `9670804`와 문서 현행화 커밋 `0ef8261` 이후 운영 서버 `/home/hnedu/hnedu_erp`에 `server/`, `web-client/` 재동기화.
- [x] 사전 백업 생성: `/home/hnedu/hnedu_erp_pre_sync_kst_baseline_20260629T225213+0900.tgz`.
- [x] `docker compose --profile apps config --quiet` 통과 후 `erp_api`, `erp_web` 재빌드/재기동.
- [x] 운영 검증: PostgreSQL `Asia/Seoul`, API health 200 및 `timestamp +09:00`, 웹 `/`·`/login` 200, protected API 15개 미인증 요청 401.
- [x] 세콤 인입 검증: `T_SECOM_ALARM` 51,610건, `gate_attendance_logs` SECOM 38,199건, 최신 `tag_time=2026-06-29 21:17:50+09`, 워터마크 `20260629211750`.
- [x] 22:55 KST 세콤 잡 확인: 신규 원천 없음으로 `Pulled=0, Inserted=0`.
- [x] 문서 커밋 `155e937 docs(secom): record production attendance import verification`; 운영 서버 `docs/` 동기화 완료.

## 검증
- [x] 로컬 `dotnet build server/HneduErp.sln --configuration Release` 통과.
- [x] 로컬 `dotnet test server/HneduErp.Tests/HneduErp.Tests.csproj --configuration Release --no-build` 통과: 359/359.
- [x] 로컬 `dotnet format server/HneduErp.sln --verify-no-changes --no-restore` 통과.
- [x] 로컬 web-client `pnpm exec tsc --noEmit`, `pnpm lint`, `pnpm build` 통과.
- [x] `git diff --check` 통과, 프로젝트 git 상태 깨끗함.
- [ ] 원격 서버에는 현재 `dotnet` 명령이 PATH에 없어 원격 테스트 미실행.

## 남은 일 (개발 불가 — 외부 대기)
- [ ] 미매핑 직원 2명(정덕균·조성진) HR 카드 등록값·휴대폰 번호 확인 → HR팀
- [ ] WORKHISTORY OWTime 2026년 미집계 원인 → 세콤 벤더 문의
- [ ] 역할별 쓰기 플로우 스모크 → 직원 파일럿 시 실계정으로 수행
- [ ] MFA TOTP 등록 5명 → 다음 로그인 시 자동 강제
- [ ] 직책(position) HR 보정 → HR팀 ERP 직접 수정

## 추가 완료 (위 기록 이후)
- [x] Flag1 매핑 검증 `c384458`: '1'→IN, '4'→OUT, 나머지→SkippedNonPunch
- [x] WORKHISTORY OWTime 분석: 2026년 0건(세콤링크 스케줄 미갱신, 개발 이슈 아님)
- [x] 웹 화면 회귀 확인: / → 200, /login → 200 (나머지는 SPA 구조상 의도적 404)
- [x] 단일 페이지 앱 구조 확인: 모든 기능이 (app)/page.tsx 탭으로 구현됨
- [x] API 스모크 19/19 통과 (미인증 게이트 전부 401, health 200, Swagger 404=Production 정상)
- [x] 연차·휴가 잔여/API 연결 보강(2026-06-30): `db/migrations/026_leave_special_balance_and_reject_reason.sql` 추가, `leave_balances` 특수 잔여 필드와 `leave_requests.reject_reason` 반영, 승인 시 `used_days`·`holiday_comp_count`·`total_leave_days`·`sabbatical_days` 갱신, 웹 클라이언트 생일휴가·휴일근무 대체·안식휴가 잔여 표시 연결.
- [x] 검증: `dotnet build --configuration Release`, `dotnet test --configuration Release --no-build`(단위 376/376, 통합 15 skip), `dotnet format --verify-no-changes`, web-client `pnpm lint`, `pnpm exec tsc --noEmit` 통과.
- [x] 연차·휴가 내규 검증 보강(2026-06-30, 로컬 미배포): 신청 시 잔여 연차 부족, 휴일근무 대체 5회 초과, 연차+특별+대체 30일 상한, 안식휴가 잔여 부족, 생일휴가 중복/미보유를 백엔드에서 400 차단. `LeaveRequestDto.reviewerName` 추가, 결재 상세·이력 반려 사유/검토자 표시, 웹 클라이언트 사전 경고 계산을 내규와 일치시킴.
- [x] 검증: `dotnet build --configuration Release`, `dotnet test --configuration Release --no-build`(단위 380/380, 통합 15 skip), `dotnet format --verify-no-changes`, web-client `pnpm lint`, `pnpm exec tsc --noEmit`, `git diff --check` 통과.
- [x] 연차 기간 키 정합성 보강(2026-06-30, 로컬 미배포): `CompanyTime.LeaveYearFor*`를 4월 1일~익년 3월 31일(`YYYY-04`) 기준으로 통일하고, `LeaveService`·`LeaveAccrualService`·`TenureMilestoneService`·web-client 잔여 조회 키를 같은 규약으로 전환. 신규 마이그레이션 026에 기존 `YYYY-01` 행을 `YYYY-04`로 안전 정규화하는 구문 추가.
- [x] 생일휴가 당일 검증 보강(2026-06-30, 로컬 미배포): 서버에서 직원 생년월일을 복호화해 신청일 월일과 대조하고, 2월 29일 생일은 비윤년 2월 28일로 허용. 반차·생일휴가 다일 범위 신청 차단. web-client는 `YYYY-04` 기간 표시와 사전 검증 시 신청 버튼 비활성화 반영.
- [x] 검증: `DOTNET_CLI_HOME=/tmp/hnedu-dotnet dotnet build --configuration Release`, `dotnet test --configuration Release --no-build`(단위 386/386, 통합 15 skip), `dotnet format --verify-no-changes`, web-client `pnpm lint`, `pnpm exec tsc --noEmit`, `pnpm build`, `git diff --check` 통과.
- [x] 연차·휴가 프론트 오류 UX 보강(2026-06-30, 로컬 미배포): `CODE: 메시지` 형태의 백엔드 검증 오류를 공통 API 클라이언트에서 사용자 문구만 표시하도록 정규화. 생일휴가는 신청 일수를 `0.5일 (오후 반차)`로 표시하고, 생일휴가 선택 시 오후 반차 상태를 고정하며 등록 생일 동일 날짜 안내를 차단 메시지와 분리.
- [x] 검증: web-client `pnpm lint`, `pnpm exec tsc --noEmit`, `pnpm build`, `git diff --check` 통과.

**백엔드 P0~P9 전기능 + 운영 배포 완료.**

## 남은 작업 (웹 클라이언트 프론트엔드)

- [ ] **지출 신청 모달** — 폼 state 없음, API mutation 없음, 날짜 하드코딩
- [ ] **회의 소집 모달** — 참석자 하드코딩, API mutation 없음, 날짜 하드코딩
- [ ] **업무보고 작성 UI** — mutation 없음 (조회만 가능, 작성 미구현)

---

# [완료 스레드] ai-ops — Usage Antigravity 토큰 표시 운영 반영

> updated 2026-06-28 10:02 UTC · 코드·검증·운영 반영 확인 완료

## 완료
- [x] `autobots/backend/lib/runtime-auth.ts`: Antigravity 인증 판정을 `~/.gemini/antigravity-cli/antigravity-oauth-token` 우선, `~/.gemini/oauth_creds.json` fallback으로 변경. 토큰 원문은 노출하지 않고 `tokenSource`, `tokenUpdatedAt`, `tokenExpiresAt`, `tokenStatus`만 반환.
- [x] 재발 방지 보강: access token 만료와 refresh token 존재를 분리해 `tokenStatus='refreshable'` 지원. Usage 화면에는 "갱신 가능"으로 표시.
- [x] `autobots/backend/lib/runtime-auth.test.ts`: 라이브 토큰, 레거시 fallback, access 만료+refresh token 회귀 테스트 추가.
- [x] `autobots/frontend/app/usage/page.tsx`: Antigravity 카드에서 계정, 인증 방식, 토큰 출처, 상태, 만료, 갱신, 검증 시각 표시.
- [x] DB/API Usage 상태 동기화 확인: `/api/usage`의 `antigravity.status='available'`, `updated_at='2026-06-28 09:03:23'`.
- [x] 실제 `agy -p "Reply exactly: AGY_TOKEN_REFRESH_OK"` 성공. 최신 코드 기준 토큰 메타데이터: 계정 `blowbywind@gmail.com`, 출처 `antigravity-cli`, 만료 `2026-06-28T10:30:01.879Z`, 갱신 `2026-06-28T09:30:02.878Z`, 상태 `valid`.
- [x] 운영 `/api/usage/auth`가 `tokenSource`, `tokenUpdatedAt`, `tokenExpiresAt`, `tokenStatus`를 반환하는 것 확인.
- [x] 정적 프론트 산출물 `autobots/frontend/out/_next/static/chunks/app/usage/*.js`에 Antigravity 토큰 표시 UI 반영 확인.

## 검증
- [x] backend `npm run typecheck` 통과.
- [x] backend `npm test -- lib/runtime-auth.test.ts` 통과: 185/185.
- [x] frontend `npm run lint` 통과: 기존 경고 20개, 오류 0개.
- [x] frontend `npm run build` 통과: `Compiled successfully`, `[verify-build] OK`.
- [x] `git diff --check` 통과.
- [x] 2026-06-28 10:02 UTC 재검증: backend `npm run typecheck` 통과, backend `npm test -- lib/runtime-auth.test.ts` 185/185 통과, `agy -p "Reply exactly: AGY_DONE_CHECK"` 성공.

## 운영 반영 확인
- [x] `wget -qO- http://127.0.0.1:9200/api/usage/auth` 기준 Antigravity 응답: `tokenSource='antigravity-cli'`, `tokenStatus='valid'`, `tokenUpdatedAt='2026-06-28T09:30:02.878Z'`, `tokenExpiresAt='2026-06-28T10:30:01.879Z'`.
- [x] `wget -qO- http://127.0.0.1:9200/api/usage` 기준 Antigravity 상태: `available`, `updated_at='2026-06-28 09:03:23'`.

# [활성 스레드] ai-ops — 안정화 R1/R2/R2.5 코드 보강 + R3 부분 정리

> updated 2026-06-26 · 기준 결정 [[2026-06-25-ai-ops-stabilization]] · 코드 보강 및 잔재 삭제 완료 · 키 이전과 systemd 설치는 권한 게이트 대기

## 완료
- [x] `autobots/scripts/governance/db-backup.mjs`에 `DB_BACKUP_REMOTE` 분기 추가. 미설정은 기존 로컬 동작 유지, 로컬 디렉터리 복사 지원, `rsync`/`scp` 원격 대상 지원, 원격 실패는 `cron_script_warning`만 남기고 로컬 백업 성공을 깨지 않음.
- [x] `autobots/backend/db/client.ts` `withTransaction`이 Promise-like 반환을 거부해 async 콜백 조기 commit을 방지. 동기 예외와 async 오용 모두 rollback.
- [x] 회귀 테스트 추가: `db/client.test.ts`, `db/db-backup.test.ts`. 검증: backend `npm run typecheck`, `npm test` 126/126 pass.
- [x] 루트 CI에 `live-console` typecheck + isolation + build job 추가. 검증: `live-console` `npm run typecheck`, `npm run verify:isolation`, `npm run build` pass.
- [x] 루트 README의 frontend 원격 백업 오정보 정정. `autobots/frontend/.git/config` 기준 `origin` 존재 확인.
- [x] R2.5 위생 보강: `db-backup.mjs` 원격 복사 `rsync`/`scp` 인자에 `--` 구분자 추가, `push.test.ts`에서 VAPID env를 import 전 임시 제거 후 복원해 환경 오염과 무관하게 결정론화.
- [x] R2.5 검증: backend `npm run typecheck` pass, `npm test` 128/128 pass, `VAPID_SUBJECT=mailto:x@y.z VAPID_PRIVATE_KEY=k VAPID_PUBLIC_KEY=k npm test` 128/128 pass, `scp --` 로컬 복사 호환 확인. 현재 `rsync`는 PATH에 없음.
- [x] R3 일부: 0바이트 DB 잔재 3개 삭제 완료. 대상: `/home/bbw/ai-ops/autobots.db`, `/home/bbw/ai-ops/autobots/autobots.db`, `/home/bbw/ai-ops/autobots/backend/db/backups/autobots_20260618_040105.db-wal`.
- [x] R3 검증: 0바이트 DB/WAL/SHM 잔재 재검색 결과 없음. backend `npm run typecheck` pass, backend `npm test` 135/135 pass, live-console `npm run typecheck` pass, `npm run verify:isolation` pass, `npm run build` pass.

## 남은 게이트
- [ ] `live-console/certs/*.key`, `client.p12` 워킹트리 밖 이전 및 배포 경로 정리. 현재 `ca.key`, `server.key`, `client.key`, `client.p12`가 워킹트리에 남아 있음. `/etc/live-console/certs` 대상 이전은 `botsudo install`이 승인 대기로 전환되어 미완료.
- [ ] live-console systemd 설치/재시작 실측. `botsudo systemctl status live-console --no-pager` 결과 `Unit live-console.service could not be found.`. `/etc/systemd/system` 설치·enable은 권한 게이트 필요.

# [활성 스레드] ai-ops — 봇 지능화 (Phase 7 재작성 + Phase 4' Live 추출)

> updated 2026-06-25 · **플랜 승인 완료, 구현 미착수** · 집에서 이어감 · 영구계획 [[ai-ops-build-plan]] Phase 7·4' · 결정 [[2026-06-25-autobots-bot-intelligence]] · 게이트 [[phase7-bot-fleet-gate]]

## 작업 요약
옛 Phase 7("봇 함대·자율프록시·sudo executor 폐기")을 사용자 재논의로 **전면 재작성** → **봇 지능화**. 봇=기능별 전문성 "담당 직원" 모델, 봇이 자기 agent를 구성·관리, 자가학습으로 의도 파악. ADR 6결정 기록 완료.

## 완료 (논의·기록)
- [x] 4항목 재논의 완료(봇함대/자율프록시/sudo/cron학습), ADR급 6결정 확정.
- [x] 빌드플랜 [[ai-ops-build-plan]] Phase 7 재작성 + Phase 4' 신규 + 3경로 분리 + 의존성/순서 갱신.
- [x] ADR [[2026-06-25-autobots-bot-intelligence]] 작성. 게이트 메모리 [[phase7-bot-fleet-gate]]에 논의 전과정 기록.

## ✅ Phase 7 전체 완료 (2026-06-25 구현·검증 — typecheck 0, 테스트 115/115, 단계마다 검증)
- [x] **7-A** `db/generate-agent-files.ts` → `/home/bbw/ai-ops/.claude/agents/*.md` 9개 실체화(도구=CLAUDE_ALLOWED_TOOLS 상속). `seed-connections.ts` 末 자동 동기화. ※경로=spawn cwd(AI_OPS_DIR) 기준, autobots/ 아님.
- [x] **7-B** `resolveBotCapabilities`에 전담 agent **id**+`Task(subagent_type:"<id>")` 위임 1줄 주입.
- [x] **7-C** `concurrency.ts maxConcurrentBots()` export + 고부하 팬아웃 지시(최대 N=캡 동시 Task) 주입.
- [x] **7-D** `routes/suggestions.ts` agent 승인 시 `generateAgentFiles()` 호출=신규 agent 즉시 실체화. 고위험 승인 UI=bots-v2.ts evolutions 기존 확인.
- [x] **7-E** 보고형 cron 3종 제거(weekly-report·codex-experiment-log·dex-session-log)+dex-heartbeat→script(`scripts/governance/dex-heartbeat.mjs`). agent-type cron 0개. seed-v2·라이브DB 양쪽 반영.
- [x] **7-F** `slo-report.ts learning_tokens_daily` 메트릭 추가(비악화 모니터).

## Phase 4' — 4'-1~4'-3 완료, 4'-4만 남음 (인증=mTLS 단독, console.snowball.me.kr 라이브)
- [x] **4'-1** (2026-06-25) `/home/bbw/ai-ops/live-console/` 독립 패키지. autobots import 0. typecheck(strict)·build·파서 스모크 통과.
- [x] **4'-2 배포·실증 완료** (2026-06-25) `console.snowball.me.kr` 라이브. ACME 서버인증서+mTLS client_auth. ca.crt→`/opt/web-infra/caddy/config/live-console/`, Caddyfile console 블록(백업 .bak.1782390905), ufw `allow from 172.18.0.0/16 to port 9300`, `docker restart web_caddy`. **mTLS 실증**: 무인증서 차단(`certificate required`)·인증서로 `200 {"ok":true}`. 함정·해결 [[live-console-caddy-mtls-deploy]].
- [x] **4'-3 완료** (2026-06-25) 호스트 셸=코어 본질, 파괴거부=config DISALLOWED, MODE/MODEL=server param. **감사 로그** `src/audit.ts`(JSON Lines, turn·Bash 등 기록) 추가·검증.
- [ ] **4'-4 (남음·선택)** autobots Live 제거: 백 `backend/routes/sessions.ts`+`lib/session-manager.ts`(+server.ts:29,89) + 프론트 `app/chat/SessionPanel.tsx`(+chat/page.tsx). ⚠️백+프론트 동시 제거(부분=패널 404), 프론트 재빌드 [[feedback-no-verify-frontend-build]] 캐시함정 주의. 콘솔 동작 무영향=위생작업.
- 잔여(사람): client.p12 접속 PC 설치 / `sudo loginctl enable-linger bbw`(boot 기동) / `systemctl --user restart live-console`(새 dist 반영).
- 검증 명령: `cd live-console && npm run verify:isolation && npx tsc --noEmit && node scripts/smoke-server.mjs`.
- 인계: 추출 코어는 autobots `lib/session-manager.ts`와 동일 로직(검증된 인터럽트=control_request, SIGINT 금지 주석 보존). live-console는 `strict:true`(autobots backend는 strict:false).

## 인계 노트 (집에서 필독)
- **게이트 준수**: Phase 7/4'는 [[phase7-bot-fleet-gate]] 절차(재논의→플랜수정→승인) 통과함. 이제 구현 착수 OK이나 각 phase 착수 시 사용자 확인 권장(파괴적·인프라).
- **기검증 사실**: `Task` 이미 CLAUDE_ALLOWED_TOOLS(stream-engine.ts:380). sudo 실사용 29건(executor 유지). snow의 `docker restart autobots_backend`=error(=Phase4' 분리 근거). 학습 9봇 매일 가동·capability_suggestions 큐가 7-D 제안경로 이미 존재.
- **sudo executor 유지**: 폐기 아님. 자기생명주기 명령만 in-band 제외→Phase4' 콘솔로.
- 환경: 이 Claude는 snowball(집서버) 실행. 집/회사 어디서든 Remote-SSH로 동일 워크스페이스. 레포=`/home/bbw/ai-ops`. 커밋=`git -C /home/bbw/ai-ops`.

---

# [완료 스레드] hnedu_erp — 세콤 근태 휴대폰 매핑 배포 (.220) ✅

> updated 2026-06-25 · 배포·실증 완료 · 잔여=snowball 미커밋 코드 커밋 + 백로그 자동 소진(~55분)

## ✅ .220 배포 완료 (2026-06-25, snowball→ssh hnedu-erp)
- [x] 실제 배포루트 = **/home/hnedu/hnedu_erp** (/opt는 스테일 — 런북 경로 정정됨)
- [x] 신코드 tar전송(백업 server.bak_deploy_*) → 마이그024 적용 → erp_api 재빌드
- [x] 동기화로 **phone_hash 30/31** 채움(auth listEmployees가 phone 제공, 1명 폰없음) — cron 임시override 1회 후 원복
- [x] 워터마크 리셋 → **gate_attendance_logs Inserted=885**(첫 5000배치). 백로그 51455펀치 5000/5분 자동 소진
- [x] **잠복버그 수정**: `OccurredAt.ToUniversalTime()` (KST→UTC, timestamptz Npgsql 제약). InMemory테스트 미검출, 실PG에서 표면화

## 잔여
- [x] **미커밋 코드 커밋 완료 (2026-06-25, main)**: 3커밋 — `c9916cd` feat(세콤 폰매핑+UTC+erp_role enum 강타입화; enum/phone이 Employee.cs 등서 얽혀 본체 1커밋) · `61161c2` test(LeaveWorkflowTests+PLAN 라우트) · `27c4601` chore(Caddyfile reverse_proxy). 빌드+310테스트+포맷 통과. git add -p 미지원이라 파일단위 추가분리 불가.
- [x] **정규화 42명 전수 대조 완료 (2026-06-25, .220 실데이터, 커밋 `0d08096`)**: ★규칙 버그 적발·정정★ — CardNo 디코드가 등록코드 위치를 1자리 오인(앞7+뒤4, 8~9번 제거)했고 검증 쌍 `0109548281358`이 `card[6]==card[8]`로 우연히 두 규칙 동일 → 버그 은폐. 실데이터: 구규칙 **5/30 매칭뿐**(나머지 25명 근태 무음 누락), 정정(앞6+뒤5, 7~8번 제거) **27/30**. 인코딩 = `폰앞6+등록코드2+폰뒤5`. 잔여 3명(송영석·정덕균·조성진)=카드미등록/폰오타, SECOM 15장=비직원. 데이터: auth API(서비스토큰)로 평문폰 31명 + SECOM MS-SQL T_SECOM_PERSON 47장, 삭제위치 교집합 역산으로 규칙 도출.
- [x] **.220 재배포 완료 (2026-06-25)**: 정정코드 전송(배포루트=/home/hnedu/hnedu_erp, 백업 server.bak_fix_20260625_091359.tgz) → erp_api 재빌드·기동(healthy) → 워터마크 리셋 → 재폴링. **운영 검증: 매핑 직원 4→24명**(배치 Pulled=5000/Inserted=4237/SkippedUnmapped=731, 구버그 시 대부분 skip). 백로그(~51k펀치) 5000/5분 자동 재처리 중, distinct ~27 수렴 예정. 마이그024는 기재적용·phone_hash 30/30 불변(수정은 CardNo 디코드만).
- [ ] 후속: 미매핑 2명(정덕균·조성진) 추후 HR 카드등록/폰 확인. **송영석=카드 미등록 정상(매핑 불필요, 2026-06-25 종결)**. 외출/복귀(`Flag1 2/3`)·`T_SECOM_WORKHISTORY` 연장/야간 대조. 970 물리카드 5명 폴백.

---

# [활성 스레드] hnedu_erp — auth↔ERP 식별자 정합(Option A) 운영 배포

> updated 2026-06-24 · project hnedu_erp(+hnedu_auth) · branch main · 핸드오프: snowball → Remote-SSH(.221 auth/.220 ERP)

## 작업 요약
auth/ERP 크로스시스템 ID를 UUID로 통일(Option A, additive). auth Int PK 유지하고 `employeeUuid`(JWT 클레임)·department `uuid` 추가. ERP는 동기화 시 부서→직원 순서로 auth pull, auth의 느슨한 필드(jobTitle/status/systemRoles)에서 ERP enum 도출.

## 완료 (2026-06-24 운영 배포 실행됨, snowball→ssh)
- [x] ERP 코드 커밋 (snowball `main` `1a0b6da`) + 빌드/테스트(287)/포맷 통과
- [x] **ERP(.220) 배포**: `/home/hnedu/hnedu_erp/server` tar 전송(해시 일치) → `docker compose --profile apps build/up erp_api` 기동 OK. 백업 server.bak_20260624_092339. compose 실체=`/home/hnedu/hnedu_erp/infra`(≠/opt/hnedu-erp)
- [x] **auth(.221) 전체 최신화(MFA 포함)**: DB덤프+소스백업(*_20260624_094517) → `feat/mfa-totp` src·prisma·public·package·lock 전송 + admin-ui `next build`(public/admin=MFA UI) → host `corepack pnpm@11.5.1 install`(otplib·qrcode) → 컨테이너 `prisma generate`+`migrate deploy`(add_mfa·sabun·uuid) → `docker restart hnedu_auth`. :3100 정상
- [x] **검증**: employees(uuid·sabun·mfa_enabled)+departments(uuid) 컬럼+unique idx, **31명·12부서 전원 uuid 채워짐**, mfa_secrets·mfa_recovery_codes 생성, 새 코드 가동(200)
- auth 런타임: `/var/web-infra/hnedu_auth`→`/app` bind(node:22+tsx), 로그인UI=Fastify `public/admin` 정적서빙. DB=db_postgres(unix소켓 trust). 컨테이너 pnpm없음→host/corepack

## 동기화 서비스토큰 + 실증 (2026-06-24 완료)
- [x] **auth 서비스토큰 신설**(커밋 `3a85665` feat/mfa-totp): service_tokens 테이블·svc_ 불투명토큰·requireServiceOrAdmin(svc_=GET+IP화이트리스트, 그외 requireAdmin)·관리 API·issue-service-token.mjs. code-reviewer 통과(High2 반영). .221 배포·가드 검증(200/403/401).
- [x] **ERP 배선**: 서비스토큰 발급→.220 .env `AuthIntegration__BaseUrl=https://auth.snowball.me.kr`(도메인 변경예정)·`__ServiceToken`·`PII_ENCRYPTION_KEY`(생성·백업필수).
- [x] **기존 ERP 버그 수정**(커밋 `0f4c14d`): PG enum→text(021·022: audit.action, employees.rank/position/erp_role/education_level/gender) + AuditLogService가 Guid.Empty(시스템액터) audit 생략. 빌드+287테스트 통과.
- [x] **★ 동기화 1회 실증 완료**: EmployeeSyncJob Created=31·부서12·직원31 전원 active·FK 31/31·erp_role/rank 도출 정상. cron 02:00 자동 복원.

## 전역 enum→text 수정 (2026-06-24, 동기화 실증 중 발견·.220 배포완료)
- [x] **앱 전역 enum 매핑 버그**: PG enum 27컬럼이 Npgsql 미등록으로 EF 쓰기 시 42804 → 거의 모든 쓰기기능 영향(잠복). `db/023_all_enums_to_text.sql`(제네릭 전환+부분인덱스 재생성) + AppDbContext HasColumnType 27 제거 + **`ConfigureConventions Properties<Enum>().HaveConversion<string>()`**(enum 이름 저장). 커밋 a4210eb+84e6989.
- [x] **code-review Critical 적발·수정**: HasConversion<string>까지 제거 시 enum이 ordinal 저장되는 회귀 → 전역 컨벤션으로 해결. 리뷰 통과.
- [x] **.220 배포**: enum 테이블 0행 실측(오염無) → 023 적용(잔여 enum 0) → erp_api 재빌드·기동. 데이터 유지(부서12·직원31·erp_role 3종 정상).
- [x] 통합테스트 1→8 통과(타임존 UTC + TestAuthHandler employeeUuid + enum 수정).

## 쓰기경로 버그 3종 수정 (2026-06-24, 통합테스트로 발견·커밋 228111a·.220 배포완료)
- [x] **DTO 검증 [property:]→파라미터 타깃**(11개 record): .NET 8이 record 위치파라미터에 property-타깃 검증 두면 InvalidOperationException→409. 거의 모든 [FromBody] 쓰기 엔드포인트 영향. JsonPropertyName(sync DTO)은 보존.
- [x] **근태 KST 쿼리경계 UTC화**: AttendanceService/ReportService가 `new DateTimeOffset(...,KstOffset)`(+09:00)를 timestamptz 쿼리 파라미터로 써 Npgsql ArgumentException → `.ToUniversalTime()`(같은 instant). 인메모리 `.ToOffset`는 보존.
- [x] **audit jsonb 정규화**: old_value/new_value(jsonb)에 평문(문서종류 등) 넣어 22P02 → AuditLogService.AsJson(이미 JSON이면 유지/아니면 래핑).
- [x] **통합테스트 1→12 green**(287 단위 포함 299/299), format clean, **code-review 통과**(Low 1: AsJson이 "123"/"true" 평문을 JSON리터럴로 저장 — 현 호출부 무영향).

## 남은 일
- [ ] **관리자 MFA 등록**(사람): ERP역할자 다음 로그인 TOTP setup 강제(admin-ui 지원, 즉시잠금X). Apple 암호앱.
- [ ] auth HR 명단 임포트로 sabun 채우기 → SECOM 매핑.
- [ ] position=erp_role 도출값 → HR 보정.
- [ ] PII_ENCRYPTION_KEY 안전 백업(.220 infra/.env, 유실=PII 복호화불가).
- [ ] (미세) string 컬럼 EF store=varchar(20) vs DB text 불일치 정리.

## 인계 노트
- snowball 운영 SSH는 글로벌 deny였음→사용자가 `~/.claude/settings.json`의 `Bash(ssh:*)` 주석처리로 허용. ssh hnedu-erp(.220)/hnedu-auth(.221).
- 동기화 부서→직원 순서 강제. auth 빈목록 시 의도적 중단.
- 롤백: auth DB=auth_db_backup_*.sql, 소스=auth_src_backup_*.tgz, ERP=server.bak_*.

---

# [활성 스레드] ai-ops Phase 4 — 패스스루(인터랙티브 세션)

> 이 Claude는 **snowball(집서버)** 에서 실행. 회사에서 VS Code Remote-SSH로 snowball 접속하면 **동일 워크스페이스·파일·커밋 그대로** 이어짐. 레포 = `/home/bbw/ai-ops`.
> 영구 계획·상태는 [[ai-ops-build-plan]] Phase 4 (✅ 구현완료 마킹). 결정 출처도 거기.

## 작업 요약 (ai-ops)
기존 `-p` one-shot(매 메시지 새 프로세스·중간조향 불가)을 **persistent claude 프로세스(1세션=1프로세스, stdin JSON 턴 주입)**로 전환. 출력=기존 SSE 재사용 + 입력=신규 `POST /api/sessions/:id/input`. 미결 3건 모두 승인·구현. **backend+frontend 코드 완료·로컬 검증 통과, 배포는 미진행(코드만 자동커밋)**.

## 완료 (검증됨)
- [x] **task 0 게이트**: claude 2.1.177 `--input-format stream-json` 멀티턴 실증 — 재spawn 없이 2턴 연속·맥락유지(4→40). resume 대체 불필요.
- [x] **DB**: `autobots/backend/db/schema.sql` `sessions` 테이블(id·status·runtime·model·cwd·conversation_id·pid·started/ended) + `idx_sessions_status`. additive, `npm run db:migrate` idempotent 확인.
- [x] **backend**: `autobots/backend/lib/session-manager.ts`(프로세스1개/세션, stdin write, SSE fan-out, idle 30분 정리, 동시캡 `MAX_SESSIONS=4`), `autobots/backend/routes/sessions.ts`(POST `/api/sessions`·GET `/:id/stream`SSE·POST `/:id/input`·POST `/:id/interrupt`·DELETE `/:id`·GET 목록/상태), `server.ts` register.
- [x] **frontend**: `autobots/frontend/app/chat/SessionPanel.tsx`(자체완결 Live UI) + `app/chat/page.tsx` `⚡ Live` 토글 + early-return(기존 멀티봇 플로우 분리=회귀차단).
- [x] **검증**: BE tsc 0 · FE tsc 0 · session-manager 프로브(14→42 맥락유지·라이프사이클·누수0) · 라우트 inject 9/9(404·400·429·lifecycle).
- [x] **안전가드 보존**: session-manager가 `claudePermissionArgs()` 재사용 → `CLAUDE_DISALLOWED_TOOLS`(rm -rf·sudo·git push 등) 그대로 차단.

## 다음 단계 (회사에서 이어갈 때)
- [x] **브라우저 수동 실증 완료 (2026-06-24, 회사 Remote-SSH→snowball, 임시 9250+로컬빌드 단일포트)**: ⚡ Live→Start(Opus)→멀티턴 스트리밍·맥락유지·Stop(조향)·다음 턴·End 전부 실 claude로 동작 확인. **실증 중 2건 수정**:
  - 🐞 **인터럽트 버그**: `interruptSession`이 SIGINT 전송 → 실 claude CLI(2.1.177)는 SIGINT에 **프로세스 종료** → Stop 누르면 세션 사망·다음 메시지 404/error. **수정**: stdin `control_request{subtype:interrupt}`로 전환(실증: CLI가 control_response ack+result(is_error)로 턴만 종료, 프로세스 생존). 상태는 result(=done)에 위임(경쟁조건 방지), 프론트 `interrupted`는 busy 유지·`done`까지 대기. → [[interactive-session-interrupt]]. 통합테스트 페이크도 control_request 모사하도록 갱신, 10/10 pass.
  - 🎨 **Stop 버튼 UX**: 헤더에만 있던 Stop을 응답 중 하단 Send→빨간 Stop 토글로 변경(직관성). `send()`에서 즉시 busy=true.
  - 🔧 `next.config.ts`: basePath/API를 env(`NEXT_BASE_PATH`/`NEXT_PUBLIC_API_URL`)로 오버라이드 가능(기본값=prod `/autobots` 유지). 로컬 단일포트 실증용.
- [x] **통합 테스트 파일화 (2026-06-24)**: `autobots/backend/routes/sessions.test.ts` 신규 — 스크래치 프로브를 node:test+fastify.inject 정식 테스트로 승격. 가짜 stream-json 바이너리(CLAUDE_BIN env 주입, 임시 DB)로 실 claude 없이 프로세스 라이프사이클 검증. 10케이스: 404×4·400·413·429·라이프사이클·persistent 멀티턴(pid 불변)·인터럽트 후 생존. `npm test` 전체 85 pass(기존 75+신규 10), tsc 0. **함정**: spawn 직후(<1ms) SIGINT 보내면 가짜가 SIGINT 핸들러 등록 전이라 죽음 → 인터럽트 테스트는 워밍업 턴 1회로 완전기동 후 인터럽트. (env는 동적 import 전 세팅 — static import 호이스팅이 stream-engine CLAUDE_BIN 상수를 먼저 캡처).
- [x] **배포 완료 (2026-06-24)**: 프론트 prod 재빌드(`out/` `/autobots`) → UI_DIR 볼륨 즉시 반영 / 백엔드 `docker compose build backend && up -d backend`로 `autobots_backend` 재생성. 검증: `/health` 200, `/api/sessions` JSON(=신규 라우트 라이브), 운영 9200 실 claude 스모크(haiku READY) OK. `ensureSchema`가 부팅 시 `sessions` 테이블 자동 생성. 절차 출처: [[server-infra]].
- [~] **codex/agy 패스스루 — Gate 0 실증 후 보류 (2026-06-24)**: agy=Live세션 **제외**(`--prompt-interactive` TTY전용, 파이프 0바이트). codex=resume 재spawn 방식으로 **가능하나 OpenAI workspace "out of credits"로 검증 불가** → **크레딧 충전 후 재개** 결정(미검증 선구현 금지=Phase4 교훈). 상세 [[runtime-passthrough-gate0]].
- [x] **A1 세션 대화 persist + 자동 재접속 (2026-06-24, 배포·운영검증 완료)**: session-manager가 턴(user/assistant)을 `chat_messages`(conversation_id=세션id, 스키마변경 없음)에 저장, 신규 `GET /api/sessions/:id/messages`, SessionPanel 마운트 시 실행중 세션 자동 재접속(메시지 로드+SSE 재구독). 통합테스트 +1(11케이스), 전체 95 pass·tsc 0(BE/FE). 배포: 프론트 prod 재빌드(.next 캐시제거+명시 env)+백엔드 컨테이너 교체, 운영 실 claude 스모크(MANGO persist+재접속 감지) OK. 브라우저 재접속 UX는 사용자 하드리로드 실증 잔여.
- [x] **B1 대화 라우팅 통합테스트 (2026-06-24)**: `routes/chat.test.ts` 9케이스(conversations/messages CRUD·검증·404, spawn 없는 순수 DB 경로). Phase 2b 회귀 그물.
- [~] **A2 인터랙티브 permission 프롬프트 — Gate 실패·제외 (2026-06-24)**: raw claude `-p stream-json`이 `can_use_tool` control_request 미발생(default 자동처리, `--permission-prompt-tool stdio`도 무효). MCP permission-prompt 서버 필요=큰 작업 → 제외. 기존 자동거부가 MVP 안전. [[interactive-session-interrupt]].
- [ ] (후속·범위밖) 다중 동시 세션 스케일.

## 인계 노트 (필독)
- **permission MVP 결정**: 인터랙티브 권한 프롬프트 노출 보류. headless stream-json `-p`에선 미허용 도구 자동 거부 = 안전. 진짜 프롬프트 노출은 `--permission-prompt-tool` 필요 → 후속.
- **stream-json 입력 포맷**: `{"type":"user","message":{"role":"user","content":[{"type":"text","text":"..."}]}}` + `\n`. spawn 플래그에 `--replay-user-messages` 포함(ack용).
- **턴 경계**: result 이벤트 = 턴 종료(프로세스 유지). session-manager가 `extractDelta/ToolUses/SkillUses/Fallback`(stream-engine.ts) 재사용.
- **세션 출력은 chat_messages에 저장 안 함**(휘발). persist는 후속 과제.
- 스크래치 프로브는 세션 scratchpad에 있음(세션 종료 시 소멸 가능) → 통합테스트 파일화 때 재작성.

---

# [보류 스레드] hnedu_erp — 세콤 근태 연동 (별개 프로젝트)

> ⚠️ 아래는 ai-ops와 **다른 프로젝트**. 이어가려면 `/home/bbw/projects/hnedu_erp`로 전환. 영구정보는 hnedu_erp 프로젝트 메모리.

## 작업 요약
세콤(SECOM) 근태 연동. **브리지 MS-SQL + ERP 폴링잡을 .220에 배포·가동 완료**(Pulled=0, 세콤 전송 대기). 사번(sabun) plumbing도 양쪽 커밋. **선결과제였던 auth↔ERP 식별자 불일치(auth Int / ERP Guid) = Option A(additive UUID)로 구현·로컬검증 완료(2026-06-24), 미배포.** auth는 `tsc` 통과, ERP는 build+test(286)+format 통과.

## ✅ Option A 구현 완료 (2026-06-24, 로컬검증 OK·미배포)
**auth (feat/mfa-totp)**: schema `Employee.uuid`·`Department.uuid`(unique @db.Uuid) + 마이그레이션 `prisma/migrations/20260624100000_add_uuid` / `tokenService.buildLoginPayload`에 `employeeUuid` 클레임 추가(`sub`=Int 불변) / `types/index.ts JwtPayload.employeeUuid` / `employeeService.listEmployees`에 `uuid`+`department_uuid` flat 노출 / `routes/admin/departments.ts`에 `uuid`+`parentUuid` 노출.
**ERP (main)**: `RbacHelper.GetActorId`가 `employeeUuid` 클레임 읽음(sub 아님) / `AuthEmployeeSyncItem`이 `uuid`·`department_uuid` 키 사용 / **신규 `DepartmentSyncService`**(IDepartmentSyncService, self-FK 2-pass upsert) — `EmployeeSyncService.SyncAsync`가 직원 전에 부서 동기화 먼저 호출(단일 순서 보장점) / `AdminSyncController` `POST /api/v1/admin/sync/departments` 추가 / `AuthIntegrationSettings.DepartmentsPath` / DI 등록 / 테스트 `DepartmentSyncServiceTests` 추가·`EmployeeSyncServiceTests` 페이로드를 uuid 계약으로 갱신 / `docs/DEV_CHECKLIST.md`에 2026-06-24 항목.

## ✅ 필드 임피던스 정합 완료 (2026-06-24, ERP측 변환, 빌드/287테스트/포맷 OK·미배포)
auth는 `jobTitle`(자유 직급)·`status`·`systemRoles`만 보유 → ERP 강한 enum을 `EmployeeSyncService.ApplyEmployee`에서 도출. `AuthEmployeeSyncItem`을 auth 실제 응답 형태(camelCase, 중첩 `systemRoles:[{systemRole:{systemCode,roleCode}}]`, `hireDate`=nullable ISO datetime)로 재정의.
- `erp_role` ← systemRoles[ERP/ALL] 최고권한(ALL.ADMIN→ADMIN 승격). auth가 역할 권위자.
- `rank` ← jobTitle, enum 일치 시 그대로 + 동의어('대표'→'대표이사', '상무이사/이사/관리자'→'임원'), 미상 '사원' 폴백.
- `position` ← **erp_role 도출**(ADMIN/EXEC→임원, DEPT_LEADER→팀장, 그 외 팀원). auth 원천 없음 → 배포 후 HR이 ERP에서 보정.
- `is_active` ← status=='ACTIVE'. `hireDate` 없으면 동기화일 폴백(DB NOT NULL).
- 매핑 분기 검증 테스트 추가(`EmployeeSyncServiceTests`: 역할 승격·직급 동의어·position 도출).

### 배포 잔여 (코드 외, 미실행)
- [ ] auth 마이그레이션 `20260624100000_add_uuid` `.221` 적용 (prisma migrate deploy)
- [ ] auth·ERP 양쪽 재배포(토큰 비파괴=클레임 추가만 → 재로그인 불필요). 순서: auth 마이그레이션→auth→ERP.
- [ ] 배포 후 `POST /api/v1/admin/sync/employees` 1회 호출로 부서→직원 동기화 실증.

> 영구 계획·결정·접속정보는 프로젝트 메모리(세션시작 자동주입): `~/.claude/projects/-home-bbw-projects-hnedu-erp/memory/`
> 특히 [[secom_bridge_connection]](접속정보·가동상태), [[secom_attendance_integration]], [[dotnet_local_build]], [[dev_env_remote_ssh]], [[project_deploy_plan]].
> 환경: 이 Claude는 **snowball(집서버)** 에서 실행. 집/회사 어디서든 snowball에 VS Code Remote-SSH 접속하면 **동일 워크스페이스·파일·커밋 그대로** 이어짐.

## 완료된 단계 (배포·가동 중)
- [x] 브리지 **MS-SQL 2025 Express(50GB)** .220 가동 — `infra/docker-compose.yml` `secom_mssql`(healthy), `SECOM` DB·로그인2개(secomlink 쓰기/erp_reader 읽기)·`T_SECOM_*` 4테이블. 세콤링크 접속확인됨.
- [x] **SECOM 폴링잡** `SecomAttendanceSyncJob`(5분, KST) .220 실가동 — 로그 `Secom attendance sync job completed. Pulled=0`. `T_SECOM_ALARM`→`gate_attendance_logs`(source=SECOM), 워터마크 `secom_sync_state`, 멱등. Domain `SecomPunchMapper`, `SecomAttendanceReader`(MS-SQL read-only).
- [x] **erp_api 컨테이너화** `server/Dockerfile`(net8.0 멀티스테이지, **tzdata 설치 필수**=Asia/Seoul) .220 배포·가동. compose erp_api env 키 정합 수정: `ConnectionStrings__DefaultConnection`(구 ErpDb=오류)·`__SecomDb`·`JwtSettings__PublicKeyUrl`·`FileStorage__BasePath`.
- [x] **잠복버그 수정**: `audit_logs.ip_address` inet→text(`db/migrations/020`). string↔inet 매핑 불가로 실 Npgsql 모델검증이 깨지던 것(InMemory 테스트로는 미검출).
- [x] **사번 plumbing 커밋(미배포·식별자정합 전엔 미동작)**: auth `Employee.sabun`+`importSabun`(부서+이름, 동명이인만 email)+`POST /sabun-import` / ERP `AuthEmployeeSyncItem.sabun`+`EmployeeSyncService` 매핑.

## 커밋 상태 (로컬만 — GitHub 키 미설정 → push 불가, 배포는 tar+ssh)
- **ERP(main)**: `fd89ad7`브리지 · `b241d12`폴링잡+2025 · `93e034c`컨테이너화 · `beb4d3b`AuditLog수정 · `f715a81`sabun매핑
- **auth(feat/mfa-totp)**: `558f89e`sabun

## 다음 단계 — Option A (additive UUID) 확정안, **미착수**
> 핵심: **JWT `sub`는 절대 안 바꾼다**(auth 내부 11곳이 `Number(sub)`로 Int id 사용). 크로스시스템 ID는 `employeeUuid` 클레임을 **추가**.

**hnedu-auth (순수 additive)**
- [ ] `prisma/schema.prisma`: `Employee.uuid` + `Department.uuid` (`@unique @db.Uuid @default(uuid())`)
- [ ] `prisma/migrations/<ts>_add_uuid/migration.sql`: `ADD COLUMN uuid uuid NOT NULL DEFAULT gen_random_uuid()` + unique index (employees, departments)
- [ ] `src/services/tokenService.ts` `buildLoginPayload`: `employeeUuid: employee.uuid` 추가 (sub=String(id) 유지)
- [ ] `src/types/index.ts` `JwtPayload`: `employeeUuid` 필드
- [ ] `src/services/employeeService.ts` `listEmployees`: `uuid` + `department_uuid` 응답 노출(기존 Int `id`는 유지=비파괴)
- [ ] `src/routes/admin/departments.ts`: `uuid` + `parentUuid` 노출(ERP 부서 동기화용)

**ERP**
- [ ] `Middleware/RbacHelper.cs` `GetActorId`: `"employeeUuid"` 클레임 읽기(sub 대신)
- [ ] `Dtos/EmployeeSyncDtos.cs` `AuthEmployeeSyncItem`: `id`←`uuid`, `department_id`←`department_uuid`(둘 다 Guid)
- [ ] **부서 동기화 신규**: auth `/api/v1/admin/departments` pull → ERP `departments` upsert(uuid 기준, parent는 2-pass) → **직원 동기화 전에** 실행해야 employee FK 성립
- [ ] docs(`CLAUDE.md`·`DEV_CHECKLIST.md`) "JWT sub=Guid" 표기를 "employeeUuid 클레임"으로 정정

**검증**: auth `npx prisma generate`(스키마 변경 후 필수)→`npx tsc --noEmit` / ERP build+test+format / 가능하면 로컬 compose 스택으로 동기화 1회 실증
**배포 순서**: auth 마이그레이션→auth→ERP. 토큰 비파괴(클레임 추가만)=재로그인 불필요.

## 인계 노트 (집에서 이어갈 때 필독)
- ⚠️ **JWT `sub` 변경 금지** — `requireAdmin.ts:33,74,83,100`, `tokenService.ts:57`, 모든 admin 라우트·`me`·`logout`이 `Number(sub)`로 Int 직원 id를 씀. uuid는 별도 클레임으로만.
- ⚠️ **ERP employees 테이블 비어 있음**(동기화 한 번도 성공 못함) → 깨뜨릴 데이터 없는 **가장 안전한 시점**. 부서 먼저 동기화해야 직원 FK 성립.
- **Claude Bash에서 .220/.221 SSH·git push 차단** → 서버 명령은 사용자가 직접 실행 후 결과 붙여넣기.
- **배포(코드 전송)**: 개발PC(`bbw@snowball`)에서
  `cd /home/bbw/projects/hnedu_erp && tar czf - --exclude='./.git' --exclude='infra/data' --exclude='infra/.env' --exclude='*/bin' --exclude='*/obj' . | ssh hnedu-erp 'mkdir -p ~/hnedu_erp && tar xzf - -C ~/hnedu_erp'`
- **.220 기동/재빌드**: `cd ~/hnedu_erp/infra && set -a && . ./.env && set +a` 후 `docker compose --profile apps up -d --build erp_api`. 마이그레이션 수동(init-scripts는 최초생성만 실행): `docker compose exec -T erp_postgres psql -U "$ERP_DB_USER" -d "$ERP_DB_NAME" -f /migrations/0NN_*.sql`.
- **ERP dotnet 게이트**: `export PATH="$HOME/.dotnet:$PATH" DOTNET_CLI_HOME=/tmp/.dotnet-node NUGET_PACKAGES=/tmp/.dotnet-node/.nuget/packages` → build/test/format.
- **로컬 전체 스택 실증 가능**(snowball, docker O): `infra/.env`(로컬테스트용·gitignored) 존재. `docker compose up -d erp_postgres secom_mssql` → `docker compose up secom_mssql_init` → `docker compose --profile apps up -d --build erp_api`. erp_postgres 신규생성 시 마이그레이션 001~020 자동적용. 끝나면 `docker compose --profile apps down -v`.
- **세콤링크 입력값**: Provider=MS-SQL / SERVER IP=`192.168.0.220` / PORT=`1433` / DB명.dbo=`SECOM.dbo` / USER=`secomlink` / PW=.220 `.env`의 `SECOMLINK_PASSWORD`.
- **운영 잔여(코드 외)**: ①세콤링크 전송설정(세콤 벤더)→Pulled>0 ②HR 명단 사번 임포트 호출 ③auth 마이그레이션 `.221` 적용 ④Caddy HTTPS 라우팅(클라이언트 접속용).
- 미세 미정: 부서 동기화 소스 — 확정안은 auth `/admin/departments`에 uuid+parentUuid 노출 후 ERP 전용 동기화(employee-embed 방식 대비 중간노드 누락 없음).
- `references/secom/`·`references/.../경조비...png`는 내가 만든 것 아님 — 손대지 말 것.

## 이전 미해결 스레드 (2026-06-19, 별개 — 잊지 말 것)
- **[이슈1] 인증서 신뢰 오류**: 회사 PC Windows 신뢰루트에 옛 루트 교체 필요(회사 PC 필요, 집에서 불가). 기준지문 `FD28056AEF8FCE48D2A7F260EABE0D20C07A5BB4`. 상세는 git 이력/메모리.
- **[이슈2] MFA TOTP 배포**: `hnedu_auth/docs/MFA_DEPLOY.md` 런북대로 `.221`에서 적용·검증 대기(코드는 `feat/mfa-totp`에 구현 완료 — auth가 이 브랜치인 이유). prisma migrate deploy + .env(MFA_TOKEN_EXPIRES_IN/MFA_ISSUER) + 스모크테스트.
