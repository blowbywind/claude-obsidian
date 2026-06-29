---
title: `llm
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-haeri-learning]]
summary: "비결정적 LLM 시스템을 위해 편향 완화, 3-judge 앙상블, 객관적 검증, 복합 프롬프트로 판정·에이전트·RAG 평가 품질을 확보하는 실무 원칙"
---

# `llm

원문을 기반으로 `llm` concept 노트를 작성하겠습니다.

---

## 핵심 정의

**LLM(Large Language Model)**은 본질적으로 비결정성 시스템으로, 같은 입력에 대해 확률적으로 다른 출력을 생성한다. 실무에서는 이를 "버그가 아닌 기능"으로 인식하고, 구조적 완화와 객관적 검증 기준을 설계해야 한다.

## 주요 요점

### 1. LLM-as-Judge의 5대 편향과 완화 전략
LLM을 판정자로 사용할 때 위치 편향(position), 장황성 편향(verbosity), 자기선호(self-preference), 포맷 편향(format), 캘리브레이션 드리프트가 발생한다. 이를 완화하려면 ① 답변 순서를 랜덤화하고 ② 대칭적 포맷을 강제하며 ③ 중요 판정에는 서로 다른 모델군(Claude + GPT + Gemini)의 3-judge 앙상블을 적용하고 Krippendorff's alpha ≥ 0.8 목표로 신뢰도를 검증해야 한다.

### 2. AI 에이전트 E2E 테스트 원칙
비결정성 시스템의 단위 테스트는 LLM 레이어를 mock(DI)하여 결정론적으로 수행하고, E2E 테스트는 구조화된 추출·분류·구문 검증처럼 객관적으로 검증 가능한 시나리오만 대상으로 한다. Flaky test 발생 시 격리(quarantine) → 근본원인 분석 루프를 운영한다.

### 3. RAG 평가의 3지표 세트
RAG 파이프라인 검증 시 Faithfulness(생성 답변이 검색 결과 기반하는지) + Context Recall(검색 컨텍스트 충분성) + Answer Relevance(답변이 쿼리에 부합하는지) 3종을 함께 평가해야 downstream 오염을 방지한다.

### 4. 복합 프롬프트 설계(Composite Prompting)
단순 CoT보다 few-shot + 역할 정의(role) + CoT + 포맷 제약을 조합한 복합 프롬프트가 복잡한 통합 테스트 시나리오에서 더 높은 품질의 출력을 생성한다.

---

## 출처
- https://futureagi.com/blog/evaluating-llm-judge-bias-mitigation-2026/
- https://medium.com/@adnanmasood/rubric-based-evals-llm-as-a-judge-methodologies-and-empirical-validation-in-domain-context-71936b989e80
- https://medium.com/@derekcashmore/the-ai-agent-testing-pyramid-a-practical-framework-for-non-deterministic-systems-276c22feaec8
- https://deepeval.com/guides/guides-rag-evaluation
- https://dev.to/honestai/7-prompt-engineering-techniques-that-actually-work-in-2026-with-real-examples-3aj1

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
