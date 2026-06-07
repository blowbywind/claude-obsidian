---
title: 에이전트 루프 (Agentic Loop)
type: concept
tags: [agentic-ai, architecture, claude-code]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-how-claude-code-works]
---

## 정의

LLM 에이전트가 작업을 완료할 때까지 **맥락 파악 → 조치 실행 → 결과 검증**을 반복하는 핵심 실행 패턴. Claude Code의 작동 원리이자 현대 에이전트 AI 시스템의 기본 아키텍처.

## 3단계

1. **맥락 파악**: 파일 탐색, 코드 읽기, 현재 상태 이해
2. **조치 실행**: 파일 수정, 명령 실행, API 호출
3. **결과 검증**: 테스트 실행, 출력 확인, 다음 단계 결정

각 단계의 결과가 다음 단계의 입력이 된다. 복잡한 작업일수록 루프가 더 많이 반복된다.

## 구성 요소

- **모델**: 추론 담당 — "Claude가 선택한다"는 곧 모델이 추론한다는 의미
- **도구**: 실행 담당 — 도구 없이는 텍스트 응답만 가능; 도구가 에이전시를 만든다

## 인간의 역할

루프는 자율적이지만 언제든 개입 가능:
- `Esc` 로 즉시 중단
- 진행 중 수정 메시지 전송 → 현재 작업 완료 후 반영
- `Shift+Tab` 두 번으로 Plan 모드 진입 (읽기 전용 분석만)

## LLM Wiki와의 관계

[[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]]에서 "인제스트" 작업이 에이전트 루프의 전형적 예시:
소스 읽기 → 분석 → 위키 페이지 생성/갱신 → index/log 업데이트 반복.

## 관련 개념

- [[wiki/concepts/context-window|컨텍스트 윈도우]] — 루프가 참조하는 정보 공간
- [[wiki/concepts/claude-code-tools|Claude Code 도구]] — 루프의 실행 수단

## 관련 엔티티

- [[wiki/entities/claude-code|Claude Code]]

## 출처

- [[wiki/sources/2026-06-05-how-claude-code-works]]
