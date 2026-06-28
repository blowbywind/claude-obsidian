---
title: "쉽게 이해하는 네트워크 및 인프라 구성도 | 바이브 코딩 하는 분들을 꼭 끝까지 보세요"
type: source
origin: https://youtu.be/wqzmZ97vAOY
author: 기술노트with 알렉
date_published: 2026-06-13
tags: [network, infra, tcp-ip, http, routing, firewall, cdn, dmz, load-balancer, web-server, was, database]
created: 2026-06-13
updated: 2026-06-13
summary: "온프레미스 네트워크 인프라 구성도를 IP·TCP·HTTP 프로토콜부터 라우터·방화벽·CDN·DMZ·로드밸런서 장비, 웹서버-WAS-DB 3계층 이중화까지 전체 요청 흐름으로 정리한 기술노트 영상 요약."
---

## 요약

온프레미스 환경에서의 네트워크·인프라 구성도를 단계적으로 설명. 인터넷/웹의 차이에서 출발해 IP·TCP·HTTP 프로토콜, 라우터/스위치/방화벽/CDN/DMZ 장비, 웹서버-WAS-DB 3계층 이중화 구성까지 전체 흐름을 한 구성도로 연결. 다음 영상에서 클라우드 구성 예고.

## 핵심 주장

### 1. 인터넷 vs 웹

| | 정의 |
|--|------|
| **인터넷** | 수많은 컴퓨터가 촘촘히 연결된 그 자체 |
| **웹** | 인터넷 기반으로 동작하는 어플리케이션 (브라우저 + 도메인) |

- 인터넷 = 인프라(연결 자체), 웹 = 인터넷 위에서 동작하는 서비스
- **네트워크** = 이러한 연결을 가능하게 하는 기술 전체

### 2. 핵심 프로토콜 (IP / TCP / HTTP)

**IP (Internet Protocol)**:
- 서버에도 IP가 설정되어 있음
- 클라이언트가 서버를 찾아가는 주소 역할
- 형식: `192.168.0.1` (점(.)으로 구분된 4자리 숫자)

**TCP (Transmission Control Protocol)**:
- 데이터를 작게 나누어 전송 (패킷 단위)
- 수신 측에서 순서 확인, 오류 감지 시 재전송 요청
- 인터넷 경로가 다양하기 때문에 순서 보장이 필요

**HTTP (HyperText Transfer Protocol)**:
- HTML을 주고받는 규약 (약속)
- 클라이언트-서버 간 요청/응답 프로토콜
- HTTPS = HTTP + SSL(암호화), 포트 443 사용

### 3. 네트워크 장비

**라우터**:
- WAN(Wide Area Network, 인터넷 광케이블 망) ↔ LAN(Local Area Network, 사무실/집 내부) 연결
- ISP(인터넷 서비스 제공자) 라우터를 경계로 외부/내부 분리

**스위치**:
- LAN 내부의 컴퓨터·서버들을 연결하는 장비
- 내부 서버 이중화 구성 시 사용 (로드밸런서 역할도 가능)

**방화벽(Firewall)**:
- 허용된 IP 대역·포트만 접속 가능하도록 제어
- 예: HTTPS(443) 허용, FTP(21) 차단
- 외부망→내부망 진입의 첫 번째 관문

**CDN (Content Delivery Network)**:
- 사용자 가까이에 정적 콘텐츠(이미지·영상)를 복제 배치
- 캐시 히트(Cache Hit): CDN에 콘텐츠가 있으면 즉시 응답
- 캐시 미스(Cache Miss): 없으면 오리진 서버에서 가져온 뒤 캐싱
- 미국 서비스 → 한국 CDN 서버 → 한국 사용자에게 빠른 응답

**DMZ (Demilitarized Zone)**:
- 외부 접속을 허용하는 서버를 격리한 구역 (주로 웹서버)
- DB 같은 민감 서버는 DMZ에 두지 않음 (보안)

**로드밸런서**:
- 여러 서버에 트래픽을 분산하는 역할
- 스위치 장비로 구현하거나 소프트웨어 방식으로도 사용

