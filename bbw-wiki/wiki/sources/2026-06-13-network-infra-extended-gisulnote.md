---
title: "[확장판] 네트워크 기초 + OSI 7 Layer, TCP/IP 4계층, L4 L7 스위치, SSL 종료 지점"
type: source
origin: https://youtu.be/Q5xY0tn9Axg
author: 기술노트with 알렉
date_published: 2026-06-13
tags: [network, osi-7-layer, tcp-ip, l4-switch, l7-switch, ssl-termination, reverse-proxy]
created: 2026-06-13
updated: 2026-06-13
---

## 요약

[[wiki/sources/2026-06-13-network-infra-gisulnote|네트워크 기초 영상]]의 확장판. 기존 내용(IP·TCP·HTTP·장비·이중화)에 OSI 7 Layer vs TCP/IP 4계층 매핑, L4/L7 스위치 구분, SSL 종료 지점 3가지를 추가.

## 추가된 핵심 내용 (기존 영상 대비 델타)

### 1. OSI 7 Layer vs TCP/IP 4계층

동일한 네트워크 스택을 바라보는 두 가지 관점.

| TCP/IP 4계층 | OSI 7계층 | 주요 프로토콜 |
|-------------|-----------|--------------|
| 응용 계층 | 응용(7)·표현(6)·세션(5) | HTTP, FTP, DNS |
| 전송 계층 | 전송(4) | **TCP**, UDP |
| 인터넷 계층 | 네트워크(3) | **IP** |
| 물리/링크 계층 | 데이터링크(2)·물리(1) | 이더넷, Wi-Fi |

- OSI 7 Layer = TCP/IP 4계층을 더 세분화한 것 (실무는 4계층 기준)
- **L4** = 전송 계층(TCP), **L7** = 응용 계층(HTTP)

**데이터 흐름 (클라이언트→서버)**:
```
브라우저(HTTP) → TCP → IP → 이더넷(물리)
                                  ↓ 인터넷 경유
                             서버 이더넷 → IP → TCP → HTTP 서버
```

### 2. L4 스위치 vs L7 스위치

| 구분 | 동작 계층 | 분기 기준 | 특징 |
|------|----------|----------|------|
| **L4 스위치** | TCP(4계층) | IP + 포트 | 단순 부하 분산, 빠름 |
| **L7 스위치** | HTTP(7계층) | URL, 쿠키, 헤더 등 | 콘텐츠 기반 분기, 세밀한 제어 |

- 로드밸런서는 L4 또는 L7 방식 중 선택
- 실무에서는 Nginx(L7)가 리버스 프록시 + 로드밸런서 역할을 함께 담당

### 3. SSL 종료 지점 (SSL Termination)

```
클라이언트 ─HTTPS(443)─▶ [웹서버/리버스프록시] ─HTTP(8080)─▶ WAS
                           ← SSL 종료 지점 →
```

- **HTTPS** = HTTP + SSL(암호화 레이어)
- 웹서버(Nginx)에서 SSL 인증서를 처리한 뒤, 내부 WAS와는 **HTTP**로 통신
- **이유**:
  1. 내부망은 외부 위협이 없으므로 암호화 불필요
  2. 모든 구간에 HTTPS 적용 시 인증서 관리·처리 오버헤드 증가
- "SSL이 종료된다" = HTTPS가 웹서버에서 끊기고 HTTP로 전환됨을 의미

## 연결된 개념

- [[wiki/concepts/network-infra|네트워크 & 인프라 구성]] — 기본 구성도 (이 영상으로 OSI·L4/L7·SSL 종료 추가)
- [[wiki/sources/2026-06-13-network-infra-gisulnote]] — 기본 편 (중복 내용은 여기 참조)

## 연결된 엔티티

- [[wiki/entities/gisulnote-alex|기술노트with 알렉]] — 제작 채널
- [[wiki/entities/caddy|Caddy]] — Nginx 대신 SSL 종료·리버스프록시 역할 담당 가능 (bbw 운용 중)

## 메모

- 기술노트 알렉 시리즈 7편 (네트워크 기초 확장판)
- 기존 네트워크 영상 내용을 90% 이상 반복하며 OSI·L4/L7·SSL 3가지를 추가
- 다음 영상: 클라우드 네트워크 구성 예고
