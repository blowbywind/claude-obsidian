---
date: 2026-06-28
bot: haeri
type: web-research
tags: [self-learning, ML/AI advances, data pipeline patterns, prompt engineering]
---

# 해리 자가학습 — 2026-06-28

위키 교차검증 완료. 출처별 신뢰도 분석 후 항목을 선별한다.

---

**폐기 목록 (이유 명시):**
- **Context Engineering / Loop Engineering** → Context Engineering은 `wiki/concepts/context-engineering.md` 중복. Loop Engineering은 출처가 `medium.com` 도메인만 있고 특정 기사 URL 없음 — 검증 불가.
- **DeepEval / Braintrust 이원화** → `2026-06-24-haeri-learning.md`에 Regression CI Gate로 이미 등록. 중복.
- **OWASP Agentic AI Top 10 CI Gate** → `2026-06-25-kiel-learning.md`에 "OWASP ASI Top 10"으로 등록. 중복이며 연구 결과의 명칭("Agentic AI Top 10")도 위키 기준("ASI Top 10")과 불일치.
- **LLM Stubbing (tigera.io)** → Tigera는 Kubernetes 네트워크 보안(Calico) 전문 벤더. LLM 테스트 패턴 출처로 도메인 불일치 — 신뢰 불가, 폐기.
- **Tolerance Bands (aiml.qa)** → `aiml.qa` 도메인 검증 불가, 출처 불신 — 폐기.

---

## 오늘 배운 것

- **HLE(Humanity's Last Exam) 벤치마크 부상** — MMLU 등 기존 벤치마크가 포화 상태에 이르자 대학원 수준 다분야 지식 + 인터넷 검색 차단(anti-memorization) 설계의 약 2,500문항 HLE가 프론티어 모델 변별 지표로 대두. 에이전트 성능 평가 기준 선정 시 참조.
- **데이터 파이프라인 Shift-Left 검증** — 실행 여부 모니터링을 넘어 수집(ingestion)·변환(transformation) 단계에 스키마 검증, 비즈니스 규칙, 분포 이상탐지(anomaly detection) assertion을 선제 배치하여 무성 오류(silent failure)를 차단. 기존 메모리의 row count / null rate / freshness 3종 체크리스트에 스키마·이상탐지 항목을 추가하는 근거.
- **PyRIT — Microsoft 에이전트 레드팀 도구** — Promptfoo(CI/CD 통합) + Garak(모델 취약점 탐지)의 기존 2종 체계에 PyRIT(다회차 시나리오 기반 공격)를 추가하여 3층 레드팀 편대 구성. PyRIT는 대화 흐름 전반에 걸친 복합 공격 시나리오를 자동화하는 데 특화.

## 출처

- [Humanity's Last Exam — Wikipedia](https://en.wikipedia.org/wiki/Humanity%27s_Last_Exam)
- [Promptfoo Red Teaming Docs](https://promptfoo.dev)

## 위키화 후보

- `wiki/concepts/pyrit.md` — Microsoft PyRIT 개요, Promptfoo·Garak과의 역할 분담, 다회차 시나리오 공격 패턴
- `wiki/concepts/hle-benchmark.md` — HLE 설계 원리(anti-memorization), 기존 벤치마크 대비 차별점, 프론티어 평가 맥락

## 프로필 반영 후보 (저위험)

- 레드팀 레퍼토리 업데이트: 기존 "Garak·Promptfoo 2종" → "Promptfoo(CI gate) + Garak(모델 취약점) + PyRIT(다회차 시나리오) 3층 편대"로 기술 목록 확장
- 데이터 파이프라인 assertion 체크리스트 확장: 기존 row count / null rate / freshness에 **스키마 검증 + 분포 이상탐지** 2항목 추가

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보 (에이전트/스킬)

(없음 — PyRIT는 기존 레퍼토리 확장이며 별도 스킬/에이전트 단위가 아님)