### 4. 포트 (Port)

서버 컴퓨터 내 여러 서버 프로그램을 구분하는 식별 번호.

| 포트 | 서비스 |
|------|--------|
| **80** | HTTP 웹서버 |
| **443** | HTTPS |
| **8080** | WAS (Web Application Server, 기본값) |
| **3306** | MySQL DB |
| **22** | SSH |
| **21** | FTP (보통 방화벽에서 차단) |

- 동일한 서버 컴퓨터에 웹서버·WAS·DB가 모두 실행될 수 있음
- 포트 번호로 어떤 프로그램에 요청하는지 구분

### 5. 서버 계층 — 웹서버 vs WAS vs DB

**웹서버 (Web Server)**:
- 이미지·HTML 등 정적 콘텐츠 제공
- 리버스 프록시 역할: WAS로 트래픽 전달
- 대표 소프트웨어: **Nginx** (정적 + 리버스 프록시 모두 가능)

**WAS (Web Application Server)**:
- 백엔드 API 어플리케이션 탑재 (Spring Boot, Django, FastAPI 등)
- 비즈니스 로직, CRUD 처리, DB 연동
- 기본 포트: 8080

**DB (Database)**:
- WAS에서만 접속 (외부 직접 접속 차단)
- 내부망(Internal Network)에 위치

### 6. 인프라 이중화

**웹서버·WAS 이중화**:
```
로드밸런서
 ├─ 웹서버1 ─┬─ WAS1
 │           └─ WAS2
 └─ 웹서버2 ─┬─ WAS1
              └─ WAS2
```
- 목적: 부하 분산(Load Balancing) + 장애 시 서비스 연속성

**DB 이중화 — Primary + Standby**:
```
WAS1 ─┐
      ├→ Primary DB ──(복제)──→ Standby DB
WAS2 ─┘
```
- 모든 쓰기/읽기는 Primary DB만 사용
- Standby는 리플리케이션(복제)으로 데이터 동기화 대기
- Primary 장애 시 → Standby가 Primary로 승격
- 양쪽에 동시 쓰기 하지 않는 이유: **데이터 동기화 충돌** 방지

### 7. 전체 구성도 흐름

```
클라이언트(브라우저)
  ↓ 도메인 입력 → DNS → IP 확인
[CDN] → 캐시 히트 시 즉시 응답, 미스 시 아래로
  ↓
[인터넷 (WAN)] — 다양한 경로의 그물망
  ↓
[ISP 라우터] — WAN↔LAN 연결
  ↓
[방화벽] — 443/80 등 허용 포트만 통과
  ↓
[로드밸런서/스위치] — 트래픽 분산
  ↓
[DMZ 구간]
  [웹서버1·웹서버2] (포트 443/80, Nginx) — 리버스 프록시
  ↓
[내부망 (Internal Network)]
  [WAS1·WAS2] (포트 8080) — API 서버
  ↓
  [Primary DB] ←리플리케이션→ [Standby DB] (포트 3306)
```

## 연결된 개념

- [[wiki/concepts/network-infra|네트워크 & 인프라 구성]] — 이 영상의 핵심 구조 정리
- [[wiki/concepts/it-knowledge-map|IT 기술 지식 맵]] — 네트워크 계층을 포함한 전체 CS 지도
- [[wiki/concepts/service-dev-lifecycle|서비스 개발 라이프사이클]] — 배포·출시 단계와 연결 (도메인·HTTPS)

## 연결된 엔티티

- [[wiki/entities/gisulnote-alex|기술노트with 알렉]] — 제작 채널

## 메모

- 기술노트 알렉 시리즈 6편 (IT 지식맵 → 빅데이터 → 컴퓨터구조 1·2부 → 서비스 개발 → 네트워크·인프라)
- **온프레미스** 기준 설명; 클라우드 구성은 다음 영상에서 예고
- WAS 기본 포트 8080이 Tomcat(Java)·uvicorn(Python) 등의 관례이므로 실제 설정에 따라 다를 수 있음
- DMZ 구성은 규모·보안 정책에 따라 생략되기도 함 (소규모 서비스는 단순화)
