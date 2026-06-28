---
name: autobots-hardening-backlog
description: autobots 백엔드 보안과 안정성 개선 백로그.
metadata:
  type: project
---

# autobots-hardening-backlog

autobots 백엔드의 심층 방어, 안정성, 입력 검증, 실행 제어 관련 남은 개선 항목을 추적하는 백로그입니다.

## 축
- 동시 실행 캡과 타임아웃으로 비용 폭주를 막는다.
- SSRF, 과대 입력, webhook, 권한 상승 표면을 정책으로 제한한다.
- 스키마와 라우트 검증을 일원화한다.
- 자율 실행은 항상 감사 로그와 복구 경로를 남긴다.

## 관련
- [[bot-autonomous-sudo]]
- [[server-infra]]
- [[effective-improvement-workflow]]
