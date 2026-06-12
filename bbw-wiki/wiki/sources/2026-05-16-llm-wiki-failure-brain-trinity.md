---
title: "LLM Wiki가 망하는 진짜 이유: Obsidian·Claude Code보다 중요한 AI OS 설계"
type: source
tags: [llm-wiki, ai-os, brain-trinity, pkm, second-brain, purpose-driven]
created: 2026-06-12
updated: 2026-06-12
origin: https://youtu.be/GQtty9JOAUU
author: 브라이언 (Brain's Brain Trinity)
date_published: 2026-05-16
---

## 요약

Brain Trinity 채널 브라이언이 LLM Wiki 실패 패턴을 분석하고, 목적 없이 만든 시스템은 한두 달 안에 방치된다고 경고한다. LLM Wiki는 전체 AI OS의 작은 부품일 뿐이며, 시스템 설계 전에 삶의 철학·역할·목적 계층을 먼저 정립해야 한다는 것이 핵심 메시지. Andrej Karpathy의 LLM Wiki 개념을 Brain Trinity 프레임워크로 확장·재해석한다.

## 핵심 주장

### 1. LLM Wiki 실패의 3가지 원인
- **목적 부재**: 폴더·스키마·스킬은 만들었지만 "내 삶 어디에 끼어드는가"를 고민하지 않음
- **완벽주의**: 모든 과거 문서·템플릿을 유지 관리하려다 지침
- **방법론만 복제**: Karpathy의 gist는 의도적으로 추상적(`"this document is intentionally abstract"`) — 구현법 영상은 많지만 WHY는 없음

### 2. LLM Wiki = 외부 지식의 얕은 컴파일
- raw/ 폴더 원문 → ingest → wiki 정리 구조는 **외부에 있는 남의 지식을 AI가 얕게 프로세싱한 것**
- 장점: 사람이 1만 개 문서를 직접 정리 불가 → AI가 대량·지속 처리
- 한계: 새로운 인사이트는 LLM Wiki 자체에서 나오지 않음 — 결국 남의 글·영상·텍스트

### 3. AI가 대신할 수 없는 인간의 지식 = My Notes
- 내 일기, 판단, 결정, 경험, 기록 → **인간의 고도화된 깊은 이해**
- 암묵지를 형식지로 꺼내 놓은 것 — 내 머릿속의 구조와 지식
- LLM Wiki(얕은 컴파일)와 My Notes(깊은 이해)가 통합될 때 진짜 동료 AI가 됨

### 4. GOLD IN, GOLD OUT 원칙
- **Gold**: 나의 판단·경험·인사이트·관점이 담긴 입력
- **Garbage**: 목적·관점 없이 수집된 데이터 → garbage in, garbage out
- LLM Wiki에 나의 관점 없이 데이터만 쌓으면 갈비지(garbage)

### 5. Brain Trinity 계층 구조 — 목적이 시스템보다 먼저

```
철학 (Philosophy / 북극성 Polaris)
  나는 누구인가, 왜 사는가, 무엇을 중요시하는가
  ↓
삶의 영역 (Life Areas)
  커리어, 재정, 성장, 가족, 관계, 환경
  ↓
역할 (Roles) — 같은 자아의 다른 버전들
  예: AI 컨설턴트 / 크리에이터 / 가장 / 연구자
  ↓
역할별 목표 & 대상 (Goals & Targets)
  가장→가족의 행복·안정 / 크리에이터→구독자 지식 생산성 개선
  ↓
프로젝트 & 태스크 (Actions)
  ↓
지식 (Knowledge: LLM Wiki + My Notes)
```

### 6. AI OS 안에서 LLM Wiki의 위치
- AI OS(워크스페이스 + 워크플로우)에서 LLM Wiki는 **작은 일부분**
- 워크스페이스 = 지식이 심어지고 자라는 영토 (My Notes + LLM Wiki)
- 워크플로우 = 지식이 연결·작업되어 새 가치로 출력되는 공간
- First Brain(인간) + Second Brain(AI): 얕은 이해 + 깊은 이해 → 통합된 증강 이해 → 영상·논문·프레젠테이션 등 산출물

### 7. LLM Wiki를 만들기 전 필수 질문
1. 내 삶의 철학과 북극성은 무엇인가?
2. 내가 수행하는 역할들과 각 역할의 목표는?
3. LLM Wiki가 내 워크플로우 어디에 끼어드는가?
4. My Notes(깊은 이해)와 어떻게 연결할 것인가?

## 연결된 개념

- [[wiki/concepts/brain-trinity|Brain Trinity]] — 이 영상의 핵심 프레임워크
- [[wiki/concepts/ai-os|AI OS]] — 전체 운영 체제 관점 (Nick Milo vs 브라이언 비교)
- [[wiki/concepts/external-knowledge-system|외부 지식 시스템]] — LLM Wiki의 위치
- [[wiki/concepts/me-md|ME.MD]] — My Notes의 AI-agnostic 구현체

## 연결된 엔티티

- [[wiki/entities/brian-brain-trinity|브라이언 (Brain Trinity)]] — 발표자, AI 컨설턴트·크리에이터·연구자 지망
- [[wiki/entities/andrej-karpathy|Andrej Karpathy]] — LLM Wiki 개념 원저자 (의도적 추상 gist)

## 메모

- 브라이언은 본인을 AI 컨설턴트 + 크리에이터 + 가장 + 박사 지원 중 연구자 4역할로 소개
- Nick Milo(AI OS 3레이어)와 브라이언(Brain Trinity 계층)은 관점이 다름: Milo는 도구 아키텍처 중심, 브라이언은 삶의 목적 중심
- Brain Trinity AI OS 다이어그램 다운로드: Google Drive 링크 (영상 고정 댓글)
- 이 영상은 "구현법"이 아닌 "설계 철학" 영상 — 구현 후속편 예고
