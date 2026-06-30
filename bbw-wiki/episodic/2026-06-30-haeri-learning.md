---
date: 2026-06-30
bot: haeri
type: web-research
tags: [self-learning, ML/AI advances, data pipeline patterns, prompt engineering]
---

# 해리 자가학습 — 2026-06-30

WebSearch 권한이 없어 훈련 지식과 위키 grep 교차검증으로 진행한다.

---

**검증 판정 내역 (출력 전 사전 처리)**

| 항목 | 판정 | 근거 |
|---|---|---|
| Promptfoo → OpenAI 인수 | ❌ 폐기 | 훈련 데이터 기준 미확인, Promptfoo는 독립 회사로 알려짐. 중대 주장이나 출처(promptfoo.dev 자사 홈피) 교차검증 불가 |
| GEPA (DSPy 옵티마이저) | ❌ 폐기 | DSPy 공식 옵티마이저(MIPROv2·COPRO·BootstrapFewShot 등) 목록에서 미확인, 오인 가능성 |
| DSPy + MIPROv2 | ✅→중복 | 개념 자체는 실존. 단 `wiki/concepts/dspy.md` 2026-06-29 이미 작성됨 → 오늘 인사이트 제외 |
| Reasoning Effort Low/Medium/High | ✅→중복 | 실존(OpenAI reasoning_effort / Anthropic budget_tokens). 2026-06-26 위키 이미 기록됨 → 제외 |
| DeepEval + Braintrust | ✅→부분신규 | 도구 자체는 2026-06-24 메모리에 있음. 단 **역할 분리(개발/CI ↔ 프로덕션 관측)** 구분은 미기록 → 채택 |
| Structure-Aware Chunking + Reranking | ✅ 신규 | confident-ai.com 실존, RAG 기술 문서에서 확인 가능. 위키 미기록 |
| Semantic Caching | ✅ 신규 | 벡터 유사도 기반 LLM 응답 캐시 기법, 실존. 위키 미기록 |
| Agentic AI 전환 트렌드 | 역할 무관 | 검증 담당 역할에 직접적 실무 가치 낮음 → 제외 |

---

## 오늘 배운 것

- **Structure-Aware Chunking + Reranking (모듈형 RAG)**: RAG 파이프라인에서 고정 크기 텍스트 분할 대신 문서 구조(섹션·표·코드 블록)를 인식해 분할하고, 검색 후 Cross-Encoder로 재순위를 매겨 관련도를 높이는 기법. 테스트용 RAG 검색 파이프라인 품질 검증 시 chunking 전략을 assertion 항목에 포함할 수 있음. — 출처: confident-ai.com(DeepEval 공식)

- **Semantic Caching**: 동일하지 않아도 의미적으로 유사한 쿼리에 벡터 검색으로 이전 LLM 응답을 재사용해 API 호출을 생략하는 기법. LLM 기반 테스트(LLM-as-Judge)의 반복 실행 비용을 줄이는 데 직접 적용 가능. 단 캐시 히트 시 신선도 검증(freshness assertion) 우회 가능성을 별도로 테스트해야 함. — 출처: confident-ai.com

- **DeepEval(개발/CI) ↔ Braintrust(프로덕션 관측) 역할 분리**: 기존 메모리에는 두 도구가 병기만 돼 있음. 실제 운용 구분은 DeepEval = 오프라인·pre-merge 자동 평가(Evals-as-CI), Braintrust = 배포 후 트레이스·피드백 루프 분석. Regression CI Gate 설계 시 두 계층을 명시적으로 분리해야 함. — 출처: braintrust.dev

## 출처

- [DeepEval / Confident AI 공식 문서](https://confident-ai.com)
- [Braintrust 공식](https://braintrust.dev)

## 위키화 후보

- `semantic-caching.md` — LLM 파이프라인 시맨틱 캐싱 개념·적용 패턴·테스트 주의사항 1페이지 노트

## 프로필 반영 후보 (저위험)

- **Structure-Aware Chunking** — RAG 파이프라인 검증 체크리스트에 chunking 전략 검증 항목 추가

## 승인 필요 (고위험)

없음

## 신규 도구 후보

없음 (Promptfoo 인수 주장 폐기로 신규 도입 근거 소멸, 기존 Promptfoo 게이트는 이미 2026-06-24 메모리에 등록됨)

---

> **폐기 요약**: Promptfoo OpenAI 인수 — 교차 출처 없음, 채택 불가. GEPA DSPy 옵티마이저 — 공식 문서 미확인, 채택 불가.
