---
title: τ
type: concept
status: ai-curated
learned_by: snow
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-snow-learning]]
---

# τ

## 핵심 정의
τ-bench는 Sierra와 Princeton이 개발한 실세계 에이전트 평가 벤치마크로, 정적 QA 기준과 달리 동적 사용자 및 도구 시뮬레이션 환경에서 에이전트를 검증한다.

## 주요 특징
- **멀티턴 상호작용 기반**: 단순 정답지 대조가 아닌 연속적 사용자 입력·도구 응답 시뮬레이션으로 실무 적응력 측정
- **도구 호출 정확도**: 에이전트가 올바른 타이밍에 적절한 도구를 선택·실행하는 능력을 정량화
- **멀티턴 완료율**: 복합 작업 수행 과정에서 최종 목표 달성까지의 성공률 추적
- **실세계 환경 반영**: 동적 변수를 포함한 시뮬레이션으로 프로덕션 간극 최소화

## 적용 가치
autobots 및 멀티에이전트 시스템의 기능 검증 시 τ-bench 지표(multi-turn 완료율·도구 호출 정확도)를 평가 기준으로 채택할 만한 신뢰성 있는 벤치마크.

## 출처
- https://sierra.ai/blog/benchmarking-ai-agents

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-snow-learning]]. 사람 검증 후 status를 verified로 변경하세요.
