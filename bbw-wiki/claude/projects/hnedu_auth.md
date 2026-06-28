# hnedu_auth

동기화: 2026-06-25 KST

## 핵심
해냄에듀 사내 통합 인증 서비스. JWT(RS256) 발급. ERP·CRM의 인증 허브.

주의: 실제 UI는 admin-ui/ (Next.js 15 + Tailwind + Radix UI). public/admin/은 레거시 수정 금지.

## 현재 상태
- 서버: hnedu-server (192.168.0.221), 경로: /var/web-infra/hnedu_auth/
- 외부: https://auth.snowball.me.kr
- 내부: http://192.168.0.221:3100/health
- 브랜치: feat/mfa-totp (4커밋, main 미머지 미push)

## 아키텍처
- 인증 서비스 → JWT 발급 → ERP·CRM이 공개키로 검증
- 직원 계정, 부서, 직급, 시스템별 역할 관리
- UI: admin-ui/ (Next.js 15) — 실제 서비스
- 레거시: public/admin/ (Vanilla JS) — 건드리지 말 것

## MFA TOTP 구현 (2026-06-19, feat/mfa-totp 브랜치)
- 결정: 2단계 pending→otp 플로우 / ERP역할 setup 강제 / 복구코드 10개
- 라이브러리: otplib 12.0.1 고정 (v13 authenticator 프리셋 제거됨), qrcode 1.5.4
- DB: schema.prisma (mfaEnabled + MfaSecret + MfaRecoveryCode) + migration 20260619150000
- 서버 구현: utils/crypto.ts, plugins/jwt.ts, middlewares/requireAdmin.ts
  services/tokenService, authService, mfaService
  routes/auth/mfa.ts (setup/verify-setup/verify), routes/admin/mfa.ts
- Admin UI: login/page.tsx 상태머신, lib/mfa-api.ts, components/auth/mfa-{verify,setup,recovery}-step.tsx
- 커밋: 6a1b7c9
- 품질게이트: tsc 클린 / code-reviewer Critical 0 / evaluator-strict 5/5

## 배포 현황 (2026-06-24, .221 완료)
- ✅ feat/mfa-totp 브랜치 → .221 배포 완료 (prisma migrate deploy 포함)
- ✅ UUID + sabun 컬럼 마이그레이션 (31명 전원 uuid 채워짐)
- ✅ 서비스토큰 신설 (`svc_` 불투명토큰, IP 화이트리스트)
- ✅ ERP 연동 실증: EmployeeSyncJob 부서12+직원31 완료
- 남은 것: ERP 역할자 TOTP setup 강제 (관리자 MFA 등록, 즉시잠금X)

## 현재 보안 상태 (2026-06-11 기준)
- 패치 완료: INJ 10개 + JWT-007 + XSS 파일 제거
- 미구현 수용: JWT-009 access token 블랙리스트 (JWT-007 15m TTL로 실질적 완화)
- 잔여 항목: 실서비스 연동 후 7-4(ERP), 8-4(CRM) 통합 테스트

## 작업 히스토리
- 2026-06-19: MFA TOTP 전체 구현 완료 (서버 + Admin UI), feat/mfa-totp 브랜치 4커밋
- 2026-06-11: 보안 감사 + 전체 취약점 패치 (INJ 10개 + JWT-007) + 배포
- 2026-06-11: admin-ui 관리자 무한 루프 버그 수정 (isAdminToken 검증 추가)
- 2026-06-04: 부서 드롭다운 사이드바 UI 수정 (잘못된 파일 수정 사고 교훈)
