---
updated: 2026-06-19 (집 PC 재개 — 이슈1 서버진단 완료, Phase C 착수)
project: hnedu_erp (+ hnedu_auth Phase C)
branch: main
---

## 작업 요약: 인프라 배포검증 완료 + 이슈1 서버측 진단 완료(회사PC 신뢰루트 교체만 남음) → Phase C(auth TOTP MFA) 착수

> 영구 계획·결정은 프로젝트 메모리: `~/.claude/projects/-home-bbw-projects-hnedu-erp/memory/` 의
> `project_deploy_plan.md`, `dev_env_remote_ssh.md` (세션 시작 시 자동주입). 1차 앵커는 그쪽.

### 완료된 단계
- [x] 원격 개발환경: 작업PC → VS Code Remote-SSH → 회사 ERP서버 .220 (직접접속 A형)
- [x] 동적IP 대응: ipTIME 무료 DDNS `hnedu-work-2005.iptime.org` → 회사 공인IP 자동추적 (고정IP 계약 없음 → WAN 고정설정 금지)
- [x] SSH config (`bbw@snowball:~/.ssh/config`): `hnedu-erp`(2220→.220:22), `hnedu-auth`(2222→.221:22), 키인증 동작
- [x] step-ca PKI 초기화 + **프로비저너 충돌 해결**(compose `DOCKER_STEPCA_INIT_PROVISIONER_NAME` acme→admin, `rm -rf data/step-ca` 재init). ca.json `JWK/admin`+`ACME/acme` 확인
- [x] **Caddy ACME 인증서 발급 성공** — `erp-api.snowball.me.kr`, TLS-ALPN-01, issuer=사내CA. 사내 CA 발급체계 실증
- [x] 루트 추출(`/opt/hnedu-erp/infra/certs/root_ca.crt`) + 오프라인 백업(tgz)
- [x] 회사 PC 1대 Windows 신뢰루트 설치 (Import-Certificate)
- [x] Phase C 계획 수립 + hnedu_auth 코드 매핑 완료

### 다음 단계 (이어서 할 일)
- [~] **[열린이슈 1] 인증서 신뢰 오류** — 회사 PC 브라우저 `https://erp-api.snowball.me.kr` → `ERR_CERT_AUTHORITY_INVALID`.
  - **2026-06-19 진단 완료: 서버 측 정상.** (A)step-ca 루트 = (B)Caddy 마운트 루트 일치 = `FD:28:05:6A:EF:8F:CE:48:D2:A7:F2:60:EA:BE:0D:20:C0:7A:5B:B4` (콜론제거 `FD28056AEF8FCE48D2A7F260EABE0D20C07A5BB4`). s_client 체인 2개(리프+중간, issuer=Hnedu Internal CA Intermediate CA) 정상.
  - **남은 단 하나: 회사 PC Windows 신뢰저장소의 옛 루트 교체.** 회사 PC PowerShell(관리자):
    1) `Get-ChildItem Cert:\LocalMachine\Root | ? {$_.Subject -like "*Hnedu*"} | fl Thumbprint` → 위 기준지문과 비교
    2) 다르면 `... | Remove-Item` 후 `Import-Certificate -FilePath <root_ca.crt> -CertStoreLocation Cert:\LocalMachine\Root`
    3) 브라우저 완전 종료 후 재시작
  - ⚠️ **회사 PC에 묶임 → 집에서 진행 불가.** 회사 PC 닿을 때 위 3스텝만 실행하면 종료.
