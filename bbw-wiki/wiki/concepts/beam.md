---
title: `BEAM`
type: concept
status: ai-curated
learned_by: lian
curated_at: 2026-06-25
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-25-lian-learning]]
---

# `BEAM`

Obsidian 위키 노트 본문을 작성하겠습니다. 원문에서 제공한 정보만 사용하고 구조를 맞추겠습니다.

---

**BEAM**은 100K~10M 토큰 범위의 초장기(超長期) 메모리 환경에서 AI 에이전트 성능을 검증하는 벤치마크로, 컨텍스트 주입 우회가 불가능한 조건 하에서 에이전트의 장시간 기억 능력을 스트레스 테스트합니다.

## 요점

1. **3대 메모리 평가 표준화**: BEAM은 멀티세션 대화 평가(LoCoMo), 실제 웹 환경 동작 궤적(LongMemEval-V2)과 함께 AI 에이전트 메모리 평가의 표준 벤치마크로 정립되었습니다.

2. **극단적 대용량 메모리 테스트**: 토큰 규모 100K~10M 범위에서 에이전트가 과거 컨텍스트를 효과적으로 활용하고 회상할 수 있는지를 측정합니다.

3. **구조적 우회 방지**: 단순 프롬프트 조정이나 컨텍스트 관리 트릭으로 우회 불가능한 설계로, 실제 에이전트 메모리 역량을 평가합니다.

## 출처

- Lian 자가학습 원문 (2026-06-25): "AI 에이전트 메모리 평가 벤치마크 3종 구체화" 섹션

---

**자 수**: 약 330자 (본문 + 요점 + 출처)

Co-Authored-By: Claude Haiku 4.5 <noreply@anthropic.com>

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-25-lian-learning]]. 사람 검증 후 status를 verified로 변경하세요.
