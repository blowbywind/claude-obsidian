---
title: `claude
type: concept
status: ai-curated
learned_by: snow
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-snow-learning]]
---

# `claude

원문을 분석하여 "claude" 주제의 concept 노트 본문을 작성합니다.

---

**Anthropic이 개발한 대형언어모델(LLM) 제품군**. 특히 Claude Opus 시리즈는 코딩·추론 성능에 특화되어 있으며, 멀티에이전트 시스템의 모델 라우팅 전략에서 기준점으로 작용한다.

## 주요 특성

- **SWE-Bench Pro 코딩 성능**: Claude Opus 4.8은 2026년 6월 기준 SWE-bench Verified 88.6%로 1위 기록. Grok의 75% 대비 명확한 우위를 유지하나, GLM-5.2·DeepSeek-R1 계열 오픈웨이트 모델이 빠르게 추격 중.
  
- **라우팅 원칙의 제한성**: "코딩 작업→Claude"는 현재 유효하지만 절대 전제로 두지 말 필요. 오픈소스 모델(Nemotron 3 Ultra, MiniMax M3, Kimi K2.7 Code)의 성능 향상으로 주기적 벤치마크 재검토가 필수.

- **추론-속도 트레이드오프**: 오케스트레이터 설계 시 서브태스크 유형별로 "속도 우선 경량 모델"과 "정확도 우선 Claude"를 분기하는 전략 실무 표준화.

## 출처
- [Best AI Models June 2026](https://www.buildfastwithai.com/blogs/best-ai-models-june-2026)
- [Top LLM Models in 2026](https://aimlapi.com/blog/top-llm-models-in-2026-the-best-ai-models-for-reasoning-coding-multimodal-tasks)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-snow-learning]]. 사람 검증 후 status를 verified로 변경하세요.
