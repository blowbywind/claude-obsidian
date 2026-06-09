---
title: AI 네이티브 팀 구성
type: concept
tags: [multi-agent, ai-native, team]
created: 2026-06-09
updated: 2026-06-09
sources: [2026-06-09-ai-native-hermes-report]
---

## 정의
인간 1명이 AI 에이전트만으로 구성된 팀을 운영하는 구조. 역할별 에이전트를 분리하고, 플랫폼 특성에 따라 담당 업무를 나누는 것이 핵심.

## 상세

### 역할 분리 원칙
- **헤르메스 에이전트** = 에이전시 (야간·모바일·크론잡)
- **Claude Code** = 인하우스 (주간·터미널·기획·개발)
- 분리 이유: 주간 업무 중 헤르메스 에이전트와 혼선 방지

### 김요일의 팀 구성 예시 (10명)

| 에이전트 | 플랫폼 | 역할 |
|---|---|---|
| 효율이 (효1) | 헤르메스 | 개발 + 취합·보고 (오른팔, 모더레이터) |
| 효리 (효2) | 헤르메스 | 디자인 (웹·앱 UI, PPT) |
| 효삼이 (효3) | 헤르메스 | 자동화 + 개발 검증 (Claude Code 연결) |
| 효나 (효4) | 헤르메스 | 콘텐츠 생성 (이미지·영상·SNS) |
| 효정이 (효5) | 헤르메스 | 강의 보조·리서치·일정 관리 |
| 시원 (C1) | Claude Code | 오케스트레이터 — 업무 지시 후 최종 보고 |
| C2–C5 | Claude Code | 기획·스킬 제작·연결 |

### 맥락 공유 방식
- 10개 에이전트가 **같은 옵시디언 위키 공유** → 맥락 즉시 연결
- **Session Send = Claude Code Agent Teams** (v2.1.80+): 오케스트레이터(C1)가 팀원 에이전트에 지시 → 공유 파일 기반 통신 → 최종 결과 인간에게 보고
- 도구 종속성 제거: Codex든 Claude Code든 Gemini든 위키만 있으면 맥락 즉시 연결

### 팀 명칭 (김요일 사례)
- 헤르메스 에이전트 팀: **린네이티브(Lean Native)**
- Claude Code 에이전트 팀: **린 프로젝트**

## 관련 개념
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]] — 야간에 헤르메스 에이전트 자율 학습
- [[wiki/concepts/context-intelligence|컨텍스트 인텔리전스]] — 옵시디언 위키로 팀 전체 맥락 공유
- [[wiki/concepts/ai-orchestrator-mindset|AI 오케스트레이터 마인드셋]] — 위임·조율 역할

## 관련 엔티티
- [[wiki/entities/hermes-agent|헤르메스 에이전트]]
- [[wiki/entities/kimyoil|김요일]]
- [[wiki/entities/claude-code|Claude Code]]

## 출처
- [[wiki/sources/2026-06-09-ai-native-hermes-report]]
