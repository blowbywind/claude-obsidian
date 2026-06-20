---
title: Automatic HTTPS
type: concept
tags: [web-server, security, tls, caddy, let-s-encrypt]
created: 2026-06-20
summary: 웹 서버가 Let's Encrypt ACME 프로토콜로 TLS 인증서를 자동 발급·갱신하는 기능. Caddy가 2015년 최초로 기본값으로 채택.
---

## 정의

웹 서버가 Let's Encrypt(또는 ZeroSSL) **ACME 프로토콜**을 통해 TLS 인증서를 설정 없이 자동으로 발급·갱신하는 기능. Caddy가 2015년 최초로 기본값으로 채택, 이후 업계 표준으로 자리 잡음.

## 동작 원리

1. 도메인 소유권 증명 (HTTP-01 또는 DNS-01 챌린지)
2. Let's Encrypt에서 인증서 발급 (DV, 90일 유효)
3. 만료 30일 전 자동 갱신 (무중단)

## Caddy 예시

```caddyfile
example.com {
    reverse_proxy localhost:3000
    # TLS 자동 설정 — 추가 설정 불필요
}
```

## 관련 연결

- [[wiki/entities/caddy]] — 처음 기본값으로 채택한 웹 서버
- [[wiki/entities/matthew-holt]] — 개념 선도자
- [[wiki/concepts/caddyfile]] — Caddy 설정 파일
