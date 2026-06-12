---
title: KT hairpin NAT (NAT Loopback)
type: concept
tags: [network, nat, router, kt, port-forwarding]
created: 2026-06-12
updated: 2026-06-12
sources: [2026-06-12-hermes-external-access]
---

## 정의

**hairpin NAT** (NAT loopback)은 같은 LAN 안의 기기가 외부 도메인(또는 공인 IP)을 통해 같은 LAN의 서버에 접속할 때, 라우터가 이를 내부 IP로 올바르게 포워딩하는 기능이다.

일반 NAT과의 차이:
- **일반 NAT**: 외부 클라이언트 → 공인IP:PORT → 라우터 → 내부서버
- **hairpin NAT**: 내부 클라이언트 → 공인IP:PORT → **라우터(hairpin)** → 내부서버

## KT GiGA WiFi Home에서의 동작

KT GiGA WiFi Home 라우터는 **포트 9119에서 hairpin NAT을 지원**한다.

```
LAN 기기(예: 172.30.1.50)
  → snowball.me.kr:9119 (DNS: 221.165.64.216)
  → 패킷이 라우터 WAN 인터페이스에 도달
  → 라우터: DNAT 221.165.64.216:9119 → 172.30.1.92:9119
  → 라우터: SNAT source → 172.30.1.254 (라우터 자신의 LAN IP)
  → 서버(172.30.1.92)에서 remote_ip=172.30.1.254 로 수신
```

## 진단 방법

Caddy access 로그에서 `remote_ip: 172.30.1.254` 가 나타나면 hairpin NAT 경유 성공을 의미한다.

```json
{
  "remote_ip": "172.30.1.254",
  "client_ip": "172.30.1.254",
  "status": 200,
  "host": "snowball.me.kr:9119"
}
```

`172.30.1.254`는 KT 라우터의 LAN IP다.

## 중요한 테스트 제한사항

**서버 자체에서 공인IP 접속 테스트는 항상 실패한다.**

```bash
# ❌ 이 테스트는 항상 실패 (서버가 자신의 외부 IP로 접속)
curl https://221.165.64.216:9119/    # → timeout
curl https://snowball.me.kr:9119/    # → timeout
```

서버(172.30.1.92)가 자기 자신의 외부 IP(221.165.64.216)로 패킷을 보내면:
1. 패킷이 라우터의 WAN 인터페이스로 나감
2. 라우터는 이것을 "외부에서 들어오는 hairpin" 패킷으로 처리하지 않음
3. 서버에서 직접 나가는 패킷은 hairpin NAT 대상이 아님

**올바른 테스트**: 노트북, 스마트폰 등 **서버가 아닌 다른 LAN 기기**에서 테스트.

## 포트별 차이

KT 라우터는 모든 포트에 hairpin NAT을 지원하지 않을 수 있다. 확인된 동작:
- **포트 9119**: hairpin NAT 지원 ✅
- **포트 80/443**: KT 가정용 ISP가 인바운드 차단 가능성 (확인 필요)

## 관련 개념

- [[wiki/concepts/caddy]] — Caddy access log에서 remote_ip 확인
- [[wiki/entities/caddy]] — 실제 운용 환경

## 출처

- [[wiki/sources/2026-06-12-hermes-external-access]]