- [~] **[열린이슈 2] Phase C — `hnedu_auth` TOTP MFA 코드 구현 완료(06-19, 집PC).** 결정 3건 모두 권장안 채택(① 2단계 pending→otp ② ERP역할 setup 강제 ③ 복구코드 10개).
  - **구현 파일**: schema.prisma(mfaEnabled+MfaSecret+MfaRecoveryCode), migrations/20260619150000_add_mfa, utils/crypto.ts(encrypt/decrypt 일반화), plugins/jwt.ts(signMfaToken), types/index.ts(isMfaTokenPayload), middlewares/requireAdmin.ts(requireMfaToken+typ거부), services/{tokenService(buildLoginPayload),authService(login분기+completeLogin),mfaService}, routes/auth/mfa.ts(setup/verify-setup/verify), routes/admin/mfa.ts(리셋), app.ts
  - **라이브러리**: otplib **12.0.1 고정**(v13은 authenticator 프리셋 제거됨), qrcode 1.5.4. AES-256-GCM은 기존 crypto.ts 재사용.
  - **품질게이트 통과**: tsc --noEmit exit 0 / code-reviewer 지적(Critical typ검증·복구코드 경쟁조건·계정brute-force·복구코드반환보장·crypto버퍼) 모두 수정 / evaluator-strict 5/5 요구사항 충족.
  - **Admin UI(Next.js16) MFA 화면 완료(06-19)**: login/page.tsx 상태머신(credentials→mfa-verify|mfa-setup→recovery), lib/mfa-api.ts(mfaToken 전용 fetch, sessionStorage 비노출), components/auth/{mfa-verify,mfa-setup,mfa-recovery}-step.tsx, utils ACTION_LABEL MFA 추가. tsc·eslint(신규파일) 클린. code-reviewer: Critical 없음(High1·Med2 UX개선만 반영). 커밋 `6a1b7c9`.
  - **남은 일(배포 환경 필요)**: ① `prisma migrate deploy` 마이그레이션 적용(.221 DB) — 집/snowball DB 연결 미확인 ② 서버 .env에 MFA_TOKEN_EXPIRES_IN/MFA_ISSUER ③ pnpm approve-builds(prisma/bcrypt/esbuild) ④ ERP WinForms 로그인 2단계 처리(미착수, .csproj 없음) ⑤ 통합테스트(실제 OTP 흐름).
  - **커밋 상태**: `feat/mfa-totp` 브랜치에 5커밋(deps/db/server/admin-ui/runbook). main 미머지. **remote 없음+gh 미설치 → push/PR 불가.**
  - **환경 한계 확정(06-19)**: snowball은 **코드 전용 워크스페이스** — `.env`·`keys/`·로컬 Postgres 모두 없음. 따라서 마이그레이션 적용·.env 설정·통합테스트는 **전부 .221 런타임에서만** 가능(이 Claude 세션 불가). 
  - **배포 런북 작성**: `hnedu_auth/docs/MFA_DEPLOY.md` — .221에서 pnpm install/approve-builds → .env MFA변수 → prisma migrate deploy → build/restart → curl 스모크테스트(5종: ERP setup강제·MFA 2단계·비ERP 즉시·mfa토큰 차단 401·관리자리셋)+롤백. **다음 .221 세션에서 이 문서대로 적용·검증하면 종료.**
- [ ] (선택) .220 sshd 하드닝(`PasswordAuthentication no`) + fail2ban (sudo OK 확인됨)
- [ ] (앱 준비 후) Caddyfile `respond` placeholder → `reverse_proxy erp_api`

### 인계 노트 (집에서 이어갈 때 필독)
- **이 Claude는 snowball(집서버 221.165.64.216)에서 실행** — 작업PC는 VS Code Remote-SSH로 snowball 접속. **집/회사 어느 PC든 snowball 접속하면 동일 환경·메모리·파일 유지** → 컴퓨터 바뀌어도 워크스페이스 그대로 이어짐.
- **Claude의 Bash에서 회사 .220 SSH는 차단** → 서버 명령은 사용자가 직접 실행 후 결과 붙여넣기 방식. (.220에서 Claude가 직접 빌드하려면 VS Code를 .220에 Remote-SSH + Claude Code 서버측 설치 필요)
- IP/도메인: 회사 공인 218.235.63.196(동적). `erp-api.snowball.me.kr`→192.168.0.220(사설=LAN전용, 의도된 것) / `auth.snowball.me.kr`→218.235.63.196(공인=외부노출).
- **비밀값**: step-ca CA 비번은 .220 볼륨 `secrets/password` + 비번관리자 보관. 절대 메모리/git 금지.
- hnedu_auth 코드 매핑: Employee(passwordHash=bcrypt12, phoneEncrypted=AES-256-GCM), 로그인 `src/services/authService.ts`+`src/routes/auth/login.ts`, JWT클레임 `src/types/index.ts`(systems Record), 토큰 `src/services/tokenService.ts`(RS256, issueTokenPair/rotate), 암호화 `src/utils/crypto.ts`(encryptPhone/decryptPhone→일반화 재사용), 마이그레이션 `prisma/migrations/YYYYMMDDHHmmss_*`. TOTP 라이브러리 미설치(otplib 추가 예정). Admin UI=Next.js15.
