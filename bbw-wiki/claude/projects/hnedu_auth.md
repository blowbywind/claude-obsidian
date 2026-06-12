# hnedu_auth

## 핵심
해냄에듀 사내 통합 인증 서비스. JWT(RS256) 발급. ERP·CRM의 인증 허브.

⚠️ **주의**: 실제 UI는 `admin-ui/` (Next.js 15 + Tailwind + Radix UI). `public/admin/`은 레거시 — 수정 금지.

## 현재 상태
- 서버: hnedu-server (192.168.0.221), 경로: `/var/web-infra/hnedu_auth/`
- 외부: `https://auth.snowball.me.kr`
- 내부: `http://192.168.0.221:3100/health`

## 아키텍처
- 인증 서비스 → JWT 발급 → ERP·CRM이 공개키로 검증
- 직원 계정, 부서, 직급, 시스템별 역할 관리
- UI: `admin-ui/` (Next.js 15) — 실제 서비스
- 레거시: `public/admin/` (Vanilla JS) — 건드리지 말 것

## 주의사항
- HTML에 `role="combobox"`, `aria-controls="radix-..."`, `bg-[#353534]` 등이 보이면 admin-ui 코드
- 수정 전 반드시 `find`로 프로젝트 구조 확인

## 현재 보안 상태 (2026-06-11 기준)
- **패치 완료**: INJ 10개 + JWT-007 + XSS 파일 제거
- **미구현 수용**: JWT-009 access token 블랙리스트 (JWT-007 15m TTL로 실질적 완화)
- **잔여 항목**: 실서비스 연동 후 7-4(ERP), 8-4(CRM) 통합 테스트

## 주요 API 엔드포인트
- `POST /api/v1/auth/login` — JWT 발급
- `POST /api/v1/auth/refresh` — 토큰 갱신
- `GET /api/v1/auth/public-key` — RS256 공개키 (ERP·CRM 검증용)
- `GET /api/v1/admin/employees` — 직원 목록 (requireAdmin)
- `GET /api/v1/admin/audit-logs` — 감사 로그

## 작업 히스토리
- 2026-06-11: 보안 감사 + 전체 취약점 패치 (INJ 10개 + JWT-007) + 배포
- 2026-06-11: admin-ui 관리자 무한 루프 버그 수정 (isAdminToken 검증 추가)
- 2026-06-04: 부서 드롭다운·사이드바 UI 수정 (잘못된 파일 수정 사고 → 교훈)
