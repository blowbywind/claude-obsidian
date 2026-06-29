---
title: 커맨드 & 스킬스
type: concept
tags: [claude-code, commands, skills, automation, workflow]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-claude-code-7steps-mastery]
summary: "Claude Code의 커맨드(짧은 단축 명령)와 스킬스(순서형 워크플로우)는 반복 업무 자동화 메커니즘"
---

## 정의

Claude Code에서 반복 업무를 자동화하는 두 가지 메커니즘. 커맨드는 짧은 단축 명령, 스킬스는 순서가 있는 워크플로우 실행.

## 커맨드 (Commands)

- **개념**: 슬래시(`/`)로 호출하는 짧은 단축 명령
- **위치**: `.claude/commands/` 폴더의 `.md` 파일
- **용도**: 자주 쓰는 단일 명령을 한 단어로 실행 (예: `/김의사` → 사전 정의된 작업 즉시 실행)

## 스킬스 (Skills)

- **개념**: 순서대로 실행되는 워크플로우 — "이 작업을 이 순서대로 해라"
- **위치**: `.claude/skills/` 폴더의 `.md` 파일
- **스킬 만드는 법**: 먼저 직접 작업 수행 → 원하는 결과물 확인 → "이 작업 방식을 스킬스 파일로 만들어 줘" 요청 → 이후 동일 작업 시 스킬 호출

## 커맨드 vs 스킬 비교

| | 커맨드 | 스킬스 |
|-|--------|--------|
| 성격 | 짧은 명령 | 순서 있는 워크플로우 |
| 복잡도 | 단순 | 복합 |
| 예시 | `/릴스` → 릴스 스크립트 작성 요청 | `/블로그-자동화` → 수집→분석→작성→포맷팅 순차 실행 |

## 스킬 활용 팁

- 처음부터 스킬 만들려 하지 말 것 — 해보지 않은 일을 스킬로 만들기 어려움
- 실제 사용 사례가 쌓인 후 스킬로 변환하는 게 효과적
- 해커톤 우승자는 40개 스킬 운영

## 관련 개념

- [[wiki/concepts/claude-md|CLAUDE.md]] — 전역 규칙을 담는 파일; 커맨드·스킬은 실행 단위
- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — 스킬스는 에이전트 워크플로우의 재사용 단위
- [[wiki/concepts/hooks|훅스]] — 자동 실행 트리거, 스킬과 조합 가능

## 관련 엔티티

- [[wiki/entities/claude-code|Claude Code]]

## 출처

- [[wiki/sources/2026-06-05-claude-code-7steps-mastery]]
