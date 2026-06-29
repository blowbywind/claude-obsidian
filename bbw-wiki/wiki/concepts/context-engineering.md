---
title: 컨텍스트 엔지니어링 (Context Engineering)
type: concept
tags: [context-engineering, rag, mcp, memory, ai-agent]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-harness-engineering-guide]
summary: "프롬프트 엔지니어링 대신 RAG, MCP, 메모리, 도구로 문맥 전체를 설계하여 모델의 정보기반 의사결정을 구현하는 기술."
---

## 정의

단일 프롬프트 최적화를 넘어, 모델이 정보에 기반한 결정을 내릴 수 있도록 문맥(Context) 전체를 설계하는 기술. Andrej Karpathy가 2025년에 언급하며 널리 알려진 개념이다.

> "프롬프트 엔지니어링은 어떻게 물어볼지(what to ask), 컨텍스트 엔지니어링은 무엇을 보낼지(what to send), 하네스 엔지니어링은 전체가 어떻게 작동하는지(how it operates)에 대한 것이다." — Louis Bouchard

## 상세

### 프롬프트 엔지니어링과의 차이

- 프롬프트 엔지니어링: 한 번의 질문을 최적화 (입력 중심)
- 컨텍스트 엔지니어링: 에이전트가 접근하는 정보 전체를 설계 (시스템 중심)

### 핵심 기술

- **RAG**: 외부 문서 검색 + 모델 결합으로 최신·전문 정보 제공
- **MCP**: 외부 서비스와 모델을 연결하는 표준 프로토콜
- **메모리 시스템**: 대화 간 문맥 유지 (CLAUDE.md, claude-progress.txt 등)
- **Tool 사용**: 모델이 외부 도구를 직접 호출

### 한계

컨텍스트를 잘 구성해도 에이전트가 장기간 안정적으로 작동하는 것을 보장하기 어렵다. 이 한계를 극복하기 위해 [[wiki/concepts/harness-engineering|하네스 엔지니어링]]이 등장했다.

### OpenAI의 핵심 통찰

> "에이전트 관점에서, 인컨텍스트(in-context)로 접근할 수 없는 정보는 존재하지 않는 것과 같다. Slack 대화, 구글 문서, 사람들의 머릿속에만 있는 정보는 에이전트가 접근할 수 없다." — OpenAI

## 관련 개념

- [[wiki/concepts/harness-engineering|하네스 엔지니어링]] — 컨텍스트 엔지니어링의 다음 단계
- [[wiki/concepts/rag|RAG]] — 컨텍스트 엔지니어링의 핵심 기법
- [[wiki/concepts/mcp|MCP]] — 외부 서비스 컨텍스트 연결 표준
- [[wiki/concepts/context-window|컨텍스트 윈도우]] — 컨텍스트가 담기는 공간
- [[wiki/concepts/claude-md|CLAUDE.md]] — 프로젝트 컨텍스트 파일

## 에이전트 프로덕티비티와의 연결 (2026)

하재상(실밸개발자)은 컨텍스트 엔지니어링을 **에이전트 생산성의 가장 본질적인 요소**로 강조한다:

> "같은 모델, 같은 도구, 같은 프롬프트라도 컨텍스트가 어떻게 정리되어 있냐에 따라 결과가 완전히 달라진다."

- 모델은 점점 좋아지고, 하네스도 좋아진다
- 결국 사람이 설계해야 하는 것은 **어떤 정보를 에이전트에게, 언제, 얼마나** 주느냐
- 이를 체계화한 것이 [[wiki/concepts/context-intelligence|컨텍스트 인텔리전스]]

## 출처

- [[wiki/sources/2026-06-07-harness-engineering-guide|하네스 엔지니어링 기초 가이드북]]
- [[wiki/sources/2026-06-08-ai-workflow-overhaul-silval-dev|AI를 기존 방식에 얹지 마세요]]
