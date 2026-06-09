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

## 작업 히스토리
- 2026-06-04: 부서 드롭다운·사이드바 UI 수정 (잘못된 파일 수정 사고 → 교훈)
