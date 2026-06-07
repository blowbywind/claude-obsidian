---
title: 에이나우 클로드코드 실전 마스터가이드 v1.0
type: source
tags: [claude-code, ainow, boris-cherny, harness]
created: 2026-06-07
updated: 2026-06-07
origin: bbw-wiki/raw/에이나우_클로드코드_실전마스터가이드_v1.0.pdf
author: 신영선 (에이나우)
date_published: 2026-01-01
---

## 요약

에이나우(신영선)가 Claude Code 창시자 Boris Cherny의 42가지 팁, Anthropic 해커톤 우승자 노하우, 글로벌 커뮤니티 베스트 프랙티스를 통합한 한국어 실전 가이드북. 비개발자도 자신의 전문 분야 문제를 정확히 알면 Claude Code로 실제 서비스를 만들 수 있다는 핵심 메시지를 담는다.

## 핵심 주장

- **AI 생산자 관점**: AI를 소비(질문→답변)하는 수준을 넘어, 서비스·콘텐츠·자동화로 가치를 만드는 'AI 생산자'가 되는 것이 목표
- **전문성 × Claude Code = 10배 증폭**: 코딩 실력보다 자기 분야 문제를 정확히 아는 것이 핵심. 2026년 해커톤 1등은 변호사였고 코드를 한 줄도 직접 쓰지 않음
- **Boris Cherny 자기학습 루프**: 에이전트가 실수할 때마다 CLAUDE.md에 방지 규칙을 추가하는 방식으로 점진적으로 성장시키는 워크플로우
- **병렬 작업으로 하루 100개 PR**: 여러 독립 작업을 서브 에이전트로 동시에 실행
- **토큰 비용 50% 절감**: 고급 세팅(컨텍스트 관리, 캐싱, 모델 선택)으로 비용 최적화
- **GitHub 커뮤니티 스킬 1,234개+**: Everything Claude Code 리포 등 오픈소스 생태계 적극 활용

## 구성 (6 파트)

| 파트 | 내용 |
|------|------|
| Part 1 | 설치 ~ 첫 대화, 왕초보 실수 5가지 |
| Part 2 | Boris Cherny 워크플로우 (핵심) |
| Part 3 | 해커톤 우승자 노하우, AgentShield |
| Part 4 | GitHub 오픈소스 활용, 플러그인 시스템 |
| Part 5 | 업종별 실전 프로젝트 (마케터·크리에이터·병원·사업가) |
| Part 6 | 토큰 비용 절감, Agent Teams, 자동화 조합 |

## Boris Cherny 핵심 팁 (상위)

1. CLAUDE.md는 100줄 이내로 시작 — 처음부터 완벽하게 쓰지 말고 실수할 때마다 추가
2. 자기학습 루프: 실수 발견 → 원인 분석 → CLAUDE.md 규칙 추가 → 반복
3. 병렬 서브 에이전트로 독립 작업 동시 실행 → 하루 100개 PR 달성
4. 컨텍스트 윈도우 관리가 비용과 품질을 좌우
5. Skills(스킬)로 필요 시점에만 지침 로딩 — 컨텍스트 폭발 방지

## 연결된 개념

- [[bbw-wiki/wiki/concepts/claude-md|CLAUDE.md]]
- [[bbw-wiki/wiki/concepts/harness-engineering|하네스 엔지니어링]]
- [[bbw-wiki/wiki/concepts/boris-self-learning-loop|Boris 자기학습 루프]]
- [[bbw-wiki/wiki/concepts/context-window|컨텍스트 윈도우]]
- [[bbw-wiki/wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]]
- [[bbw-wiki/wiki/concepts/claude-code-commands-skills|커맨드 & 스킬스]]

## 연결된 엔티티

- [[bbw-wiki/wiki/entities/boris-cherny|Boris Cherny]]
- [[bbw-wiki/wiki/entities/ainow|에이나우]]
- [[bbw-wiki/wiki/entities/claude-code|Claude Code]]
- [[bbw-wiki/wiki/entities/anthropic|Anthropic]]

## 메모

- 비개발자 대상 실전 가이드로, 설치법보다 워크플로우·비즈니스 적용에 무게
- Boris의 42가지 팁 전체는 부록 A에 수록 (본 가이드에서는 상위 15개 발췌)
- 업종별 CLAUDE.md 템플릿 5종 제공 (마케터·크리에이터·병원·사업가·개발자)
