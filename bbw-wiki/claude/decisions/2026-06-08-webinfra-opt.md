---
date: 2026-06-08
project: web-infra
status: 적용 완료
tags: [infra, docker, filesystem, linux]
---

# web-infra 위치 /opt로 이전

**날짜**: 2026-06-08
**프로젝트**: web-infra
**상태**: 적용 완료

## 결정
Docker Compose 프로젝트를 `/home/bbw/web-infra`에서 `/opt/web-infra`로 이전한다.

## 배경
- `/home`은 사용자 개인 공간 — 서비스가 특정 계정에 종속됨
- `/opt`는 자체 완결형 서드파티 애플리케이션 위치 (Linux FHS 관례)

## 결과
- `sudo mv /home/bbw/web-infra /opt/web-infra` (같은 파티션이라 데이터 복사 없음)
- 도중 `rm -rf /opt/web-infra` 사고 발생 → docker-compose.yml, Caddyfile 재생성으로 복구
- **교훈**: 위험 명령어 제안 시 "이미 완료됐으니 재실행 금지" 명시 필요
