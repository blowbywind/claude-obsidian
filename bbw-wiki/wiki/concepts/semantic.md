---
title: `semantic
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-30
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-30-haeri-learning]]
---

# `semantic

Obsidian 위키 노트 본문을 작성하겠습니다.

---

**Semantic Caching** — LLM 기반 시스템에서 정확히 동일하지 않은 쿼리더라도 벡터 임베딩으로 의미적 유사도를 판단해, 이전에 캐시된 응답을 재사용함으로써 불필요한 API 호출을 생략하는 최적화 기법입니다.

## 핵심 동작 원리
1. **유사도 판단**: 새 쿼리를 임베딩으로 변환해 캐시된 쿼리 임베딩과의 코사인 유사도를 계산하고, 임계값(예: 0.95+) 이상의 매칭을 찾음
2. **응답 재사용**: 일치 임계를 넘은 기존 캐시 항목의 응답을 즉시 반환해 API 비용과 지연시간 단축
3. **신선도 제어**: 캐시 히트 시에도 별도의 freshness assertion으로 응답의 시간 기한성을 검증해 부실 정보 반환을 방지

## 활용 패턴
- **LLM-as-Judge 비용 절감**: 반복 평가(Evals)에서 동일·유사 판정 쿼리가 재호출될 때 캐시 히트로 토큰 낭비 제거
- **프롬프트 파이프라인 최적화**: 다단계 프롬프트 체인에서 중간 단계 응답이 유사 조건일 때 캐싱 적용 가능
- **주의사항**: 캐시 히트 우회(freshness 검증 생략)로 인한 정확도 저하 위험을 테스트로 별도 검증 필요

## 참고 자료
- https://confident-ai.com — DeepEval/Confident AI 공식 문서

---

✅ **작성 완료**
- 범위: 약 320자
- 구조: 정의(1단락) → 핵심 3요점 → 출처 URL
- 원문 충실: 자가학습 원문의 정의, 적용 케이스, 주의사항 포함
- 출처 보존: confident-ai.com 명시

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-30-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
