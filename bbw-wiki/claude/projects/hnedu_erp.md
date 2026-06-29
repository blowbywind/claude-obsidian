# hnedu_erp

동기화: 2026-06-29 KST (2차)

## 핵심
해냄에듀 ASP.NET Core 8 Web API + ERP. SECOM 근태 연동, auth↔ERP UUID 통합, Postgres.
배포: .220 서버 (`/home/hnedu/hnedu_erp/`), Docker `erp_api` 컨테이너 가동 중.

## 현재 상태 (2026-06-29 최종)
- 브랜치: `feat/web-client-auth`; 최신 커밋 `c384458` (세콤 Flag1 검증 문서)
- 커밋 히스토리: 9670804(KST) → 0ef8261(문서) → 155e937(세콤 운영검증) → 34842a9(API스모크+apex) → c384458(Flag1검증)
- 서버: hnedu-erp (192.168.0.220), DDNS: `hnedu-work-2005.iptime.org:2220`
- API: `erp-api.snowball.me.kr`, `api.hnedu-erp.co.kr` HTTPS health 200
- 웹: `hnedu-erp.co.kr`(apex), `www.hnedu-erp.co.kr` HTTP→HTTPS 308→정상
- 인증서: `hnedu-erp.co.kr`(apex), `www.hnedu-erp.co.kr`, `api.hnedu-erp.co.kr` step-ca ACME 자동갱신 성공 (2026-06-29 확인)
- 마이그레이션: 001~025 적용 완료
- MFA 강제: ERP API `Mfa__RequireOtp=true`, JWT `amr=otp` 검증 운영 반영
- KST 통일: CompanyTime 기반, 전 컨테이너 `TZ=Asia/Seoul`, PostgreSQL `timezone=Asia/Seoul`

## 운영 중인 기능 (2026-06-29 기준)
- SECOM 폴링잡(5분): `T_SECOM_ALARM` 51,610건 원천 확인, `gate_attendance_logs` SECOM 38,199건 수집, 최신 `tag_time=2026-06-29 21:17:50+09`
- auth↔ERP UUID 통합(Option A): employeeUuid 클레임, 31명 전원 uuid/phone_hash 채워짐
- SECOM CardNo 폰 매핑: 규칙=`폰앞6+등록코드2+폰뒤5`, 27/30 매칭, 매핑 직원 24명 확인
- 앱 전역 enum→text 전환: 27컬럼, 42804 버그 해결
- 동기화 서비스: EmployeeSyncJob, 부서→직원 순서, auth 서비스토큰 연동

## 잔여 이슈
- MFA 등록: ERP 역할자 7명 중 2명 설정 완료, 5명은 다음 로그인 시 TOTP setup 강제.
- 미매핑 2명: 정덕균·조성진 — HR 카드등록/폰 확인 필요
- 인증서 신뢰 오류: 회사 PC Windows에 구 루트 교체 (회사 PC 필요)
- 세콤 신규 인입: 워터마크 `20260629211750` 이후 신규 원천 데이터가 없어 최근 잡은 `Pulled=0, Inserted=0`으로 정상 무변경
- `hnedu-erp.co.kr` apex: Caddy 인증서 발급 실패. `www.hnedu-erp.co.kr`은 정상이며 apex A 레코드가 192.168.0.220으로 잡힌 뒤 재검증 필요.
- 인프라 기준 통합: `/home/hnedu/hnedu_erp/infra/Caddyfile`은 최신 reverse_proxy 설정으로 동기화됨. 단, `erp_caddy`·`erp_step_ca` 컨테이너는 아직 `/opt/hnedu-erp/infra` compose 라벨로 실행 중. `/home/.../infra/data`가 root 소유이고 `botsudo`가 없어 CA/Caddy 데이터 이동은 보류.
- 웹 클라이언트: 결재·서류·리포트·검색·장기근속·업무보고·업무첨부 API 모듈은 추가됨. 2026-06-29 결재 탭(`/approvals/pending`·상세·승인·반려), 서류 탭(PDF Blob 다운로드·연말정산 업로드·발급 이력), HR 전용 급여 요약(`/pay/*` 4개), 메일 계정 `displayName`/`isConnected`, 조직 직원 이름·이메일 표시까지 대시보드에 연결됨. 메일 메시지 목록도 `/mail/messages` 실 API로 전환되어 운영 반영됨.

