---
title: 컨텍스트 윈도우 (Context Window)
type: concept
tags: [llm, claude-code, memory, architecture]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-how-claude-code-works]
---

## 정의

LLM이 한 번에 처리할 수 있는 정보의 총량. Claude Code에서는 대화 이력, 파일 내용, 명령 출력, CLAUDE.md, Auto Memory, 로드된 Skills, 시스템 지시가 모두 이 공간을 공유한다.

## 컨텍스트를 채우는 것들

| 항목 | 비고 |
|------|------|
| 대화 이력 | 누적될수록 증가 |
| 파일 내용 | 읽은 파일마다 추가 |
| 명령 출력 | 특히 긴 출력은 빠르게 소모 |
| CLAUDE.md | 세션 시작 시 로드 |
| Auto Memory | 첫 200줄 또는 25KB |
| Skills | 설명은 항상 로드, 내용은 사용 시만 |
| MCP 도구 정의 | 기본 지연 로드 (이름만 보임) |

## 자동 컴팩션

컨텍스트가 한계에 가까워지면 Claude Code가 자동으로:
1. 오래된 도구 출력 제거
2. 대화 요약

→ 요청과 핵심 코드는 보존, **초기의 상세 지시는 손실될 수 있다.**

**실용 규칙**: 영구 규칙은 반드시 CLAUDE.md에, 임시 지시만 대화에 넣는다.

## 컨텍스트 절약 전략

- **Skills**: `disable-model-invocation: true`로 설명조차 컨텍스트에서 제외
- **Subagents**: 별도 컨텍스트 창에서 실행 → 메인 세션 오염 없음
- `/context` 명령으로 현재 공간 사용 현황 확인
- `/compact focus on X` 로 보존 대상 지정하며 수동 컴팩션

## 관련 개념

- [[wiki/concepts/agentic-loop|에이전트 루프]] — 컨텍스트를 소비하는 주체
- [[wiki/concepts/claude-md|CLAUDE.md]] — 컨텍스트 밖에서 영속하는 지시 파일

## 관련 엔티티

- [[wiki/entities/claude-code|Claude Code]]

## 출처

- [[wiki/sources/2026-06-05-how-claude-code-works]]
