---
title: AI 에이전트 워크플로우
type: concept
tags: [ai, claude-code, productivity, workflow]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-claude-code-beginner-install-guide, 2026-06-05-how-claude-code-works, 2026-06-05-claude-code-7steps-mastery]
summary: "명확한 지시와 검증 가능한 데이터로 AI 에이전트의 반복 작업 자동화, 초기 설정 투자로 메인 및 목적별 서브에이전트 팀 병렬 운영 시스템."
---

## 정의

AI 에이전트(Claude Code 등)를 활용해 반복 작업을 자동화하는 작업 흐름. 한 번 시스템을 구축해두면 이후 동일한 작업을 빠르게 반복 실행할 수 있다.

## 핵심 원칙

### 1. 검증 가능한 데이터 제공
AI에게 명확한 기준이 있는 데이터를 주면 출력 품질이 올라간다.
- 나쁜 예: "블로그 글 써줘"
- 좋은 예: "이 샘플 텍스트를 분석해서 합쇼체 95%, 영어 0%, 볼드체 포함한 블로그 글 작성"

### 2. 명확한 지시 (CLAUDE.md 활용)
반복되는 규칙과 컨텍스트는 CLAUDE.md에 저장. 매 세션마다 다시 설명하지 않아도 된다.

### 3. 시스템 구축 후 반복
초기 설정(주방)에 투자하면 이후 실행(요리) 비용이 낮아진다.

## 주방/셰프 비유

| 비유 | 실제 의미 |
|------|-----------|
| 주방 | IDE / 개발 환경 |
| 셰프 | Claude Code, Gemini 등 AI |
| 레시피 | CLAUDE.md, 프롬프트 |
| 요리 결과물 | AI 아웃풋 |

하나의 주방(IDE)에서 여러 셰프(AI)를 동시에 쓸 수 있다.

## 서브에이전트 운영

메인 AI 하나만 쓰는 것이 아니라 목적별 에이전트(임원)를 팀으로 구성:
- 메인 AI가 명령을 받으면 적합한 서브에이전트에게 위임
- 에이전트 수보다 목적 명확성·결과값 품질이 중요
- 실사례: CCO(콘텐츠), CMO(마케팅) 등 업무별 에이전트를 연결해 병렬 수행
- 참고 수치: Claude Code 창시자 5개, 해커톤 우승자 13개

## 관련 개념

- [[wiki/concepts/agentic-loop|에이전트 루프]] — 워크플로우의 실행 메커니즘
- [[wiki/concepts/claude-md|CLAUDE.md]] — 워크플로우 지시를 저장하는 파일
- [[wiki/concepts/claude-code-commands-skills|커맨드 & 스킬스]] — 워크플로우 재사용 단위
- [[wiki/concepts/mcp|MCP]] — 외부 도구 연결로 워크플로우 확장
- [[wiki/concepts/hooks|훅스]] — 자동 실행 트리거
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 이 위키 자체가 AI 에이전트 워크플로우의 실사례

## 관련 엔티티

- [[wiki/entities/claude-code|Claude Code]]

## 출처

- [[wiki/sources/2026-06-05-claude-code-beginner-install-guide]]
- [[wiki/sources/2026-06-05-how-claude-code-works]]
- [[wiki/sources/2026-06-05-claude-code-7steps-mastery]]
