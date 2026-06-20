# hnedu_erp

동기화: 2026-06-20 08:02 KST

## 핵심
해냄에듀 Windows 바탕화면 고정형 업무 근태 통합 대시보드 (win-screen).
Phase 0(프로토타입) 완료 → Phase 1(WinForms 셸) 착수 전.

## 현재 상태
- 위치: /home/bbw/projects/hnedu_erp
- 기획서: docs/PLAN.md (Ch.1~9, 최종)
- 디자인 시스템: docs/DESIGN.md
- 작업 리포트: docs/리포트.md (2026-06-09~10 전체 작업 기록)
- 참조 이미지: references/ (읽기 전용, 수정 금지)
- UI 목업: prototype/index.html (v3, 1920x1080)

## 인프라 현황 (2026-06-19, step-ca PKI)
- step-ca PKI 초기화 완료 + 프로비저너 충돌 해결
- Caddy ACME 인증서 발급 성공: erp-api.snowball.me.kr (TLS-ALPN-01, issuer=사내CA)
- 루트 인증서: /opt/hnedu-erp/infra/certs/root_ca.crt
- 회사 PC 1대 Windows 신뢰루트 설치 완료

## 열린 이슈
1. 회사 PC 브라우저 ERR_CERT_AUTHORITY_INVALID
   - 서버 측 정상 확인 (지문: FD28056AEF8FCE48D2A7F260EABE0D20C07A5BB4)
   - 남은 작업: 회사 PC PowerShell(관리자)로 옛 루트 교체
     Get-ChildItem Cert:LocalMachineRoot | ? {$_.Subject -like "*Hnedu*"} | Remove-Item
     Import-Certificate -FilePath root_ca.crt -CertStoreLocation Cert:LocalMachineRoot
   - 집에서 진행 불가 (회사 PC 필요)

## 프로토타입 구조 (2026-06-08 모듈화)
prototype/
- index.html (HTML 스켈레톤 1602줄)
- css/app.css (전체 스타일 911줄)
- js/db.js, utils.js, render.js, calendar.js, tasks.js, mail.js, forms.js, app.js

로드 순서 의존성: db → utils → render → calendar → tasks → mail → forms → app

## 규칙
- prototype/index.html 수정 후 docs/DESIGN.md + docs/PLAN.md 반드시 동기화
- references/ 는 참조만, 기획 기준은 docs/PLAN.md
- Live Server 포트: 5502 고정 (http://127.0.0.1:5502/prototype/index.html)
- JS는 글로벌 스코프 유지 (ES module 금지 — onclick 핸들러 호환성)

## 작업 히스토리
- 2026-06-19: step-ca PKI 구축 + Caddy HTTPS 인증서 발급 성공
- 2026-06-09~10: 공지 페이지네이션 Spotlight 검색 추가, 모노리식 HTML → CSS+JS 8파일 모듈화
- 2026-06-08: prototype/index.html 이동 모듈화 시작
- 2026-06-07: 배지 통합 (조건부 실행 사고 교훈)
