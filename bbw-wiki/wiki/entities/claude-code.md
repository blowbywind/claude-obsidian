---
title: Claude Code
type: entity
tags: [product, developer-tool, ai, agentic]
created: 2026-06-05
updated: 2026-06-07
sources: [2026-06-05-how-claude-code-works, 2026-06-05-claude-code-beginner-install-guide, 2026-06-05-claude-code-7steps-mastery, 2026-06-07-ainow-claude-code-master-guide, 2026-06-07-harness-engineering-guide]
---

## 개요

Anthropic이 만든 터미널 기반 에이전트형 코딩 도우미. Claude 언어 모델을 감싸는 **에이전트 기반 장치**로, 도구·컨텍스트 관리·실행 환경을 제공해 LLM을 유능한 코딩 에이전트로 변환한다.

bbw-wiki를 포함한 bbw의 개인 프로젝트 전반을 관리하는 핵심 도구.

## 핵심 특징

- **에이전트 루프**: 맥락 파악 → 조치 실행 → 결과 검증을 자율 반복
- **도구**: 파일 읽기/수정, 셸 실행, 웹 검색, 코드 인텔리전스
- **컨텍스트 관리**: CLAUDE.md(영구 지시), Auto Memory(자동 학습), 자동 컴팩션
- **확장**: Skills(워크플로), MCP(외부 서비스 연결), Subagents(목적별 AI 팀), Hooks(자동화 트리거), Commands(슬래시 단축 명령)
- **세션**: 독립적, resume/fork 가능, git worktree로 병렬 운용

## 실행 인터페이스

터미널, VS Code 확장, JetBrains 확장, claude.ai/code, Remote Control, Slack, CI/CD

## bbw 설정

- 홈 서버 Ubuntu에서 VSCode Remote SSH + 터미널로 사용
- 프로젝트별 CLAUDE.md + `~/.claude/CLAUDE.md` (글로벌) 설정
- bbw-wiki에서 에이전트 스키마(CLAUDE.md)에 따라 위키 유지 담당

## 주요 연결

- [[wiki/concepts/agentic-loop|에이전트 루프]] — 핵심 작동 원리
- [[wiki/concepts/context-window|컨텍스트 윈도우]] — 컨텍스트 관리
- [[wiki/concepts/claude-md|CLAUDE.md]] — 영구 지시 파일
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — bbw-wiki를 유지하는 데 사용
- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — Claude Code 기반 자동화 패턴
- [[wiki/entities/anthropic|Anthropic]] — 개발사

## 관련 개념 추가

- [[wiki/concepts/mcp|MCP]] — 외부 도구 연결 프로토콜
- [[wiki/concepts/hooks|훅스]] — 자동화 트리거
- [[wiki/concepts/claude-code-commands-skills|커맨드 & 스킬스]] — 반복 업무 자동화 단위

## 하네스 엔지니어링 관점

Claude Code 자체가 하네스 엔지니어링 도구다. CLAUDE.md(컨텍스트)·Hooks(피드백 루프)·권한 모델(인간 개입)·Skills(점진적 정보 공개)·Sub-agents(병렬 처리)·MCP(외부 연결)가 하네스의 5대 구성요소를 모두 구현한다.

- [[wiki/concepts/harness-engineering|하네스 엔지니어링]]

## 출처

- [[wiki/sources/2026-06-05-how-claude-code-works]]
- [[wiki/sources/2026-06-05-claude-code-beginner-install-guide]]
- [[wiki/sources/2026-06-05-claude-code-7steps-mastery]]
- [[wiki/sources/2026-06-07-ainow-claude-code-master-guide]]
- [[wiki/sources/2026-06-07-harness-engineering-guide]]
