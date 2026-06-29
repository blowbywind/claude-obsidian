---
title: Caddy
type: concept
tags: [caddy, web-server, reverse-proxy, https, docker, caddyfile]
created: 2026-06-12
updated: 2026-06-12
sources: [2026-06-12-caddy-v2-docs]
summary: "TLS 자동 발급, Caddyfile 설정, JSON API 무중단 변경을 지원하는 Go 기반 웹 서버다."
---

## 정의

Caddy v2는 **자동 HTTPS**를 내장한 Go 기반 웹 서버. nginx/Apache와 달리 TLS 인증서 발급·갱신에 certbot이나 cron이 필요 없다. Caddyfile이라는 간결한 DSL로 설정하며 JSON Admin API로 무중단 변경이 가능하다.

---

## 자동 HTTPS

DNS A/AAAA 레코드가 서버를 가리키고 포트 80·443이 열려 있으면 **설정 없이** 자동 인증서 발급.

- **CA 순서**: ZeroSSL → Let's Encrypt (폴백)
- **챌린지**: HTTP-01(포트 80) + TLS-ALPN-01(포트 443) 기본 활성화
- **갱신**: 만료 30일 전 자동, 지수 백오프로 최대 30일 재시도
- **localhost/내부 IP**: Caddy 내장 CA로 자체 서명 인증서 (`tls internal`)
- **와일드카드**: DNS-01 챌린지 필수 (별도 플러그인), Caddy 2.10+에서 서브도메인 인증서 재사용

```caddyfile
# 이것만으로 자동 HTTPS 활성화
example.com {
    file_server
}
```

---

## Caddyfile 문법

### Site Blocks

```caddyfile
example.com {
    reverse_proxy localhost:8080
}

# 다중 호스트
example.com, www.example.com {
    file_server
}
```

### 핵심 디렉티브

#### reverse_proxy
```caddyfile
example.com {
    reverse_proxy localhost:8080

    reverse_proxy localhost:8080 {
        lb_policy round_robin           # random, least_conn, ip_hash
        health_uri /healthz
        health_interval 10s
        header_up Host {upstream_hostport}
        header_up X-Real-IP {remote_host}
    }
}
```
기본으로 `X-Forwarded-For`, `X-Forwarded-Proto`, `X-Forwarded-Host` 헤더 추가.

#### handle / handle_path
```caddyfile
example.com {
    # handle: 첫 번째 매칭만 실행 (상호 배타적)
    handle /api/* {
        reverse_proxy localhost:9000
    }
    handle {   # 폴백
        file_server
    }
}

# handle_path: /app prefix 제거 후 upstream 전달
# /app/foo → /foo
handle_path /app/* {
    reverse_proxy localhost:3000
}
```

#### log (access logging)
```caddyfile
example.com {
    log {
        output file /var/log/caddy/access.log {
            roll_size 100mb
            roll_keep 5
        }
        format json
        level INFO
    }
}
```

**JSON 로그 주요 필드**:

| 필드 | 설명 |
|------|------|
| `remote_ip` | TCP 연결 직접 피어 IP (프록시 뒤면 프록시 IP) |
| `client_ip` | `trusted_proxies` 설정 시 X-Forwarded-For에서 파싱한 실제 클라이언트 IP |
| `status` | HTTP 응답 코드 |
| `duration` | 응답 시간 (초) |
| `size` | 응답 바이트 |

리버스 프록시 뒤에서 실제 접속자 IP 추적:
```caddyfile
{
    servers {
        trusted_proxies static 10.0.0.0/8 172.16.0.0/12 192.168.0.0/16
    }
}
```

#### tls
```caddyfile
localhost { tls internal }                      # 자체 서명 (개발용)
example.com { tls /path/cert.pem /path/key.pem } # 커스텀 인증서
```

#### file_server
```caddyfile
example.com {
    root * /var/www/html
    file_server {
        browse          # 디렉터리 목록
        hide .git .env  # 숨길 파일
    }
}
```

### Matchers (요청 필터링)
```caddyfile
# 경로 매처 (내장)
reverse_proxy /api/* localhost:9000

# Named Matcher (@이름)
@api {
    path /api/*
    method GET POST
}
reverse_proxy @api localhost:9000

# 기타 조건: host, header, query, method, expression
@websocket {
    header Connection *Upgrade*
    header Upgrade websocket
}
```

같은 named matcher 블록 내 여러 타입 → **AND**. 같은 타입이 여러 값 → **OR**.

### Snippets (재사용)
```caddyfile
(logging) {
    log { output file /var/log/caddy/access.log; format json }
}

example.com {
    import logging
}
```

---

## JSON vs Caddyfile

JSON이 Caddy 네이티브 설정 언어. Caddyfile은 JSON으로 변환되는 adapter.

