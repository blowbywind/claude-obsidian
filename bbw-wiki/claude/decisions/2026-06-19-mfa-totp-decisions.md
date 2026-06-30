---
date: 2026-06-19
project: hnedu_auth
status: 구현 완료 (배포 대기)
tags: [hnedu_auth, mfa, totp, security, auth]
summary: "hnedu_auth TOTP MFA: 2단계 로그인(credentials→mfa_token→OTP), ERP역할 강제setup, 복구코드 10개 채택, 배포.221 필수"
---

hnedu_auth TOTP MFA 핵심 결정 3건

날짜: 2026-06-19 / 프로젝트: hnedu_auth / 상태: 구현 완료 (배포 .221 필요)

## 배경
Phase C TOTP MFA 구현 시 아키텍처 결정 3건 사용자 승인 후 채택.
브랜치: feat/mfa-totp (5커밋, main 미머지·미push)

## 결정 1: 2단계 로그인 (pending to otp)
채택: credentials -> mfa_token -> OTP -> access/refresh
대안 A(단일요청) 거부: 첫 setup 시 닭-달걀 문제 발생

범위:
  - mfaEnabled=true: credentials -> mfa_token -> verify -> access/refresh
  - ERP역할 보유 + 미설정: credentials -> mfa_token -> QR setup -> access/refresh
  - ERP역할 없음: credentials -> 즉시 access/refresh

## 결정 2: ERP 역할 보유자 MFA setup 강제
채택: systems 클레임에 ERP 역할 1개라도 있으면 setup 필수
근거: ERP = 급여/근태/개인정보, 가장 민감. CRM은 추후 결정.
구현: authService.login() hasMfaSetup 체크, routes/auth/mfa.ts 3 엔드포인트

## 결정 3: 복구코드 10개
채택: 16자 랜덤 코드 10개, 1회 사용 후 폐기
근거: 업계표준(GitHub/Google 10개 내외), SHA-256 해시 저장
주의: /verify-setup 시 1회만 반환 / brute-force 동일 지연 응답

## 라이브러리
otplib 12.0.1 고정 (v13 authenticator 프리셋 제거됨)
qrcode 1.5.4 / AES-256-GCM은 기존 crypto.ts 재사용

## 품질 게이트
tsc: exit 0 / code-reviewer Critical 0 / evaluator-strict 5/5

## 배포 잔여
1. prisma migrate deploy (.221 DB)
2. .env MFA_TOKEN_EXPIRES_IN=5m, MFA_ISSUER=해냄에듀
3. pnpm approve-builds
4. ERP WinForms 2단계 (미착수)
5. 통합테스트
런북: hnedu_auth/docs/MFA_DEPLOY.md
