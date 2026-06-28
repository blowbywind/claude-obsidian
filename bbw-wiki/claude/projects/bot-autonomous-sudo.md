---
name: bot-autonomous-sudo
description: 봇 자율 sudo 실행 모델과 보안 경계 요약.
metadata:
  type: project
---

# bot-autonomous-sudo

봇이 필요한 권한 상승 작업을 `botsudo`로 요청하고, 백엔드 큐와 호스트 executor가 정책에 따라 실행하는 구조입니다.

## 핵심 경계
- 봇은 컨테이너 안의 비루트 프로세스로 실행된다.
- 실제 권한 상승은 호스트 executor가 담당한다.
- 승인 시크릿은 봇 실행 환경에서 제거되어 자기 승인이 불가능해야 한다.
- 자동 허용은 패키지 설치, 서비스 재시작, 파일 권한, 포트/프로세스 관리처럼 정책으로 제한된 범위만 허용한다.

## 관련
- [[autobots-hardening-backlog]]
- [[server-infra]]