## 아키텍처
- 서버: ASP.NET Core 8, EF Core Code-First, PostgreSQL (db_postgres:5432)
- 컨테이너: `infra/docker-compose.yml` — erp_api, erp_web, erp_postgres, secom_mssql, secom_mssql_init
- 배포: tar+ssh (GitHub push 불가), `~/hnedu_erp/infra/.env` gitignored
- Caddyfile: `/home/hnedu/hnedu_erp/infra/Caddyfile`와 `/opt/hnedu-erp/infra/Caddyfile` 내용 일치. 실행 중인 Caddy는 아직 `/opt` compose 라벨.
- SECOM bridge: MS-SQL 2025 Express — T_SECOM_PERSON, T_SECOM_ALARM 등

## 배포 명령 (snowball에서)
```bash
cd /home/bbw/projects/hnedu_erp
tar czf - --exclude='*/bin' --exclude='*/obj' server | ssh -p 2220 hnedu@hnedu-work-2005.iptime.org 'tar xzf - -C ~/hnedu_erp'
tar czf - --exclude='.env*' --exclude='node_modules' --exclude='.next' --exclude='out' --exclude='.turbo' web-client | ssh -p 2220 hnedu@hnedu-work-2005.iptime.org 'tar xzf - -C ~/hnedu_erp'
# .220에서:
cd ~/hnedu_erp/infra && docker compose --profile apps up -d --build erp_api erp_web
```

