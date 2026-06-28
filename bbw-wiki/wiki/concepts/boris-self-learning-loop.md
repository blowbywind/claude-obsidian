---
title: Boris 자기학습 루프 (Self-Learning Loop)
type: concept
tags: [claude-code, boris-cherny, claude-md, harness]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-ainow-claude-code-master-guide]
---

## 정의

Claude Code 창시자 Boris Cherny가 제안한 CLAUDE.md 점진적 성장 방법론. 에이전트가 실수할 때마다 원인을 분석하고 방지 규칙을 CLAUDE.md에 추가하여 시스템이 스스로 학습·성장하는 루프.

## 상세

### 루프 구조

```
에이전트 실수 발생
     ↓
원인 분석
     ↓
방지 규칙 작성
     ↓
CLAUDE.md에 추가
     ↓
다음 세션부터 적용 → (반복)
```

### 핵심 원칙

- **작게 시작**: CLAUDE.md 100줄 이내로 시작, 처음부터 완벽하게 쓰지 않는다
- **실수 주도 성장**: 이론적 규칙보다 실제 발생한 실수를 기반으로 규칙 추가
- **점진적 축적**: 세션이 반복될수록 에이전트가 점점 더 정확하게 동작
- **영구 방지**: 같은 실수는 두 번 반복하지 않도록 구조화

### Hashimoto 정의와의 연결

이 루프는 Mitchell Hashimoto의 하네스 엔지니어링 정의와 동일한 원리다:
"에이전트가 실수를 할 때마다 그 실수를 다시는 반복하지 못하도록 해결책을 설계하는 것."

CLAUDE.md가 바로 그 '해결책'의 저장소다.

### bbw 실천 현황

현재 bbw의 `~/.claude/CLAUDE.md`와 `~/.claude/memory/lessons.md`가 이 루프의 구현체다:
- 실수 원인 분석 → `memory/lessons.md` 기록 → ACTIVE RULES 반영

## 관련 개념

- [[wiki/concepts/claude-md|CLAUDE.md]] — 자기학습 루프의 저장소
- [[wiki/concepts/harness-engineering|하네스 엔지니어링]] — 동일 원리의 시스템 수준 확장
- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — 루프가 동작하는 맥락

## 관련 엔티티

- [[wiki/entities/boris-cherny|Boris Cherny]] — 방법론 창안자
- [[wiki/entities/claude-code|Claude Code]] — 루프가 적용되는 도구

## 출처

- [[wiki/sources/2026-06-07-ainow-claude-code-master-guide|에이나우 클로드코드 실전 마스터가이드]]
