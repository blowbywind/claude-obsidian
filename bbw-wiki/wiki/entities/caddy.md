---
title: Caddy (Web Server)
type: entity
tags: [product, open-source, web-server, go]
created: 2026-06-12
updated: 2026-06-12
sources: [2026-06-12-caddy-v2-docs]
---

## 개요

- **종류**: 오픈소스 웹 서버 / 리버스 프록시
- **언어**: Go
- **라이선스**: Apache 2.0
- **최신 버전**: v2.11.4 (2026-06-03)
- **GitHub Stars**: 73.3k
- **개발 시작**: 2014년, Matthew Holt
- **v2 출시**: 2020년
- **후원**: ZeroSSL (HID Global)
- **공식 사이트**: https://caddyserver.com
- **GitHub**: https://github.com/caddyserver/caddy

## 주요 특징

1. **자동 HTTPS** — Let's Encrypt/ZeroSSL 인증서 자동 발급·갱신 (certbot 불필요)
2. **Caddyfile DSL** — 간결한 설정 언어 (nginx 설정 대비 70% 이상 짧음)
3. **단일 바이너리** — 런타임 의존성 없음
4. **HTTP/1·2·3 기본 지원** — TLS 시 자동 활성화
5. **Admin REST API** — `localhost:2019`로 무중단 설정 변경
6. **고성능 리버스 프록시** — 로드밸런싱, 헬스체크, 재시도 내장

## 시장 위치

- 웹 서버 점유율: ~0.1% (2025 기준, 성장 중)
- nginx: ~38.6%, Apache: ~25%
- 홈서버·스타트업·DevOps 자동화 환경에서 빠르게 채택 중

## 현재 사용 환경 (bbw 홈서버)

`/opt/web-infra`의 Docker Compose 스택에서 리버스 프록시로 운용 중.

- 포트: 80, 443, 9119
- 컨테이너: `web_caddy` (이미지: `caddy:latest`)
- Caddyfile: `/opt/web-infra/Caddyfile`
- 연관 서비스: hermes-dashboard, postgres/adminer, seaweedfs
- 접속 도메인: `snowball.me.kr`

상세: [[claude/projects/web-infra]]

## 주요 연결

- [[wiki/concepts/caddy]] — Caddyfile·자동 HTTPS·함정 전체 가이드
- [[wiki/entities/matthew-holt]] — 창업자

## 출처

- [[wiki/sources/2026-06-12-caddy-v2-docs]]
