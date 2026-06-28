---
title: "How I Use Obsidian + Claude Cowork to Run My Life"
type: source
tags: [obsidian, claude, ai-os, pkm, cowork, nick-milo]
created: 2026-06-07
updated: 2026-06-07
origin: https://youtu.be/rRa9td4oe7k
author: Nick Milo
date_published: 2026-06
summary: "Nick Milo이 Obsidian+Claude Cowork를 AI OS 3레이어(볼트·번역층·외부AI)로 구성하고 ME.MD·Vault Map·스킬을 로컬에 보존해 AI 교체 가능한 개인 운영체제를 구축하는 방법을"
summary: "Nick Milo이 Obsidian·Claude Cowork를 결합한 AI OS 3레이어(Ideaverse→번역층→AI) 구조와 ME.MD·Vault Map·Skill Map으로 AI 종속 없이 이식 가능한 개인 지"
---

## 요약

Nick Milo이 Obsidian + Claude Cowork를 결합한 **AI OS (AI 운영체제)** 개념과 실제 구축 방법을 설명한다. 핵심은 AI를 언제든 교체 가능한 레이어로 두고, 자신의 노트와 스킬은 AI-agnostic한 형태로 로컬에 보존하는 것이다. 번역층(AIOS 폴더)이 Obsidian 볼트와 외부 AI 사이의 다리 역할을 한다.

## 핵심 주장

- **AI OS 3레이어**: Ideaverse(내 생각) → Maps/Manuals(번역층) → Claude Cowork(외부 AI)
- **이식성 원칙**: Claude가 사라져도 파일·스킬·AI 코어 문서가 어떤 AI에서도 작동해야 한다
- **번역층 3대 파일**: ME.MD(포터블 아이덴티티) + Vault Map(볼트 탐색 가이드) + Skill Map(스킬 목록)
- **스킬은 로컬에**: 스킬을 Claude 내부가 아닌 자신의 Obsidian에 저장해야 AI 종속에서 벗어난다
- **세션 시작 프롬프트**: 매 세션 ME.MD·Vault Map·Skill Map 읽기를 명시적으로 지시해야 AI 기억상실을 보완한다

## 구조 상세

### AIOS 폴더 구성
Ideaverse 안에 별도 폴더(`AIOS/`)를 만들어 AI 생성 콘텐츠를 격리:
- `ME.MD` — 내가 누구인지, 어떻게 생각하는지, AI와 어떻게 협업할지 정의
- `Vault Map` — AI가 볼트의 어느 노트로 이동해야 하는지 TOC+매뉴얼
- `Skill Map` — 어떤 스킬이 존재하고 언제 써야 하는지 목록

### Claude Cowork 모델 선택 전략
- **Sonnet** (기본): 대부분의 작업에 충분, 토큰 효율적
- **Opus**: 복잡한 합성·심층 리서치·품질이 중요한 작업
- **Haiku**: Web Clipper 요약 등 초경량 작업에만 사용

### 7가지 스킬 시스템
| 시스템 | 역할 |
|--------|------|
| Daily Trident | 아침 브리핑(Daily Brief) + 하루 중 인터스티셜 저널(Daily Log) |
| Sherpa | 새 주제 학습 가속 — 토픽 맵핑 |
| Weekly Review | 한 주 리뷰 보조 렌즈 |
| Rock Tumbler | IDI 프레임워크(Imagine·Discern·Integrate) 기반 작업 피드백 |
| Chronicler | AI 대화·아이디어를 verbatim 저장, 요약본 생성 |
| Janitor | AI OS 시스템 자가 유지·정비 |
| Courier | 개인 볼트 → 팀 공유 공간으로 sanitize하여 전달 |

## 연결된 개념

- [[wiki/concepts/ai-os|AI OS]] — 이 영상의 핵심 프레임워크
- [[wiki/concepts/me-md|ME.MD]] — AI 포터블 아이덴티티
- [[wiki/concepts/ace-folder-framework|ACE 폴더 프레임워크]] — Atlas·Calendar·Efforts 구조
- [[wiki/concepts/vault-map|Vault Map & Skill Map]] — 번역층 핵심 파일
- [[wiki/concepts/second-brain|세컨드 브레인]] — 상위 개념
- [[wiki/concepts/claude-md|CLAUDE.md]] — ME.MD의 Claude 전용 버전

## 연결된 엔티티

- [[wiki/entities/nick-milo|Nick Milo]] — 영상 저자
- [[wiki/entities/obsidian|Obsidian]] — Ideaverse 호스팅 앱
- [[wiki/entities/cowork|Cowork]] — Claude 데스크탑 앱의 파일 접근 모드

## 메모

- "Claude Co-work"는 Claude 데스크탑 앱의 3가지 모드 중 중간 모드(파일 시스템 접근)
- Claude 데이터 정책: 학습에 미사용, 서버 30일 롤링 보존
- Nick Milo은 약 17,000개 노트 보유 — 지도 없이 AI를 볼트에 연결하면 탐색 불가
- Daily Brief는 Gmail·Calendar·ClickUp·Ideaverse 4개 소스를 통합해 매일 06:00 자동 생성