## 작업 히스토리
- 2026-06-29: KST 기준선 커밋 운영 재동기화 완료 — 백업 `/home/hnedu/hnedu_erp_pre_sync_kst_baseline_20260629T225213+0900.tgz` 생성 후 `server/`, `web-client/`를 DDNS `hnedu-work-2005.iptime.org:2220` 경유로 동기화(`.env*`, 빌드 산출물 제외). `docker compose --profile apps config --quiet` 통과, `erp_api`·`erp_web` 재빌드/재기동 성공. 운영 검증: 컨테이너 running, PostgreSQL `Asia/Seoul`, API health 200 및 `timestamp +09:00`, 웹 `/`·`/login` 200, protected API 15개 미인증 요청 401, `gate_attendance_logs` SECOM 38,199건/최신 `2026-06-29 21:17:50+09`, `T_SECOM_ALARM` 51,610건. 22:55 세콤 잡은 신규 원천 없음으로 `Pulled=0, Inserted=0`. 로컬 검증: Release 빌드 통과, 단위 테스트 359/359 통과, `dotnet format --verify-no-changes` 통과, web-client `tsc`/`lint`/`build` 통과. 세콤 운영 검증 문서 커밋 `155e937` 생성 후 운영 서버 `docs/`도 동기화. 원격 서버는 현재 `dotnet` 명령이 PATH에 없어 원격 테스트는 미실행.
- 2026-06-29: KST 변경분 git 기준선 고정 — `feat(timezone): unify ERP to KST across all layers` 커밋 `9670804` 생성. 검증: `dotnet build server/HneduErp.sln --configuration Release` 통과, `dotnet test server/HneduErp.Tests/HneduErp.Tests.csproj --configuration Release` 359/359 통과, `dotnet format server/HneduErp.sln --verify-no-changes --no-restore` 통과, `git diff --check` 통과. 새 운영 동기화 시도는 현재 SSH `192.168.0.220:22` 타임아웃으로 보류.
- 2026-06-29: ERP KST CompanyTime fallback 운영 재배포 완료 — .220 현재 관련 파일 백업 `/home/hnedu/hnedu_erp_pre_companytime_fallback_20260629T185756+0900.tgz` 생성 후 로컬 소스를 `infra` 제외 tar+ssh로 `/home/hnedu/hnedu_erp`에 동기화. `CompanyTime.GetTimeZone()`의 IANA·Windows·고정 KST fallback이 운영 소스에 반영된 것을 확인하고, `docker compose --profile apps build erp_api erp_web && docker compose --profile apps up -d erp_api erp_web` 성공. 운영 검증: `erp_api`·`erp_web` running, 컨테이너 `KST +0900`, PostgreSQL `SHOW timezone=Asia/Seoul`, API health 200 및 `timestamp +09:00`, 웹 `/`·`/login` 200, 재기동 직후 치명 오류 없음.
- 2026-06-29: ERP KST 통일 이어받기 로컬 마무리 — `CompanyTime.GetTimeZone()`에 IANA(`Asia/Seoul`)·Windows(`Korea Standard Time`)·고정 KST fallback을 추가하고, 영수증 다운로드도 기존 UTC 월 폴더 fallback 테스트를 보강. 검증: `dotnet test server/HneduErp.Tests/HneduErp.Tests.csproj --configuration Release` 359/359 통과, `dotnet test server/HneduErp.IntegrationTests/HneduErp.IntegrationTests.csproj --configuration Release` 15개 Docker 부재로 skip, `dotnet format server/HneduErp.sln --verify-no-changes` 통과, `git diff --check` 통과. 운영 읽기 전용 재확인: `erp_api`·`erp_web`·`erp_postgres`·`erp_secom_mssql` 모두 `KST +0900`, PostgreSQL `SHOW timezone=Asia/Seoul`, API health `timestamp +09:00`.
- 2026-06-29: ERP KST 통일 운영 배포 완료 — 로컬 KST 변경 파일 29개만 tar+ssh로 .220 `/home/hnedu/hnedu_erp`에 반영. 서버 기존 파일 백업: `/home/hnedu/hnedu_erp_pre_kst_20260629T184255+0900.tgz`. `docker compose --profile apps build erp_api erp_web` 성공 후 `erp_postgres`·`erp_api`·`erp_web` 재생성. 운영 검증: `erp_postgres`·`erp_api`·`erp_web`·`erp_secom_mssql` 모두 `Asia/Seoul`/`KST +0900`, PostgreSQL `SHOW timezone` = `Asia/Seoul`, `now()` = `+09`, `api.hnedu-erp.co.kr/health` 200 및 `timestamp +09:00`, `hnedu-erp.co.kr` 200. 재기동 직후 API·웹 로그에 치명 오류 없음.
- 2026-06-29: ERP KST 통일 로컬 수정 완료 — `CompanyTime` 공용 유틸로 업무 기준 현재시각·오늘·연차연도·KST 일자 경계를 통일하고, 출근 요약·주간 근태·외근 오늘 조회·연차 기본연도·장기근속 보상 연도·문서 발급일·보고 기간·배치잡 기준일을 KST로 정리. `infra/docker-compose.yml`/`docker-compose.verify.yml`의 `erp_postgres`는 `TZ`·`PGTZ`·`postgres -c timezone=Asia/Seoul`로 세션 표시까지 KST 고정, `erp_api`/`erp_web`/`web-client` 런타임도 `TZ=Asia/Seoul`로 고정. 검증: `DOTNET_CLI_HOME=/tmp/dotnet-cli-home dotnet build server/HneduErp.sln --configuration Release` 통과, 단위 테스트 357/357 통과, 통합 테스트는 로컬 Docker CLI 부재로 미실행, `dotnet format --verify-no-changes` 및 `git diff --check` 통과.
- 2026-06-29: MFA 강제 활성화 완료 — .221 auth `.env`에 `MFA_TOKEN_EXPIRES_IN=5m`, `MFA_ISSUER=해냄에듀` 추가 후 `hnedu_auth` 재생성. ERP 역할자 집계: active 7명, MFA 설정 2명, setup 대기 5명. .220 ERP API는 `Mfa:RequireOtp=true`일 때 JWT `amr`에 `otp`가 없으면 401 `MFA_REQUIRED`를 반환하도록 미들웨어 추가, auth 공개키 JSON 봉투(`data.public_key`) 파싱 보정, auth 토큰 계약에 맞춰 audience 검증 비활성. 운영 검증: `api.hnedu-erp.co.kr/health` 200, 익명 보호 엔드포인트 401, production auth 키로 서명한 `amr=["pwd"]` 토큰은 401 `MFA_REQUIRED`, `amr=["pwd","otp"]` 토큰은 `/api/v1/mail/messages` 200. .220 실환경 `dotnet test server/HneduErp.sln --configuration Release`: 단위 333/333 + 통합 15/15 통과.
- 2026-06-29: 메일 메시지 API 및 웹 배선 운영 배포 완료 — 로컬 소스·문서·`025_mail_messages.sql`을 .220 `/home/hnedu/hnedu_erp`로 동기화하되 `infra` 런타임 파일은 보존. `025_mail_messages.sql`을 Postgres에 `ON_ERROR_STOP=1`로 적용해 `mail_messages` 테이블과 인덱스 생성. `docker compose --profile apps up -d --build erp_api erp_web`로 API/웹 재빌드·재기동. 검증: `erp_api`/`erp_web` running, `erp_postgres` healthy, `erp-api.snowball.me.kr/health` 200, `api.hnedu-erp.co.kr/health` 200, `www.hnedu-erp.co.kr` `/`·`/login` 200, `/api/v1/mail/messages` 미인증 요청 401.
- 2026-06-29: 메일 메시지 목록 API 개발 — `025_mail_messages.sql`로 `mail_messages` 메타데이터 캐시 테이블 추가, `/api/v1/mail/messages?accountId=&folder=&page=&limit=` 신설. 조회는 JWT `employeeUuid` 기준 본인 활성 메일 계정으로 제한하며 타인 계정은 404. web-client 메일 탭은 `API 미제공` 대신 실 API 결과를 기존 계정·폴더·페이지네이션 렌더러로 표시. 외부 IMAP/OAuth 자격증명과 원문 본문은 서버 미저장.
- 2026-06-29: `mail_messages` DB 변경 문서화 보강 — `CLAUDE.md` 핵심 DB 테이블 목록에 `mail_messages` 추가, `docs/PLAN.md` Ch.6에 목록 렌더링용 외부 메일 메타데이터 평문 저장 범위와 금지 항목(자격증명·본문·첨부 원문·내부 직원 마스터 PII)을 명시.
- 2026-06-29: 통합테스트 15개 실제 환경 검증 완료 — .220 서버(Docker 29.1.3)에 .NET SDK 8.0.422 설치 후 Testcontainers PostgreSQL로 실행. 15/15 전부 통과: RBAC(401/403), 휴가 워크플로(신청→승인/차단), 자기결재 차단(404), 근속보상 멱등성·동시성(409 정확히 1건), 근태수정 감사로그, 증명서 PDF. P1 완전 종결.
- 2026-06-29: web-client 잔여 화면 배선 — 결재 탭은 `/approvals/pending` 목록·상세 드로어·승인/반려 Mutation 연결, 서류 탭은 `/documents/certificate` PDF Blob 다운로드·`/documents/tax-return` 파일 업로드·`/documents/history` 표시 연결, 지출 탭은 HR_TEAM 이상 전용 `/pay/summary`·`/pay/overtime-allowances`·`/pay/approved-expenses`·`/pay/tenure-rewards` 요약 블록 연결. 메일 계정 칩은 `displayName`/`isConnected`, 조직도는 백엔드 마스킹/복호화 DTO 값을 표시.
- 2026-06-29: 백엔드 API 갭 보강 — HR_TEAM 이상 전용 `PayController` 추가(`/pay/summary`, `/pay/overtime-allowances`, `/pay/approved-expenses`, `/pay/tenure-rewards`), `OrgService` 직원 DTO에 이름·이메일 추가(본인/팀장 이상 전체 표시, 일반 조직도 조회 마스킹), `MailAccountDto`에 displayName/providerLabel/isConnected 추가. web-client는 `pay.ts` API 모듈 추가, 조직도 이름·이메일 표시 연결, mail/org 타입 보강. 검증: Release 빌드 0경고/0오류, 단위 테스트 317/317 통과, 로컬 통합테스트 15개는 Docker 소켓 부재로 skip, `dotnet format --verify-no-changes` 통과.
- 2026-06-28: web-client 누락 API 모듈 7개 추가 — `approval`, `document`, `report`, `search`, `tenure-reward`, `work-report`, `task-attachment`. 공통 `request` 래퍼는 기존 JSON 봉투 처리 유지 + FormData 업로드와 Blob 다운로드 응답 지원으로 확장. 검증: `pnpm exec tsc --noEmit`, `pnpm lint`, `pnpm build`, 서버 `dotnet build --configuration Release`, 단위 테스트 311개, `dotnet format --verify-no-changes`, `git diff --check` 통과. 통합 테스트 15개는 현재 환경에서 기존과 동일하게 skip.
- 2026-06-28: 로컬 미커밋 작업본을 서버 `/home/hnedu/hnedu_erp`에 동기화하고 `docker compose --profile apps up -d --build erp_web` 실행. Compose 의존성으로 `erp_api`도 재빌드·재기동됨. 검증: `erp_api`/`erp_web` running, `erp_postgres`/`erp_secom_mssql` healthy, API health 200, `www.hnedu-erp.co.kr` `/`·`/login` HTTPS 200. `hnedu-erp.co.kr` apex는 step-ca ACME challenge timeout으로 TLS 실패.
- 2026-06-28: 로컬 미커밋 web-client/API 배선 및 통합테스트 정리 재검증 — `web-client` `tsc --noEmit`/`pnpm lint`/`pnpm build` 통과. 신규 `mail`/`meetings`/`org` API 모듈은 서버 라우트·DTO와 대조 완료. 서버 `dotnet build --configuration Release`, 단위 테스트 311개, `dotnet format --verify-no-changes`, `git diff --check` 통과. 통합 테스트 15개는 현재 셸에 `docker` 명령이 없어 Testcontainers 가용성 검사에서 skip. 커밋·배포는 미진행.
- 2026-06-27: web-client 텍스트 파리티 기준 확정 — 실 API 모드에서는 정본 mock 데이터값 1:1 비교 대신 레이아웃·클래스·주요 고정 라벨·상태 문구를 완료 기준으로 적용. 데이터값 완전 대조는 동일 API fixture/seed가 있는 별도 테스트 모드로 분리.
- 2026-06-27: web-client 서버 실행 후 1920×1080 파리티 캡처 완료 — `NEXT_PUBLIC_AUTH_BYPASS=1 pnpm dev`와 prototype 정적 서버로 정본/배포본 캡처 생성. CSS 복사본 일치, 배포본 전용 클래스 0건, Dev Gate `tsc --noEmit`/`pnpm lint`/`pnpm build` 통과. 정본 mock 데이터값 완전 대조는 동일 API fixture/seed가 있는 별도 테스트 모드로 분리.
- 2026-06-27: web-client 실 API 배선 2차 게이트 보정 완료 — KST 기준일 통일, 메일 카운트 silent fallback 제거, 조직도 직원 전체 페이지 로드, 업무검색/근태리포트 백드롭 파리티 보정. Dev Gate `tsc --noEmit`/`pnpm lint`/`pnpm build` 통과.
- 2026-06-27: web-client 실 API 배선 2차 완료 — 회의(`/meetings`), 메일 계정(`/mail/accounts`), 조직도(`/org/departments`, `/org/employees`) 연결. Dev Gate `tsc --noEmit`/`pnpm lint`/`pnpm build` 통과.
- 2026-06-25: SECOM CardNo 디코드 버그 정정 (`0d08096`), 매핑 직원 4→24명, 재배포 완료
- 2026-06-25: 미커밋 코드 커밋 완료 (3커밋: feat세콤+test+chore)
- 2026-06-24: auth↔ERP UUID 통합 배포, 동기화 실증(부서12+직원31), 쓰기경로 버그 3종 수정
- 2026-06-24: auth .221 MFA+UUID 마이그레이션 배포 (feat/mfa-totp → .221 가동)
- 2026-06-24: 서비스토큰 신설, 통합테스트 12/12 green
- 2026-06-19: step-ca PKI, Caddy HTTPS 인증서
