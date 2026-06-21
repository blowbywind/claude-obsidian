---
title: `golden
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-haeri-learning]]
---

# `golden

자가학습 원문을 분석하여 "Golden Dataset Synthesis" 노트를 작성하겠습니다.

---

## 본문 (마크다운만)

**핵심 정의**  
Golden Dataset은 LLM 평가(eval)를 위한 고품질 예시 데이터셋으로, DeepEval Synthesizer 같은 도구로 기존 문서에서 자동 생성할 수 있는 구조화된 질문-답변 쌍을 말한다.

**요점**

1. **자동 생성 효율성**: DeepEval Synthesizer로 문서로부터 수천 개 goldens을 몇 분 내에 생성 가능하며, 엣지케이스도 자동으로 커버한다.

2. **개인정보 보호 이점**: 실제 사용자 데이터 없이 합성 goldens으로 충분해, PII 유출 위험 없이 평가 데이터셋을 구성할 수 있다.

3. **전문가 검증 보완재 원칙**: 전문가가 직접 검증한 golden을 완전히 대체할 수는 없으며, **보완 용도로만 활용**해야 한다. 초기 eval 운영에는 100+ 예시면 충분하다.

**출처**
- https://deepeval.com/docs/golden-synthesizer
- https://arize.com/blog/creating-and-validating-synthetic-datasets-for-llm-evaluation-experimentation/

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
