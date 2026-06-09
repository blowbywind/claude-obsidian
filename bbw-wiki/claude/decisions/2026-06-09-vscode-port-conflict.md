---
date: 2026-06-09
project: web-infra
status: 해결됨
tags: [vscode, live-server, port, debugging]
---

# VS Code 원격 환경 포트 충돌 사례 (2026-06-09)

## 증상
- 프로토타입 브라우저 빈화면 (ERR_CONNECTION_REFUSED)
- DevTools Network 탭: 요청 없음
- DevTools Elements: `<body></body>` 비어있음

## 원인
진단 목적으로 실행한 `python3 -m http.server 8090 &` 백그라운드 프로세스가 VS Code Ports 패널에 포트 항목을 등록 → Live Server 재시작 시 포트 충돌

## 해결
VS Code Ports 패널에서 스테일 포트 항목 삭제 → Live Server 재시작

## 교훈
- VS Code 원격 환경에서 백그라운드 HTTP 서버 실행 금지
- 빈화면 + 네트워크 요청 없음 → Ports 패널 먼저 확인
