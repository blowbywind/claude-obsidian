---
name: server-infra
description: autobots 서버 인프라, Caddy 라우팅, Docker 배포 워크플로 요약.
metadata:
  type: reference
---

# server-infra

autobots는 Docker 백엔드와 Caddy reverse proxy 뒤에서 운영됩니다.

## 핵심
- 백엔드 코드 변경은 이미지 재빌드 후 재기동이 필요하다.
- `/autobots*` 외부 접근은 Caddy 인증 뒤에 둔다.
- Caddy 설정과 Docker compose 변경은 배포 영향이 크므로 변경 전후 상태를 확인한다.

## 관련
- [[claude/projects/web-infra]]
- [[bot-autonomous-sudo]]
