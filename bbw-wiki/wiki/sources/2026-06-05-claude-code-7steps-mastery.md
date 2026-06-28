---
title: "클로드 코드를 정말 잘 쓰는 7단계 테크트"
type: source
tags: [youtube, claude-code, tutorial, korean, workflow, mcp, hooks, agents]
created: 2026-06-05
updated: 2026-06-05
origin: https://youtu.be/qaJivLeOeQI?si=12v62vWCUebTxgA7
author: 물광 (유튜버)
date_published: 2026-06-05
summary: "Claude Code를 실무 생산성으로 연결하는 7단계 프레임워크(설치→CLAUDE.md→커맨드→스킬→서브에이전트→MCP→훅스)를 비개발자 실무 경험 기반으로 설명한 영상 요약."
---

## 요약

전 영상(왕초보 설치 강의)의 후속편. Claude Code를 단순 설치에서 끝내지 않고 실제 생산성으로 연결하는 7단계 프레임워크를 제시한다. 비개발자 입장에서 실무 운영 경험(개발 OS 80개 에이전트, 운영 OS 8–9개 에이전트)을 바탕으로 설명.

## 7단계 프레임워크

1. **설치** — Antigravity 확장 프로그램(초보자) 또는 터미널(Git + Node.js + `npm install -g @anthropic-ai/claude-code`)
2. **CLAUDE.md 세팅** — AI의 두뇌 설계. 글로벌 최상위에는 100줄 핵심만, 프로젝트별 하위 폴더에 세분화된 CLAUDE.md 별도 운영
3. **커맨드** — 반복 업무를 슬래시 단축 명령으로 등록 (`.claude/commands/` 폴더). 짧은 명령 개념
4. **스킬스** — 순서대로 실행되는 워크플로우 (`.claude/skills/` 폴더). 먼저 직접 해보고 결과물이 나왔을 때 "스킬스 파일로 만들어줘" 방식 권장
5. **서브에이전트** — AI 팀 단위 운영. 창시자 5개, 해커톤 우승자 13개. 많다고 좋은 게 아님 — 목적·결과값 품질이 중요
6. **MCP** — 외부 도구와 AI를 연결하는 다리. 노션·구글 캘린더·피그마·GitHub·Slack·Discord·메타 광고 등 연결
7. **훅스** — 자동화 트리거. preToolUse(위험 명령 차단), postToolUse(자동 포맷팅), notification(Discord 알림). 매일 6–7시 에이전트 자동 보고

## 핵심 인사이트

- CLAUDE.md는 100줄 핵심만 글로벌에, 프로젝트별 세분화가 원칙 (클로드 코드 창시자·해커톤 우승자·커뮤니티 공통 권장)
- 커맨드 vs 스킬 구분: 커맨드=짧은 명령, 스킬=순서대로 실행하는 워크플로우
- 스킬 만드는 법: 먼저 작업 수행 → 결과물 확인 → "스킬스 파일로 정리해 줘" 요청
- 서브에이전트 비유: 임원(CCO, CMO 등) — 메인 AI가 적합한 에이전트에 위임
- MCP를 여러 개 조합하면 여러 외부 도구를 엮은 워크플로우 자동화 가능
- 훅스는 일종의 크론(Cron) — 특정 상황 발생 시 자동 실행

## 연결된 개념

- [[wiki/concepts/claude-md|CLAUDE.md]] — 2단계, 글로벌 vs 프로젝트 분리 원칙
- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — 스킬스·서브에이전트 실전 운영
- [[wiki/concepts/mcp|MCP]] — 6단계, 외부 도구 연결
- [[wiki/concepts/hooks|훅스]] — 7단계, 자동화 트리거
- [[wiki/concepts/claude-code-commands-skills|커맨드 & 스킬스]] — 3·4단계

## 연결된 엔티티

- [[wiki/entities/claude-code|Claude Code]] — 이 영상의 주제
- [[wiki/entities/antigravity|Antigravity]] — 1단계 추천 IDE
- [[wiki/entities/cowork|Cowork]] — Claude Code와 비교 언급된 AI 도구

## 메모

- "코워크" = Cowork. Claude 앱과 함께 사용하던 AI 도구. "클로드 코드 설치하면 Cowork 쓸 필요 없다"는 맥락 — 다중 파일 수정·읽기·쓰기 권한 기능을 제공하나 Claude Code 터미널이 이를 포함·초과함.
- "Shift+Tab"으로 Plan Mode ↔ Accept Edition ↔ 일반 모드 전환 가능 (영상에서 "알트 시프트 탭"으로 ASR 오류)
- 저자는 비개발자. 커뮤니티·공식 문서 취합 후 실무 적용 경험 공유
- 부트캠프 운영(1기 30명, 하루 만에 마감) — 외부 공개 자료는 아님
