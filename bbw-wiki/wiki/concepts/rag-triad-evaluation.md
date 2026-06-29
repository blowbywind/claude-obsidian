---
title: RAG Triad Evaluation
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-haeri-learning]]
summary: "RAG 파이프라인에서 환각 방지, 문서 완전성, 답변 정확성을 검증하는 3가지 평가 지표."
---

# RAG Triad Evaluation

## 핵심 정의

**RAG Triad Evaluation**은 검색 증강 생성(RAG) 파이프라인을 평가하기 위한 세 가지 핵심 지표 세트입니다. LLM 기반 응답 생성 시 검색 단계의 품질, 컨텍스트의 충분성, 최종 답변의 관련성을 종합적으로 검증합니다.

## 3가지 평가 지표

1. **Faithfulness** — 생성된 답변이 검색 문서에 근거하는지 검증. 환각(hallucination) 방지.
2. **Context Recall** — 검색 컨텍스트가 충분하고 완전한지 평가. 누락된 관련 문서 감지.
3. **Answer Relevance** — 최종 답변이 쿼리에 실제로 답하는지 확인. 생성 정확성 검증.

## 적용 범위

- LLM 앱 E2E 검증 시나리오에 적용 가능
- DeepEval, RAGAS, TruLens 등 오픈소스 구현체 활용 가능

## 출처

- https://deepeval.com/guides/guides-rag-evaluation

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
