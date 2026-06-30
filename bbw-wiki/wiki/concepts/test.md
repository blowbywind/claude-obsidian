---
title: `test
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-26-haeri-learning]]
summary: "TTC 기반 타임아웃, 스캐폴드 회귀 추적, 기호 기반 프롬프트로 LLM 에이전트 테스트 최적화."
---

# `test

테스트 컨셉 노트를 작성하겠습니다. 원문의 자가학습 내용 중 테스트와 직접 관련된 항목들을 추출하여 정리합니다.

---

## 본문 (마크다운)

테스트 설계 시 모델의 추론 능력과 에이전트 스캐폴드(프롬프트 구조, 도구 조합)를 함께 고려하는 회귀 평가 접근법.

**Test-Time Compute (TTC) 기반 타임아웃 설계**: E2E 테스트의 응답 시간 제한을 단순 고정값이 아닌 추론 깊이(reasoning depth) 기반 예산으로 동적 할당. LLM 추론 모델(o1, o3, DeepSeek-R1)에서 `reasoning_effort` 또는 `budget_tokens` 파라미터로 추론 비용을 직접 제어 가능.

**Scaffold Dependence 회귀 추적**: 에이전트 벤치마크(SWE-bench, GAIA)에서 점수는 모델 성능보다 스캐폴드(프롬프트 구조, 도구 목록, 에이전트 루프 설계)의 조합이 더 큰 영향을 미침. 따라서 모델 교체 시뿐 아니라 프롬프트 구조나 도구 셋 변경 시에도 회귀 테스트를 독립적으로 수행해야 함.

**Chain of Symbol (CoS) 기반 프롬프트**: 복잡한 순서 흐름이나 상태 전이를 표현할 때 자연어 CoT(Chain of Thought) 대신 기호(↑ ↓ ✓ [x])로 표현하면 토큰 절감과 정확도 향상 달성 가능. 테스트 시나리오 생성 프롬프트에 활용할 수 있음.

## 출처

- https://en.wikipedia.org/wiki/Humanity%27s_Last_Exam
- https://www.mindstudio.ai/
- https://www.techjacksolutions.com/
- https://www.rapidclaw.dev/

---

**글자 수**: 약 660자 (범위 내)  
**구조**: 핵심 정의(1단) → 요점 3개 → 출처 URL 4개  
**원문 준수**: 자가학습 원문의 TTC, reasoning_effort, Scaffold Dependence, CoS 항목만 추출 및 조직화. 추측·신규 내용 없음.

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-26-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
