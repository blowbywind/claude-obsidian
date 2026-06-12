---
title: IT 기술 지식 맵 (비전공자·바이브코더용)
type: concept
tags: [it-fundamentals, software-architecture, network, cloud, vibe-coding, cs]
created: 2026-06-13
updated: 2026-06-13
sources: [2026-06-13-it-knowledge-map-gisulnote]
---

## 정의

CS 전공자가 체계적으로 배우는 지식 영역 전체를 연결하여 이해하는 멘탈 모델. 소프트웨어 개발 → 언어/프레임워크 → 컴퓨터 구조 → 네트워크 → 아키텍처 → 클라우드 순서로 상위 개념에서 하위 구현으로 내려가는 구조.

## 전체 계층 구조

```
[소프트웨어 개발]
  앱 종류 (웹/앱/하이브리드)
  프론트엔드 ↔ 백엔드
        ↓
[언어 & 프레임워크]
  언어: C, Java, JS, Python
  프레임워크: React, Spring Boot, Node.js, FastAPI
        ↓
[소프트웨어 공학]
  방법론: 폭포수 → 애자일/DevOps
        ↓
[컴퓨터 구조]
  프로그램 → 프로세스 → CPU → OS
        ↓
[네트워크]
  HTTP/HTTPS, IP, 라우터/스위치
        ↓
[아키텍처]
  3-tier, MSA
        ↓
[클라우드 & 컨테이너]
  가상화 → VM → Docker → Kubernetes
        ↓
[빅데이터 & AI]
  데이터 파이프라인, 분석, 모델 서빙
```

## 핵심 구분: 언어 vs 프레임워크

| 구분 | 설명 | 예시 |
|------|------|------|
| **언어** | 문법을 가진 개발 도구 | C, Java, JavaScript, Python |
| **프레임워크** | 언어 기반의 개발 틀 (미리 만들어진 구조) | React, Spring Boot, Node.js, FastAPI |

Java ≠ JavaScript (이름만 비슷, 완전히 별개 언어)

## 프론트엔드 vs 백엔드

- **프론트엔드**: 사용자가 보는 화면. HTML + CSS + JS, React
- **백엔드**: 서버 로직 + 데이터베이스. Java/Spring, Python/FastAPI
- **통신**: HTTP/HTTPS 프로토콜로 연결

## 컴퓨터 구조 계층

```
프로그램(언어로 만든 결과물)
  → 프로세스(실행 상태)
  → CPU(처리)
  → OS(관리, 소프트웨어)
  → 하드웨어
```

## 소프트웨어 개발 방법론

| 방법론 | 특징 | 적합한 상황 |
|--------|------|------------|
| **폭포수** | 기획→설계→개발→테스트 순차 진행, 되돌리기 어려움 | 요구사항이 고정된 납품형 프로젝트 |
| **애자일/DevOps** | 반복적 개선, 빠른 피드백 | 지속 서비스, 스타트업 |

## 클라우드 핵심: 가상화

```
물리 서버
  └─ VM (가상머신, OS 포함, 무거움)
       └─ 컨테이너 (OS 경량화, Docker)
            └─ 오케스트레이션 (Kubernetes)
```

AWS EC2 = IaaS (Infrastructure as a Service) — 가상화로 5분 내 서버 생성 가능

## 바이브코딩과의 연관

AI 코딩 도구로 코드를 생성하더라도 이 지식 맵의 흐름을 이해하면:
- 어떤 영역의 코드를 생성하는지 파악
- 에러 발생 시 원인 레이어 추정
- 아키텍처 결정 시 적절한 판단

## 관련 개념

- [[wiki/concepts/bigdata-pipeline|빅데이터 분석 파이프라인]] — 이 맵의 최상단(빅데이터·AI) 영역
- [[wiki/concepts/hermes-architecture|Hermes 아키텍처]] — 실제 서비스 아키텍처 사례

## 관련 엔티티

- [[wiki/entities/gisulnote-alex|기술노트with 알렉]] — 이 개념을 소개한 채널

## 출처

- [[wiki/sources/2026-06-13-it-knowledge-map-gisulnote]]
