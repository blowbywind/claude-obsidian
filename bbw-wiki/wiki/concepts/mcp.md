---
title: MCP (Model Context Protocol)
type: concept
tags: [claude-code, integration, tools, automation]
created: 2026-06-05
updated: 2026-06-07
sources: [2026-06-05-claude-code-7steps-mastery, 2026-06-07-zotero-notebooklm-llm-wiki-upgrade]
---

## 정의

AI(Claude Code 등)와 외부 도구를 연결하는 다리 역할의 프로토콜. MCP를 설정하면 Claude Code가 외부 서비스의 데이터를 읽고 쓰며 작업을 자동화할 수 있다.

## 연결 가능한 외부 도구

- 생산성: 노션, 구글 캘린더, 구글 드라이브, 구글 Docs/Sheets
- 개발: GitHub, 데이터베이스
- 커뮤니케이션: Slack, Discord, 텔레그램
- 마케팅: 메타 광고 라이브러리
- 디자인: 피그마
- 검색/스크래핑: 웹 검색, 웹스크래핑
- 지식 관리: **Zotero** (레퍼런스 매니저), **NotebookLM** (Google AI 연구 도구)

## 활용 패턴

여러 MCP를 조합해 하나의 워크플로우 구성 가능:
> 구글 캘린더 + 노션 참고 → 피그마에 랜딩 페이지 생성

→ 단일 명령으로 여러 외부 서비스를 가로질러 작업 자동화

## 관련 개념

- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — MCP는 워크플로우 확장 수단
- [[wiki/concepts/hooks|훅스]] — MCP 연동과 함께 사용하면 자동화 범위 확대
- [[wiki/concepts/claude-code-commands-skills|커맨드 & 스킬스]] — 스킬에서 MCP를 활용하는 패턴

## PKM 특화 MCP 사례 (Zotero × NotebookLM)

**Zotero MCP**:
- GitHub 오픈소스, Claude Code에 URL 붙여넣기로 설치
- 시멘틱 검색, 하이라이트, 풀텍스트, 컬렉션 생성 가능
- → 조테로 인제스트 스킬로 Zotero → LLM Wiki 자동화

**notebooklm.py MCP**:
- Claude Code에서 NotebookLM(Google)을 코드로 제어
- 처리는 Gemini가 담당 → Claude 토큰 절약
- 아웃풋(인포그래픽·PPT)을 Obsidian에 자동 저장

## 관련 엔티티

- [[wiki/entities/claude-code|Claude Code]]
- [[wiki/entities/zotero|Zotero]] — Zotero MCP
- [[wiki/entities/notebooklm|NotebookLM]] — notebooklm.py MCP

## 출처

- [[wiki/sources/2026-06-05-claude-code-7steps-mastery]]
- [[wiki/sources/2026-06-07-zotero-notebooklm-llm-wiki-upgrade]]
