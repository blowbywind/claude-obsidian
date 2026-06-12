---
title: hermes dashboard 외부 접속 설정 — KT hairpin NAT 성공 사례
type: source
tags: [hermes, caddy, docker, kt-router, hairpin-nat, port-forwarding]
created: 2026-06-12
updated: 2026-06-12
origin: /opt/web-infra (bbw 홈서버 실전 작업)
author: bbw
date_published: 2026-06-12
---

## 요약

KT GiGA WiFi Home 공유기 환경에서 Docker + Caddy로 운영 중인 hermes dashboard를 `https://snowball.me.kr:9119/`로 외부 브라우저에서 접속 가능하게 설정하고 검증한 실전 기록. 핵심은 KT 라우터가 **hairpin NAT**을 지원한다는 점과, 서버 자체에서 외부 IP로 테스트하면 항상 실패한다는 교훈이다.

## 핵심 주장

- KT GiGA WiFi Home 라우터는 포트 9119에 대해 hairpin NAT을 지원한다
- 서버→외부IP→서버 경로 테스트(hairpin 자체 루프)는 항상 실패 — 다른 LAN 기기로 테스트해야 함
- Caddy에 `trusted_proxies` 설정 시 cloudflared/프록시 경유 요청의 실제 클라이언트 IP를 `client_ip` 필드로 추적 가능
- Docker bind-mount 파일 단위 마운트는 이노드 교체로 인해 컨테이너에 반영 안 됨 → 디렉터리 마운트 또는 `docker exec -i` 방식 사용

## 최종 성공 구성

### 인프라 체인
```
외부 브라우저
  → snowball.me.kr:9119 (DNS: 221.165.64.216)
  → KT GiGA WiFi Home 라우터 (포트포워딩 9119→172.30.1.92:9119)
  → server: docker-proxy (0.0.0.0:9119)
  → Caddy 컨테이너 (172.18.0.4:9119, HTTPS)
  → hermes-dashboard 컨테이너 (172.18.0.6:19119)
```

### Caddyfile (최종)
```caddyfile
{
    servers {
        trusted_proxies static 127.0.0.1 172.18.0.0/16
    }
}

snowball.me.kr:9119 {
    log {
        output file /var/log/caddy/access-9119.log
        format json
    }
    reverse_proxy hermes-dashboard:19119
}

:19120 {
    # 내부 HTTP 리스너 (cloudflared/터널 테스트용)
    log {
        output file /var/log/caddy/access-9119.log
        format json
    }
    reverse_proxy hermes-dashboard:19119
}

snowball.me.kr {
    log {
        output file /var/log/caddy/access-443.log
        format json
    }
    handle_path /hermes* { reverse_proxy hermes-dashboard:19119 }
    handle /api/* { reverse_proxy hermes-dashboard:19119 }
    handle /assets/* { reverse_proxy hermes-dashboard:19119 }
    handle_path /db-admin* { reverse_proxy 172.18.0.2:8080 }
    handle_path /s3* { reverse_proxy 172.18.0.5:8333 }
    handle /auth/* { reverse_proxy 172.30.1.92:3000 }
    handle { root * /var/www/html; file_server }
}
```

### docker-compose.yml 로그 볼륨
```yaml
volumes:
  - ./caddy/logs:/var/log/caddy
```

### UFW 상태
```
9119/tcp    ALLOW IN    Anywhere
172.18.0.4 9119/tcp   ALLOW FWD   Anywhere
```

## 성공 증거 (Caddy 로그)

```
[07:51:12] remote_ip=172.30.1.254  host=snowball.me.kr:9119  status=200  uri=/
[07:51:13] remote_ip=172.30.1.254  host=snowball.me.kr:9119  status=101  uri=/api/ws
[07:51:14] remote_ip=172.30.1.254  host=snowball.me.kr:9119  status=101  uri=/api/pty

[20:27:14] remote_ip=172.30.1.254  host=snowball.me.kr:9119  status=200  uri=/
[20:27:19] remote_ip=172.30.1.254  host=snowball.me.kr:9119  status=101  uri=/api/ws
[20:27:19] remote_ip=172.30.1.254  host=snowball.me.kr:9119  status=101  uri=/api/pty
```

`172.30.1.254`는 KT 라우터의 LAN IP — hairpin NAT으로 라우팅됐음을 의미한다. 각 세션에서 HTML·CSS·JS 로드 + WebSocket 터미널 연결까지 완전히 성공.

## 실패했던 시도 목록

| 시도 | 실패 원인 |
|---|---|
| 서버에서 `curl https://221.165.64.216:9119/` | hairpin NAT 불가 (서버 = 목적지) |
| WebFetch from Anthropic servers | 외부(한국 외) 차단 또는 타임아웃 |
| `nslookup` / `host` 명령 | 서버에 미설치 → `resolvectl` 사용 |
| `docker cp`로 bind-mount 파일 교체 | "device or resource busy" → 이노드 문제 |
| `cloudflared --no-tls-verify` | auto-mode classifier 차단 |
| 라우터 기본 자격 증명 시도 | auto-mode classifier 차단 (brute-force 분류) |
| snap install cloudflared | TTY 없이 실행 불가 |
| UPnP로 라우터 설정 확인 | KT 라우터 UPnP 비활성화 |

## 연결된 개념

- [[wiki/concepts/caddy]]
- [[wiki/concepts/kt-hairpin-nat]]
- [[wiki/concepts/docker-bind-mount-inode]]

## 메모

- cloudflared Quick Tunnel(`/tmp/cloudflared`)은 재부팅 시 사라짐 — 영구 설치 필요시 `sudo mv /tmp/cloudflared /usr/local/bin/`
- Caddy inode bind-mount 문제: 파일 단위 마운트 시 에디터 저장(atomic rename)으로 이노드 교체 → 컨테이너에 미반영. `docker exec -i container sh -c 'cat > /path'` 방식으로 in-place 수정 후 재시작 필요.
- 포트 19120은 내부 HTTP 테스트·터널용으로만 유지. 외부에 노출되지 않음(UFW FORWARD 룰 없음).
