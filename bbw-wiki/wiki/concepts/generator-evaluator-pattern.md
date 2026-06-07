---
title: Generator-Evaluator 패턴
type: concept
tags: [multi-agent, evaluation, harness, anthropic]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-harness-engineering-guide]
---

## 정의

코드·콘텐츠를 생성하는 에이전트(Generator)와 결과물을 검증하는 에이전트(Evaluator)를 분리하는 멀티 에이전트 설계 패턴. Anthropic이 GAN(Generative Adversarial Network)에서 영감을 받아 제안했다.

## 상세

### 문제 인식

Anthropic 연구팀이 발견한 핵심 문제: **AI 모델은 자신의 작업을 객관적으로 평가하지 못한다.** 스스로 생성한 결과물을 너무 관대하게 평가하는 경향이 있다.

### 구조

```
[Generator Agent] → 생성(코드, 디자인, 콘텐츠)
        ↓
[Evaluator Agent] → 독립적 평가 기준으로 검증
        ↓
피드백 → Generator가 수정 → 반복
```

Evaluator는 Generator와 완전히 분리된 별도 에이전트로, **더 엄격하게 튜닝**하는 것이 가능하다.

### Anthropic 적용 사례

프론트엔드 디자인 품질 향상에 적용, 4가지 평가 기준 사용:
1. 디자인 품질
2. 독창성
3. UX 완성도
4. 코드 품질

### 하네스 법칙 4

"생성과 평가를 분리하라" — [[bbw-wiki/wiki/concepts/harness-engineering|하네스 엔지니어링]] 7가지 법칙 중 하나로 핵심 원칙으로 자리잡음.

### bbw-wiki와의 관계

현재 bbw의 `~/.claude/CLAUDE.md`에도 품질 게이트로 `code-reviewer → evaluator-strict` 분리 구조가 반영되어 있다.

## 관련 개념

- [[bbw-wiki/wiki/concepts/harness-engineering|하네스 엔지니어링]] — 이 패턴을 법칙 4로 포함
- [[bbw-wiki/wiki/concepts/agentic-loop|에이전트 루프]] — Generator-Evaluator가 동작하는 루프
- [[bbw-wiki/wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — 실전 적용 맥락

## 관련 엔티티

- [[bbw-wiki/wiki/entities/anthropic|Anthropic]] — 패턴 연구·제안

## 출처

- [[bbw-wiki/wiki/sources/2026-06-07-harness-engineering-guide|하네스 엔지니어링 기초 가이드북]]
