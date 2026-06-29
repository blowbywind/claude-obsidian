---
title: `scaffold
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-26-haeri-learning]]
summary: "에이전트 시스템에서 프롬프트·도구·루프 설계로 구성된 스캐폴드 구조가 모델 성능보다 벤치마크 점수에 더 큰 영향을 미친다."
---

# `scaffold

Obsidian 위키 노트 본문을 자가학습 원문만 기반으로 작성하겠습니다.

---

스캐폴드(Scaffold)는 에이전트 시스템에서 모델 추론을 지원하는 구조 계층입니다. 프롬프트 구조, 도구 목록, 에이전트 루프 설계의 조합으로 구성됩니다.

## 핵심 요점

1. **벤치마크 영향도**: SWE-bench, GAIA 등 에이전트 벤치마크에서 모델 성능보다 스캐폴드 구조가 최종 점수에 더 큰 영향을 미칩니다. 모델 자체 능력이 높아도 루프·도구·프롬프트 설계가 부족하면 점수가 낮을 수 있습니다.

2. **회귀 추적 범위**: E2E 테스트에서 모델 교체 시뿐 아니라 프롬프트 구조나 도구 목록을 변경할 때도 회귀 테스트 범위에 포함해야 합니다. 스캐폴드 변경 자체가 성능 변화 요인이기 때문입니다.

3. **성능 분리 분석**: 에이전트 성능 평가 시 모델 성능과 스캐폴드 효과를 구분해서 분석할 필요가 있습니다.

## 출처

- [Rapidclaw: Scaffold Dependence in Agent Benchmarks](https://www.rapidclaw.dev/)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-26-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
