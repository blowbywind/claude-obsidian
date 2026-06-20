---
title: Caddyfile
type: concept
tags: [caddy, config, web-server, dsl]
created: 2026-06-20
summary: Caddy 웹 서버의 선언적 설정 파일. 간결한 DSL로 리버스 프록시·TLS·라우팅을 정의. JSON API의 인간 친화적 대안.
---

## 정의

Caddy 웹 서버의 주요 설정 파일 형식. JSON Admin API 대신 사용 가능한 인간 친화적 DSL로, 리버스 프록시·자동 TLS·라우팅 규칙을 간결하게 선언한다.

## 기본 구조

```caddyfile
# 전역 설정
{
    email admin@example.com
}

# 사이트 블록
example.com {
    reverse_proxy localhost:3000
}

api.example.com {
    reverse_proxy localhost:8080
    header X-Forwarded-For {remote_host}
}
```

## 특징

- 들여쓰기 기반 블록 구조
- 자동 HTTPS는 도메인 선언만으로 활성화
- `import` 지시자로 파일 분할 가능

## 관련 연결

- [[wiki/entities/caddy]] — 적용 대상 웹 서버
- [[wiki/concepts/automatic-https]] — Caddyfile에서 자동 활성화되는 TLS
- [[wiki/sources/2026-06-12-caddy-v2-docs]] — 공식 문서 출처
