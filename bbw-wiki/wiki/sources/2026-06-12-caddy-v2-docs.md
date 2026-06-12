---
title: Caddy v2 공식 문서 — 리버스 프록시·자동 HTTPS·Caddyfile 종합
type: source
tags: [caddy, web-server, reverse-proxy, https, docker]
created: 2026-06-12
updated: 2026-06-12
origin: https://caddyserver.com/docs/
author: Matthew Holt, Caddy contributors
date_published: 2024-ongoing
---

## 요약

Caddy v2는 Go로 작성된 웹 서버로 **자동 HTTPS**가 핵심 차별점이다. Let's Encrypt/ZeroSSL 인증서를 별도 도구 없이 발급·갱신하며, Caddyfile이라는 간결한 DSL로 설정한다. 현재 버전 v2.11.4 (2026-06-03).

## 핵심 주장

- TLS 인증서 발급·갱신이 완전 자동화 — certbot, cron 불필요
- JSON이 네이티브 설정, Caddyfile은 JSON으로 변환되는 config adapter
- `caddy reload`로 무중단 설정 적용 (실패 시 자동 롤백)
- HTTP/1.1·2·3 모두 기본 지원
- Admin REST API (`localhost:2019`)로 런타임 설정 변경 가능

## 연결된 개념

- [[wiki/concepts/caddy]]
- [[wiki/concepts/automatic-https]]
- [[wiki/concepts/caddyfile]]

## 연결된 엔티티

- [[wiki/entities/caddy]]
- [[wiki/entities/matthew-holt]]

## 메모

- inode 바인드 마운트 문제: Docker에서 파일 단위 마운트 시 에디터의 rename 방식 저장으로 inode 교체 → 컨테이너 내부에 반영 안 됨. **디렉터리 마운트** 필수.
- staging CA 오염: 테스트용 스테이징 CA 인증서가 `/data`에 남으면 프로덕션 전환 후에도 사용됨. `/data` 볼륨 초기화 필요.
- HTTP/3 방화벽: UDP 443 별도 허용 + `cap_add: NET_ADMIN` 필요
- caddy adapt 멀티라인: `-d` 대신 `--data-binary` 사용 필수
