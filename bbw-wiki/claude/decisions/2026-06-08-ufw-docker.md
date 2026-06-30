---
date: 2026-06-08
project: web-infra
status: 적용 완료
tags: [infra, docker, ufw, security, networking]
summary: "UFW와 Docker 병용 시 ufw reload에서 Docker 규칙 소멸 및 UFW 우회 문제를 ufw-docker로 해결."
---

# ufw-docker 도입

**날짜**: 2026-06-08
**프로젝트**: web-infra
**상태**: 적용 완료

## 결정
UFW + Docker 병용 환경에서 `ufw-docker` 툴을 도입한다.

## 배경
- `ufw reload` 시 Docker가 iptables에 추가한 MASQUERADE/FORWARD 규칙이 소멸
- Docker가 UFW를 우회해 `ports:` 설정된 컨테이너가 UFW 규칙 무관하게 외부 노출됨

## 검토한 대안
| 방법 | 결론 |
|---|---|
| iptables 직접 관리 | 복잡도 높음, 실수 위험 |
| `/etc/ufw/after.rules` 수동 편집 | Docker UFW 우회 문제 미해결 |
| **ufw-docker** | 두 문제 모두 해결, 난이도 낮음 |

## 결과
- `ufw reload` 이제 안전
- 외부 접근 필요한 컨테이너는 `sudo ufw-docker allow <container> <port>/tcp` 명시 필요
- 현재 허용: `web_caddy 80/tcp`, `web_caddy 443/tcp`
