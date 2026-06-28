# hnedu_erp

동기화: 2026-06-28 KST

## 핵심
해냄에듀 ASP.NET Core 8 Web API + ERP. SECOM 근태 연동, auth↔ERP UUID 통합, Postgres.
배포: .220 서버 (`/home/hnedu/hnedu_erp/`), Docker `erp_api` 컨테이너 가동 중.

## 현재 상태 (2026-06-28)
- 브랜치: `main` + 로컬 미커밋 변경 배포 반영
- 서버: hnedu-erp (192.168.0.220), 앱 compose 기준: `/home/hnedu/hnedu_erp/infra/docker-compose.yml`
- API: `erp-api.snowball.me.kr`, `api.hnedu-erp.co.kr` HTTPS health 200
- 웹: `www.hnedu-erp.co.kr` HTTPS 200, `/login` 200
- 마이그레이션: 001~024 적용 완료

## 운영 중인 기능 (2026-06-25 기준)
- SECOM 폴링잡(5분): `gate_attendance_logs` 수집 — Inserted=885, 백로그 51455펀치 자동 처리 중
- auth↔ERP UUID 통합(Option A): employeeUuid 클레임, 31명 전원 uuid/phone_hash 채워짐
- SECOM CardNo 폰 매핑: 규칙=`폰앞6+등록코드2+폰뒤5`, 27/30 매칭, 매핑 직원 24명 확인
- 앱 전역 enum→text 전환: 27컬럼, 42804 버그 해결
- 동기화 서비스: EmployeeSyncJob, 부서→직원 순서, auth 서비스토큰 연동

## 잔여 이슈
- MFA 등록: ERP 역할자 다음 로그인 TOTP setup 강제 (admin-ui 지원, 미착수)
- 미매핑 2명: 정덕균·조성진 — HR 카드등록/폰 확인 필요
- 인증서 신뢰 오류: 회사 PC Windows에 구 루트 교체 (회사 PC 필요)
- 세콤링크 전송 설정: 벤더 측 설정 대기 (Pulled=0 상태)
- `hnedu-erp.co.kr` apex: Caddy 인증서 발급 실패. `www.hnedu-erp.co.kr`은 정상이며 apex A 레코드가 192.168.0.220으로 잡힌 뒤 재검증 필요.
- 인프라 기준 통합: `/home/hnedu/hnedu_erp/infra/Caddyfile`은 최신 reverse_proxy 설정으로 동기화됨. 단, `erp_caddy`·`erp_step_ca` 컨테이너는 아직 `/opt/hnedu-erp/infra` compose 라벨로 실행 중. `/home/.../infra/data`가 root 소유이고 `botsudo`가 없어 CA/Caddy 데이터 이동은 보류.
- 웹 클라이언트: 결재·서류·리포트·검색·장기근속·업무보고·업무첨부 API 모듈은 추가됨. 대시보드 결재·서류 화면 배선은 아직 후속 범위. `pay` 도메인은 별도 백엔드 컨트롤러 부재로 정적 유지. 메일 메시지 목록, 조직 직원 이름·이메일은 현재 DTO 미제공이라 화면에 `API 미제공`으로 표시.

## 아키텍처
- 서버: ASP.NET Core 8, EF Core Code-First, PostgreSQL (db_postgres:5432)
- 컨테이너: `infra/docker-compose.yml` — erp_api, erp_web, erp_postgres, secom_mssql, secom_mssql_init
- 배포: tar+ssh (GitHub push 불가), `~/hnedu_erp/infra/.env` gitignored
- Caddyfile: `/home/hnedu/hnedu_erp/infra/Caddyfile`와 `/opt/hnedu-erp/infra/Caddyfile` 내용 일치. 실행 중인 Caddy는 아직 `/opt` compose 라벨.
- SECOM bridge: MS-SQL 2025 Express — T_SECOM_PERSON, T_SECOM_ALARM 등

## 배포 명령 (snowball에서)
```bash
cd /home/bbw/projects/hnedu_erp && tar czf - --exclude='./.git' --exclude='infra/data' --exclude='infra/.env' --exclude='*/bin' --exclude='*/obj' . | ssh hnedu-erp 'tar xzf - -C ~/hnedu_erp'
# .220에서:
cd ~/hnedu_erp/infra && docker compose --profile apps up -d --build erp_api
```

## 작업 히스토리
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
