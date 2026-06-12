---
title: 네트워크 & 인프라 구성
type: concept
tags: [network, infra, tcp-ip, http, routing, firewall, cdn, load-balancer, web-server, was, database, dmz]
created: 2026-06-13
updated: 2026-06-13
sources: [2026-06-13-network-infra-gisulnote]
---

## 정의

서비스를 외부에 제공하기 위해 컴퓨터·장비·소프트웨어를 연결하는 체계. 인터넷 통신 프로토콜(IP·TCP·HTTP)부터 방화벽·CDN·웹서버·WAS·DB에 이르는 전체 흐름을 다룬다.

## 인터넷 · 웹 · 네트워크 구분

| 용어 | 정의 |
|------|------|
| **인터넷** | 수많은 컴퓨터가 촘촘히 연결된 인프라 그 자체 |
| **웹** | 인터넷 위에서 브라우저로 동작하는 어플리케이션 |
| **네트워크** | 컴퓨터 간 연결을 가능하게 하는 기술 전체 |

## 핵심 프로토콜

**IP (Internet Protocol)**: 서버 주소 체계. 패킷이 목적지 서버를 찾아가는 근거.

**TCP (Transmission Control Protocol)**:
- 데이터를 패킷 단위로 분할해 전송
- 수신 측이 순서·오류를 확인 후 재전송 요청
- IP 위에서 신뢰성 있는 전송을 보장

**HTTP/HTTPS**:
- HTML·데이터를 주고받는 클라이언트-서버 약속
- HTTPS = HTTP + SSL 암호화, 포트 443

## 네트워크 장비

```
인터넷(WAN) ←[라우터]→ 내부망(LAN)
                           ↓
                       [스위치] — 내부 서버 연결
                           ↓
                       [방화벽] — IP·포트 필터링
```

| 장비 | 역할 |
|------|------|
| **라우터** | WAN ↔ LAN 연결; ISP 라우터가 경계 |
| **스위치** | LAN 내 서버·기기 연결 |
| **방화벽** | 허용 포트(443, 80 등)만 통과, 나머지 차단 |
| **CDN** | 이미지·영상을 사용자 가까이 복제 배치해 빠른 응답 |
| **로드밸런서** | 여러 서버에 트래픽 분산 |
| **DMZ** | 외부 접속 허용 구역(웹서버); DB는 제외 |

**CDN 캐시 로직**:
```
요청 → CDN 캐시 확인
  ├─ 캐시 히트: 즉시 응답 (오리진 서버 불필요)
  └─ 캐시 미스: 오리진 서버에서 가져온 후 캐싱
```

## 포트 번호

| 포트 | 서비스 |
|------|--------|
| 80 | HTTP |
| **443** | HTTPS |
| **8080** | WAS 기본값 |
| **3306** | MySQL |
| 22 | SSH |
| 21 | FTP (보통 방화벽 차단) |

## 서버 3계층 구조

```
[웹서버(Nginx)] — 정적 콘텐츠 + 리버스 프록시  (포트 443/80)
      ↓
[WAS]           — 백엔드 API, 비즈니스 로직      (포트 8080)
      ↓
[DB]            — 데이터 영구 저장                (포트 3306)
```

- **웹서버**: 이미지·HTML 정적 응답 또는 WAS로 요청 전달 (Nginx)
- **WAS**: Spring Boot / Django / FastAPI 등 API 어플리케이션 실행
- **DB**: 내부망에서만 접근 가능

## 이중화 (High Availability)

**목적**: 부하 분산 + 장애 시 서비스 연속성

**웹서버·WAS 이중화**:
```
로드밸런서
 ├─ 웹서버1 ─→ WAS1, WAS2
 └─ 웹서버2 ─→ WAS1, WAS2
```

**DB 이중화 — Primary/Standby**:
```
WAS → Primary DB ─(리플리케이션)─→ Standby DB
```
- 쓰기/읽기는 Primary 하나만 담당 (동시 쓰기 시 동기화 충돌 위험)
- Primary 장애 → Standby 자동 승격
- Standby는 복제 대기 상태

## 전체 요청 흐름 (온프레미스)

```
클라이언트
  → CDN (캐시 히트 시 종료)
  → 인터넷 (WAN, 그물망 라우팅)
  → ISP 라우터
  → 방화벽 (포트 443 허용)
  → 로드밸런서
  → DMZ: 웹서버 (Nginx, 443)
  → 내부망: WAS (8080)
  → DB (3306)
```

## 관련 개념

- [[wiki/concepts/it-knowledge-map|IT 기술 지식 맵]] — 네트워크를 포함한 CS 전체 지도
- [[wiki/concepts/service-dev-lifecycle|서비스 개발 라이프사이클]] — 배포 단계에서 이 구성도 사용 (도메인·HTTPS)
- [[wiki/concepts/computer-architecture-os|컴퓨터 구조 & 운영체제]] — 포트·프로세스 기반 지식

## 관련 엔티티

- [[wiki/entities/caddy|Caddy]] — 웹서버·리버스 프록시 (Nginx 대안, bbw 운용 중)
- [[wiki/entities/gisulnote-alex|기술노트with 알렉]] — 이 개념을 소개한 채널

## 출처

- [[wiki/sources/2026-06-13-network-infra-gisulnote]]
