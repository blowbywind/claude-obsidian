---
title: `non
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-haeri-learning]]
---

# `non

주제 "`non-deterministic-agent-testing`"에 대해 원문 기반 concept 노트 본문을 작성하겠습니다:

---

AI 에이전트의 비결정성을 버그가 아닌 아키텍처 특성으로 인정하고 구조적으로 다루는 테스트 프레임워크. LLM 출력의 확률론적 본질을 고려해 테스트 전략을 계층별로 분화한다.

**핵심 원칙**

1. **단위 테스트의 결정론화**: LLM 레이어를 Dependency Injection(DI)으로 mock하여 비즈니스 로직 검증을 결정론적으로 수행. 실제 LLM 호출 불가 환경에서도 완전한 단위 테스트 가능.

2. **E2E 테스트의 범위 축소**: 구조화 데이터 추출, 분류, 구문 검증 등 객관적으로 검증 가능한 시나리오에만 집중. 자연어 품질 판정처럼 주관적인 검증은 제외.

3. **Flake 관리 루프**: 비결정성으로 인한 테스트 실패(flake) 발생 시 격리(quarantine) → 근본원인 분석 → 개선 사이클. 무조건적 재시도가 아닌 체계적 추적.

이 접근은 기존 "LLM 테스트를 고정값과 비교" 패러다임을 벗어나 AI 시스템의 본질을 수용하면서도 신뢰성을 확보한다.

**출처**
- [The AI Agent Testing Pyramid for Non-Deterministic Systems](https://medium.com/@derekcashmore/the-ai-agent-testing-pyramid-a-practical-framework-for-non-deterministic-systems-276c22feaec8)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
