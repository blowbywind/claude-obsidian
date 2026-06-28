---
title: "How Claude Code Works"
type: source
tags: [claude-code, agentic-ai, developer-tools]
created: 2026-06-05
updated: 2026-06-05
origin: https://code.claude.com/docs/en/how-claude-code-works
author: Anthropic
date_published:
summary: "Claude Code는 터미널 기반 에이전트형 코딩 도우미로, 에이전트 루프를 반복하며 파일·명령·웹 도구를 활용하고 CLAUDE.md·AutoMemory·Skills·Subagents로 세션 간 지식을 관리한다."
---

## 요약

Claude Code는 터미널에서 실행되는 에이전트형 코딩 도우미로, **에이전트 루프**(맥락 파악 → 조치 실행 → 결과 검증)를 반복하며 작동한다. 도구를 통해 파일 읽기·수정, 명령 실행, 웹 검색 등을 수행하며, CLAUDE.md와 Auto Memory로 세션 간 지식을 유지한다. Skills·Subagents로 컨텍스트를 효율적으로 관리한다.

## 핵심 주장

- 도구가 없으면 LLM은 텍스트만 반환한다 — 도구가 에이전시를 만든다
- 에이전트 루프는 요청의 복잡도에 따라 반복 횟수가 달라진다
- 컨텍스트 윈도우는 자동 컴팩션되지만 영구 규칙은 반드시 CLAUDE.md에 써야 한다
- 세션은 독립적이며 `claude --continue` / `--resume`으로 재개, `/branch`로 포크 가능
- Subagents는 별도 컨텍스트 창에서 실행되므로 메인 세션 컨텍스트를 오염시키지 않는다
- Skills는 사용 시점에만 로드되어 컨텍스트 비용을 절약한다
- 체크포인트로 모든 파일 변경을 되돌릴 수 있다 (원격 시스템 작업 제외)

## 내장 도구 5가지

| 카테고리 | 기능 |
|----------|------|
| File operations | 파일 읽기·편집·생성·이동 |
| Search | 패턴 검색, 정규식 검색, 코드베이스 탐색 |
| Execution | 셸 명령, 서버 시작, 테스트 실행, git |
| Web | 웹 검색, 문서 fetch, 에러 메시지 조회 |
| Code intelligence | 타입 에러, 정의 이동, 참조 찾기 (플러그인 필요) |

## 실행 환경

| 환경 | 코드 실행 위치 |
|------|---------------|
| Local | 사용자 머신 (기본) |
| Cloud | Anthropic 관리 VM |
| Remote Control | 사용자 머신, 브라우저로 제어 |

## 효과적인 사용 팁

- **처음부터 구체적으로**: 파일 경로, 제약 조건, 예시 패턴 명시
- **검증 가능한 기준 제공**: 테스트 케이스, 스크린샷, 예상 출력
- **지시보다 위임**: 어떤 파일을 읽을지 지정하지 말고 목표와 맥락만 제공
- **Plan 모드 먼저**: `Shift+Tab` 두 번으로 계획 모드 진입, 분석 후 실행 분리

## 연결된 개념

- [[wiki/concepts/agentic-loop|에이전트 루프]]
- [[wiki/concepts/context-window|컨텍스트 윈도우]]
- [[wiki/concepts/claude-code-tools|Claude Code 도구]]
- [[wiki/concepts/claude-code-sessions|세션 관리]]
- [[wiki/concepts/claude-md|CLAUDE.md]]

## 연결된 엔티티

- [[wiki/entities/claude-code|Claude Code]]
- [[wiki/entities/anthropic|Anthropic]]

## 메모

- bbw-wiki 자체를 관리하는 도구에 대한 공식 문서 — 실용적 참고값이 높음
- Remote Control 환경은 현재 bbw의 홈서버+회사PC 구성과 유사한 활용 가능성
