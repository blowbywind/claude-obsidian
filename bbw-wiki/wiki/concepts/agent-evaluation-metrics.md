---
title: Agent Evaluation Metrics
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-18-haeri-learning]]
---

# Agent Evaluation Metrics

## 핵심 정의

Agent Evaluation Metrics는 에이전트의 성능을 정량적으로 측정하는 평가 지표 체계다. 에이전트가 주어진 작업을 정확하게 완료했는지, 각 단계가 올바른지, 도구 호출이 적절했는지를 체계적으로 검증하는 기준을 제공한다.

## 3대 핵심 지표

1. **TrajectoryAccuracy** (단계 경로 정확도)
   - 에이전트가 목표 달성까지 따른 단계별 의사결정이 얼마나 최적인지 평가
   - 불필요한 중간 단계나 우회 경로 감지

2. **ToolCorrectnessJudge** (툴 호출 정확도)
   - 에이전트가 호출한 각 도구(함수, API)가 문제 해결에 적절했는지 판단
   - 도구 선택 오류나 매개변수 오류 적발

3. **TaskCompletionJudge** (최종 목표 달성 여부)
   - 최종 출력이 사용자의 요구사항을 충족하는지 평가
   - 작업 완료의 성공/실패를 이분적으로 판단

## LLM-as-Judge 자동화

LLM을 평가자로 활용하면 인간 판단과 80~90% 일치하면서도 비용을 500~5000배 절감할 수 있다. 자동화된 회귀 테스트와 대규모 에이전트 성능 검증에 적합한 성숙한 기법이다.

## 출처

- https://medium.com/@nairmilind3/llm-evaluation-in-2026-e631a78c67dc
- https://futureagi.substack.com/p/llm-evaluation-frameworks-metrics

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-18-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
