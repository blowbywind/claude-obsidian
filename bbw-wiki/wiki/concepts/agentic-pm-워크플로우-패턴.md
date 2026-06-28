---
title: Agentic PM 워크플로우 패턴
type: concept
status: ai-curated
learned_by: kiel
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-kiel-learning]]
summary: "PM의 고수준 목표 기반으로 AI 에이전트가 티켓 수집·분석·우선순위 산정·연동을 자율 실행하되 구조화된 컨텍스트 제공과 PM 검증이 핵심인 워크플로우."
---

# Agentic PM 워크플로우 패턴

Agentic PM 워크플로우는 목표(예: "50개 티켓을 분석해 고우선순위 버그를 백로그에 반영")만 제시하면 AI 에이전트가 데이터 수집→분석→우선순위 산정→Jira/Linear 연동까지 다단계 실행·검증·자동화하는 패턴입니다.

## 핵심 특징

**1. 자율 다단계 워크플로우**
PM이 고수준 목표만 정의하면 에이전트가 티켓 메타데이터 수집·패턴 추출·점수 계산·백로그 반영을 순차 실행합니다. 2026년 PM의 70% 이상이 일상 업무에 AI 도구를 활용 중입니다.

**2. 구조화된 컨텍스트 프레임의 중요성**
단순 "스토리 작성"보다 AI에게 스토리 맵·도메인 정의·제약조건·용어집을 함께 제공하면 생성 인수 조건 품질이 크게 향상됩니다. Capgemini 2024 조사 결과 AI 인수 조건 활용 시 재작업 티켓 약 15% 감소.

**3. PM의 최종 검증 단계**
에이전트는 초안과 틀을 제공하는 역할이며, 도메인 판단·우선순위 조정은 PM이 검토·보정합니다.

## 출처
- [AI Is Changing Product Management in 2026 | AI PM Tools](https://aipmtools.org/articles/ai-changing-product-management)
- [AI-Assisted Story Splitting for Large Features | Agile Seekers](https://agileseekers.com/blog/ai-assisted-story-splitting-for-large-features-in-safe)
- [AI-Assisted Backlog Refinement | StoriesOnBoard](https://storiesonboard.com/blog/ai-assisted-backlog-refinement-clear-user-stories)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-kiel-learning]]. 사람 검증 후 status를 verified로 변경하세요.