| 항목 | Caddyfile | JSON |
|------|-----------|------|
| 가독성 | 높음 | 낮음 (장황) |
| 표현력 | 95% 커버 | 100% (완전한 API) |
| 프로그래밍 생성 | 어려움 | 쉬움 |
| API 세밀 변경 | `/load` 전체만 | `/config/*` 경로별 |

```bash
# Caddyfile → JSON 변환 확인
caddy adapt --config /etc/caddy/Caddyfile --adapter caddyfile --pretty
```

**Admin API 주요 엔드포인트** (`localhost:2019`):
- `POST /load` — 전체 설정 교체 (실패 시 자동 롤백)
- `GET /config/` — 현재 설정 조회
- `PATCH /config/[path]` — 특정 경로 교체

---

## Docker 배포

### 표준 docker-compose.yml
```yaml
services:
  caddy:
    image: caddy:2.11
    restart: unless-stopped
    cap_add:
      - NET_ADMIN        # HTTP/3 QUIC 필수
    ports:
      - "80:80"
      - "443:443"
      - "443:443/udp"   # HTTP/3
    volumes:
      - ./caddy:/etc/caddy          # 디렉터리 마운트 (파일 직접 마운트 금지!)
      - caddy_data:/data            # 인증서 저장 (named volume 필수)
      - caddy_config:/config

volumes:
  caddy_data:
  caddy_config:
```

### caddy reload (무중단 설정 적용)
```bash
# 컨테이너 내에서
docker compose exec -w /etc/caddy caddy caddy reload

# 실패 시 자동 롤백, container restart보다 항상 선호
```

| | `caddy reload` | container restart |
|---|---|---|
| 다운타임 | 없음 | 있음 |
| 실패 시 | 자동 롤백 | 새 설정으로 시작 실패 |
| TLS 인증서 | 유지 | 재로드 |

---

## HTTP/2, HTTP/3

- **HTTP/2**: TLS 시 자동 활성화 (ALPN `h2`), 별도 설정 불필요
- **HTTP/3**: TLS 시 자동 활성화, UDP 443 방화벽 허용 + `cap_add: NET_ADMIN` 필요
- `Alt-Svc: h3=":443"; ma=86400` 헤더로 클라이언트에 자동 광고
- 브라우저 미지원 시 HTTP/2 → HTTP/1.1 자동 폴백

---

## 주요 함정 (Gotchas)

### 1. Docker inode 바인드 마운트 문제 ★★★
**증상**: Caddyfile 수정 후 `caddy reload` 성공인데 변경이 반영 안 됨.

**원인**: vim/VS Code 등 에디터는 임시 파일에 쓴 뒤 rename → 새 inode 생성. Docker의 파일 단위 bind-mount는 컨테이너 시작 시점의 구 inode를 가리켜 새 inode를 인식 못 함.

**해결**: 파일 대신 **디렉터리를 마운트**.
```yaml
# 잘못됨
- ./Caddyfile:/etc/caddy/Caddyfile

# 올바름
- ./caddy:/etc/caddy
```

컨테이너 내부에서 직접 수정해야 할 때:
```bash
docker exec web_caddy sh -c 'cat > /etc/caddy/Caddyfile' < ./Caddyfile
```

### 2. staging CA 오염
테스트용 스테이징 CA 인증서가 `/data` 볼륨에 남아 프로덕션에서도 사용됨.
```bash
docker compose down && docker volume rm <project>_caddy_data && docker compose up -d
```

### 3. caddy adapt 멀티라인 출력
`caddy adapt` 출력이 멀티라인 JSON — 첫 줄은 warning, 두 번째 줄이 실제 config. `"apps"` 키 포함 줄을 찾아서 파싱해야 함.

### 4. curl로 Caddyfile 전송 시 줄바꿈 손실
```bash
# 잘못됨 (-d는 줄바꿈 제거)
curl -d @Caddyfile http://localhost:2019/load

# 올바름
curl --data-binary @Caddyfile http://localhost:2019/load
```

### 5. Let's Encrypt 속도 제한
동일 도메인 주당 5회 발급 제한. 개발/테스트 시 스테이징 CA 사용:
```caddyfile
example.com {
    tls { issuer acme { ca https://acme-staging-v02.api.letsencrypt.org/directory } }
}
```

### 6. Admin API 비활성화 시 reload 불가
`admin off` 설정 시 `caddy reload`가 동작하지 않음. 컨테이너 재시작이 유일한 수단.

---

## 관련 개념

- [[wiki/concepts/automatic-https]] — ACME 프로토콜 심화
- [[wiki/entities/caddy]] — Caddy 소프트웨어·커뮤니티 정보

## 출처

- [[wiki/sources/2026-06-12-caddy-v2-docs]]
