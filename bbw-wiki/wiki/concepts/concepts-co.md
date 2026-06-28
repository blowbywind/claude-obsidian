---
title: `concepts/co
type: concept
status: ai-curated
learned_by: snow
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-26-snow-learning]]
---

# `concepts/co

Obsidian 위키 concept 노트를 자가학습 원문 기반으로 작성하겠습니다.

## `concepts/co-failure-ceiling.md` 본문

**핵심 정의**  
Mixture-of-Agents(MoA)의 정확도 상한이 "전 멤버 모델이 동시에 실패하는 확률"에 의해 결정되는 현상. 개별 모델의 오류율이 아닌 모든 에이전트가 한 질문에 동시에 틀릴 가능성으로 시스템 성능 한계가 정해진다.

**요점**

1. **모델 다양성의 결정성**: 단순히 에이전트 개수를 증가시키는 것보다 출처·계열·학습 데이터 이질성이 Co-Failure Ceiling을 낮추는 핵심 축. 동일 계열 모델 집단은 동시 실패 확률이 높음.

2. **라우팅 설계 원칙**: 앙상블 시스템의 성능은 개별 모델 품질이 아닌 "실패 패턴의 독립성"에 좌우됨. 모델 선택 단계에서 학습 데이터 다중성·아키텍처 차이·학습 매개변수 변동성 확보 필수.

3. **정확도 상한 계산**: P(all fail) = ∏ P(model_i fails) 구조로, 멤버 모델이 이질할수록 누적 실패 확률이 낮아짐.

**출처**

- [arxiv 2606.27288 — Co-Failure Ceiling in Mixture-of-Agents](https://arxiv.org/abs/2606.27288)

---

**배치**: `~/obsidian-vault/bbw-wiki/concepts/co-failure-ceiling.md` 로 저장 후, 기존 `Agents/Skills 카탈로그.md`의 "라우팅 원칙" 섹션에 해당 링크 추가 권장.

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-26-snow-learning]]. 사람 검증 후 status를 verified로 변경하세요.
