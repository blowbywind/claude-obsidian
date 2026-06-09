---
title: AI 네이티브 운영 방법 — 헤르메스 에이전트 실무 적용기
type: source
tags: [ai-native, hermes, multi-agent, obsidian, cron]
created: 2026-06-09
updated: 2026-06-09
origin: https://youtu.be/vrc0Uv2BfRk
author: 김요일
date_published: 2026-06-09
---

## 요약
1인 기업 대표 김요일이 헤르메스 에이전트 5명 + Claude Code 에이전트 5명으로 구성된 AI 네이티브 팀을 실제 운영하는 방법을 공유한 영상. 옵시디언 위키를 에이전트 간 맥락 공유 시스템으로 사용해 메모리 효율을 유지하면서 지식을 누적하는 것이 핵심이다.

## 핵심 주장
- 헤르메스(야간·모바일·크론잡)와 Claude Code(주간·인하우스)는 역할을 분리해야 혼선이 없다
- 에이전트도 폴더처럼 집중 환경이 필요하다 — 헤르메스=에이전시, Claude Code=인하우스
- 자는 시간에 크론잡 + 학습 루프를 돌리면 기상 시 레벨업된 에이전트를 얻는다
- 방대한 학습을 에이전트 메모리에 저장하면 메모리가 터지고 멍청해진다 → 옵시디언 위키화 필수
- 옵시디언 위키 공유로 10개 에이전트 간 맥락 즉시 연결, 도구 종속성(Codex/Claude/Gemini) 제거
- 에이전트 간 Session Send(AI 간 대화)로 오케스트레이터가 업무 지시·취합·보고
- AI 네이티브 ERP = 위키 + 태스크 + 메신저 + 에이전트 현황 + 토큰 대시보드 통합

## 연결된 개념
- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]]
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]]
- [[wiki/concepts/context-intelligence|컨텍스트 인텔리전스]]
- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]]

## 연결된 엔티티
- [[wiki/entities/kimyoil|김요일]]
- [[wiki/entities/hermes-agent|헤르메스 에이전트]]
- [[wiki/entities/opendesign|OpenDesign]]
- [[wiki/entities/obsidian|Obsidian]]
- [[wiki/entities/claude-code|Claude Code]]

## 메모
- 헤르메스 설치 → 구글 "헤르메스 에이전트" → 공식 홈페이지 데스크톱 앱. 세팅은 Claude Code/Codex에게 명령 ("Opus 4.8로 연결해줘")
- 헤르메스 = "오픈 클로와 유사한 로컬 에이전트" — 자막 표기 오류 가능, 정확한 비교 대상 불명확
- 현재 Codex(OpenAI)와 연결 — "토큰이 넉넉해서" 선택
- 팀명: 헤르메스=린네이티브, Claude Code=린 프로젝트
- OpenDesign은 Claude Design 로컬화 오픈소스, CLI로 연결. 구체적 URL 없음
- AI 네이티브 ERP는 현재 구상 단계 (미출시)
- 상세 분석은 `raw/2026-06-09-ai-native-hermes-리포트.md` 참조
