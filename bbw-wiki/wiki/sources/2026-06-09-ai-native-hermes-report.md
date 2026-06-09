---
title: AI 네이티브 운영 방법 — 헤르메스 에이전트 실무 적용기
type: source
tags: [ai-native, hermes, multi-agent, obsidian, cron, codex, session-send, erp]
created: 2026-06-09
updated: 2026-06-10
origin: https://youtu.be/vrc0Uv2BfRk
author: 김요일
date_published: 2026-06-09
---

## 요약
1인 기업 대표 김요일이 헤르메스 에이전트 5명 + Claude Code 에이전트 5명으로 구성된 AI 네이티브 팀을 실제 운영하는 방법을 공유한 영상. 핵심은 플랫폼별 역할 분리(헤르메스=에이전시/야간, Claude Code=인하우스/주간), 크론잡 야간 자율 학습 루프, 옵시디언 위키로 10명 에이전트 간 맥락 공유다. 어떤 도구(Codex·Claude·Gemini)를 써도 위키만 있으면 맥락이 즉시 연결되어 도구 종속성이 제거된다.

## 핵심 주장
- 에이전트도 폴더처럼 집중 환경이 필요 — 헤르메스=에이전시, Claude Code=인하우스로 분리
- 자는 시간에 크론잡 + 학습 루프 → 기상 시 레벨업된 에이전트
- 방대한 학습을 에이전트 메모리에 저장하면 메모리 터짐·성능 저하 → 옵시디언 위키화 필수
- 옵시디언 위키로 도구 종속성(Codex/Claude/Gemini) 제거 — 위키만 있으면 어디서든 맥락 연결
- Session Send = Claude Code Agent Teams (v2.1.80+) — 공유 파일 기반 에이전트 간 통신
- AI 네이티브 ERP = 위키 + 태스크 + 메신저 + 에이전트 현황 + 토큰 대시보드 통합

## 핵심 인사이트 원문

> "저는 코덱스든 클로드 코드든 제미나이든 어떤 도구를 사용하든 이 위키만 있으면 하던 작업을 바로 이어서 진행할 수가 있고 일일이 업무에 대해 설명을 할 필요가 없어지는 겁니다."

> "방대한 자료들을 전부 저장하면 메모리가 터져버리고 에이전트가 멍청해집니다."

> "AI든 에이전트든 개발 과잉 영역이 존재한다고 생각합니다. AI를 만든 사람도 이 정도까지 만들어야지 하고 만들지는 않았을 겁니다."

## 실제 작업물 예시

**유튜브 쇼츠 조회수 급상승 실시간 수집 사이트** — 에이전트 5명 협업:

| 에이전트 | 담당 |
|---|---|
| 효리 (효2) | UI 디자인 |
| 효율이 (효1) | 개발 |
| 효삼이 (효3) | 검증 |
| 효나 (효4) | 유튜브 정책·콘텐츠 데이터 확인 |
| 김요일 (인간) | 기획·감독·디렉션 |

향후: 크론잡으로 자가 점검·수정 + UX 리서치 자동화 → 효리에게 전달 → 디자인 수정

## BBW 적용 포인트

| 인사이트 | BBW 현황 | 적용 방향 |
|---|---|---|
| 옵시디언 위키 = 에이전트 맥락 공유 | 이미 구축 중 (bbw-wiki) | 이 전략이 검증된 실전 사례 |
| 행동 기준 규칙 (≒CLAUDE.md) | CLAUDE.md 있음 | 헤르메스 도입 시 동일 패턴 적용 |
| 야간 크론잡 학습 루프 | 미구축 | 관심 영역이면 헤르메스 탐색 고려 |
| 3시간 자동 커밋 크론잡 | 수동 커밋 | 간단한 크론잡으로 적용 가능 |
| 도구 종속성 제거 (위키 우선) | 진행 중 | 위키 완성도가 핵심 자산 |

## 연결된 개념
- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]]
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]]
- [[wiki/concepts/context-intelligence|컨텍스트 인텔리전스]]
- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]]

## 연결된 엔티티
- [[wiki/entities/kimyoil|김요일]]
- [[wiki/entities/hermes-agent|헤르메스 에이전트]]
- [[wiki/entities/openclaw|OpenClaw]] — 헤르메스 유사 도구, 웹 검색 확인
- [[wiki/entities/opendesign|OpenDesign]]
- [[wiki/entities/obsidian|Obsidian]]
- [[wiki/entities/claude-code|Claude Code]]

## 메모
- "오픈 클로" = **OpenClaw** 확인 (2026.01 출시 오픈소스, https://openclaw.ai/)
- 코덱스 = **OpenAI Codex CLI** 확인 (2026.04 토큰 기반 과금, $100–200/월)
- Session Send = **Claude Code Agent Teams** (v2.1.80+) 확인
- 팀명: 헤르메스=린네이티브, Claude Code=린 프로젝트 (추정, 미확인)
- OpenDesign 공식 URL 불명확
- AI 네이티브 ERP는 현재 구상 단계 (미출시)
- 상세 분석: `raw/2026-06-09-ai-native-hermes-report-full.md`
