---
title: 훅스 (Hooks)
type: concept
tags: [claude-code, automation, hooks, trigger]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-claude-code-7steps-mastery]
---

## 정의

Claude Code의 자동화 트리거 시스템. "이런 상황이 생기면 이걸 실행해라"는 조건부 자동 실행 규칙으로, Cron과 유사한 개념.

## 주요 훅 종류

| 훅 | 타이밍 | 예시 용도 |
|----|--------|-----------|
| preToolUse | 도구 실행 전 | 위험한 명령어 차단, 검토 요청 |
| postToolUse | 도구 실행 후 | 코드 작성 시 자동 포맷팅 |
| notification | AI가 입력 대기 중 | 작업 완료 시 Slack/Discord 알림 |

## 실전 활용 예

- **매일 자동 보고**: 에이전트들이 매일 6–7시에 전날 작업 내용·이슈·의사결정 과정을 Discord로 자동 보고
- **기록 자동화**: 보고 내용이 아카이브로 누적 → 시스템 자체가 데이터 기반으로 발전

## 관련 개념

- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — 훅스는 에이전트 워크플로우의 자동화 층
- [[wiki/concepts/mcp|MCP]] — 훅 알림 대상으로 Discord(MCP) 연동 가능

## 관련 엔티티

- [[wiki/entities/claude-code|Claude Code]]

## 출처

- [[wiki/sources/2026-06-05-claude-code-7steps-mastery]]
