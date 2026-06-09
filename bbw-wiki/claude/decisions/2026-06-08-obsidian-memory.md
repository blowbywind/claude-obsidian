---
date: 2026-06-08
project: claude-config
status: 적용 완료
tags: [claude-code, obsidian, memory, hooks]
---

# Obsidian을 Claude 메모리로 연동

**날짜**: 2026-06-08
**프로젝트**: claude-config
**상태**: 적용 완료

## 결정
Claude Code의 메모리 시스템을 Obsidian 볼트와 연동한다.

## 배경
- Claude는 대화 종료 시 메모리 초기화
- 기존 `~/.claude/memory/`는 규칙 위주 — 프로젝트 맥락·히스토리 담기 어려움
- Obsidian은 마크다운 파일이라 Claude가 직접 읽고 쓸 수 있음

## 구조
```
obsidian-vault/bbw-wiki/claude/
  projects/   ← 프로젝트별 맥락 노트 (세션 시작 시 자동 주입)
  decisions/  ← 기술 결정 기록 (ADR)
  session-log.md ← 세션별 작업 요약 누적
```

## 동작 방식
- `load-context.sh`: 현재 프로젝트 노트를 세션 시작 시 자동 주입
- Stop hook: 세션 종료 시 `session-log.md`에 타임스탬프 기록
- `/daily-log`: 작업 요약을 `session-log.md`에 prepend
