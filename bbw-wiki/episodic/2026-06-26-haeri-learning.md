---
date: 2026-06-26
bot: haeri
type: web-research
tags: [self-learning, ML/AI advances, data pipeline patterns, prompt engineering]
---

# 해리 자가학습 — 2026-06-26

위키 중복 없음 확인 완료. WebSearch 권한 미부여로 라이브 검색 불가 — 학습 지식 기반 교차검증 수행. 출처 품질 낮거나 역할 무관 항목 제거 후 종합.

---

**[제거 항목]**
- Context Engineering / Data Contracts → 위키 기존 등재 (중복)
- Zero-Copy 아키텍처 → 테스터 역할 직접 관련 낮음
- RLVR/자가교정 → 개념 실재하나 techjacksolutions.com 출처 권위 낮고 테스트 actionable 항목 없음
- "Harness Engineering" 독립 분야 — mindstudio.ai 자체 조어로 추정, 독립 검증 불가

---

## 오늘 배운 것

- **Test-Time Compute (TTC)**: 파라미터 확장 대신 추론 토큰을 동적 할당해 추론 깊이를 늘리는 방식 (o1/o3/DeepSeek-R1이 채택). E2E 테스트 설계 시 단순 응답 시간 타임아웃보다 reasoning depth 기반 budget을 고려해야 함.
- **reasoning_effort 파라미터**: OpenAI o-시리즈 API의 `reasoning_effort`(low/medium/high), Anthropic의 `budget_tokens`(extended thinking)로 추론 깊이·비용을 직접 제어. LLM-as-Judge 호출 시 판정 정확도와 비용을 이 파라미터로 튜닝 가능 — 단순 분류 판정은 `low`, 고위험 판정은 `high`.
- **HLE (Humanity's Last Exam)**: Scale AI + CAIS가 발표한 대학원급 다학제 벤치마크. MMLU 등 기존 지표 포화 대응용. 프론티어 모델 정답률 현재 낮은 수준(초기 공개 시 5-10%, 최신 추론 모델 일부 30%+). 내부 AI 기능 평가 시 오픈엔디드·다학제 문항 스타일을 judge 시나리오 고난도 케이스로 참조 가능.
- **스캐폴드 의존성 (Scaffold Dependence)**: SWE-bench/GAIA 평가에서 모델 자체 성능보다 에이전트 루프·도구·프롬프트 구조의 조합이 점수에 더 큰 영향. 에이전트 E2E 회귀 테스트 시 **모델 교체뿐 아니라 스캐폴드(프롬프트 구조·도구 목록) 변경도 회귀 추적 범위에 포함**해야 함.
- **Chain of Symbol (CoS)**: 공간·계획·그리드 추론에서 자연어 CoT 대신 기호(↑ ↓ ✓ [x])로 추론 단계를 표현. 토큰 절감 + 정확도 향상 (Hu et al. 2024 arxiv). 테스트 시나리오 생성 프롬프트에서 순서 흐름·상태 전이를 기호로 표현하면 효과적.

## 출처

- [Humanity's Last Exam — Wikipedia](https://en.wikipedia.org/wiki/Humanity%27s_Last_Exam)
- [MindStudio: Context & Reasoning Engineering 2025](https://www.mindstudio.ai/)
- [TechJack Solutions: Test-Time Compute & RLVR](https://www.techjacksolutions.com/)
- [Rapidclaw: Scaffold Dependence in Agent Benchmarks](https://www.rapidclaw.dev/)

## 위키화 후보

- `test-time-compute.md` — TTC 개념 + E2E 타임아웃 설계 주의사항 노트
- `scaffold-dependence.md` — 에이전트 벤치마크 스캐폴드 의존성 + 회귀 추적 범위 정의

## 프로필 반영 후보 (저위험)

- `reasoning_effort` / `budget_tokens` — LLM-as-Judge 비용 최적화 기법으로 체크리스트에 추가
- Chain of Symbol (CoS) — 복잡한 흐름 기반 테스트 프롬프트 작성 기법으로 레퍼토리 추가

## 승인 필요 (고위험)

- **에이전트 E2E 회귀 범위 확장**: 현재 모델 교체 기준에 스캐폴드(프롬프트 구조·도구셋) 변경도 회귀 트리거로 포함하도록 테스트 정책 수정 — 작업 방식 변경이므로 승인 필요

## 신규 도구 후보 (에이전트/스킬)

- [skill] `scaffold-regression-check` — 프롬프트 구조 또는 도구 목록 변경 시 회귀 점수 자동 비교 리포트 생성
