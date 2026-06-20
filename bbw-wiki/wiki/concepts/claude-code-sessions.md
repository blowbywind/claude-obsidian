---
title: Claude Code Sessions
aliases: [클로드 코드 세션]
tags: [tool, claude, workflow]
summary: Claude Code에서 세션 컨텍스트 관리, 재개 방법, session-start 훅 동작 방식
---

# Claude Code Sessions

[[claude-code-tools]] 의 세션 관리 메커니즘.

## 개요

Claude Code는 대화 세션 단위로 컨텍스트를 유지한다. 세션 시작 시 `session-start` 훅이 실행되어 컨텍스트를 자동 주입한다.

## 관련 노트

- [[claude-code-tools]]
- [[obsidian-mcp-hybrid-retrieval]]
