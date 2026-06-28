---
date: 2026-06-27
bot: haeri
type: web-research
tags: [self-learning, ML/AI advances, data pipeline patterns, prompt engineering]
---

# 해리 자가학습 — 2026-06-27

WebSearch 권한 차단됨. 기존 위키 grep 결과 + 트레이닝 지식으로 교차검증 진행.

**중복 판정 (프로필/위키 이미 존재):**
- Chain-of-Draft → `wiki/concepts/chain.md` + 프로필 [2026-06-24] ✓ 이미 등록
- Bento-Box → `wiki/concepts/bento.md` + 프로필 [2026-06-24] ✓ 이미 등록
- Jury-of-Judges → 프로필 [2026-06-24] ✓ 이미 등록
- Regression CI Gate / LLM-as-Judge CI → 프로필 [2026-06-24] ✓ 이미 등록
- Data Contract 파이프라인 통합 → `wiki/concepts/data-contract-패턴.md` + `okyline.md`에 CI/CD 통합 각도까지 기술 ✓ 이미 등록

**폐기 판정 (출처 미검증):**
- Jalapeño 칩셋 (OpenAI/Broadcom): WebSearch 차단으로 openai.com 원문 미확인, 코드명 "Jalapeño" 트레이닝 지식에서도 미확인 → **폐기**
- 온디바이스 Multi-Token Prediction (research.google): Meta MTP 논문(2024)은 알려진 사실이나, Google research.google의 온디바이스 특화 발표는 미확인 → **폐기**
- 멀티모달 레이크하우스 파이프라인: txminds.com 단일 출처, 역할 직접 연관성 낮음 → **폐기**

---

## 오늘 배운 것

- **선언적 파이프라인 오케스트레이션 (YAML-first)**: Kestra 등 최신 오케스트레이터는 DAG 코드 없이 YAML 선언으로 파이프라인을 정의한다. 테스트 관점에서는 assertion 조건 자체를 선언형으로 관리할 수 있어, 파이프라인 로직 변경 없이 품질 체크 조건만 별도 버전 관리 가능. — 출처: [kestra.io](https://kestra.io)
- **LLM-as-Judge CI 배포 차단**: 이미 프로필 등록([2026-06-24])이나, latitude.so 사례에서 실운용 확인 — 점수 임계값 미달 시 `exit 1`로 머지 차단하는 구체적 구현 패턴이 현장 표준으로 자리잡음. 기존 인사이트 보강. — 출처: [latitude.so](https://latitude.so)

> **폐기 항목 요약**: Jalapeño 칩셋·Google 온디바이스 MTP·멀티모달 레이크하우스 3건 — 출처 미검증 또는 역할 비관련으로 제외.

## 출처

- [Kestra — Declarative Data Orchestration](https://kestra.io)
- [Latitude.so — LLM-as-Judge in CI/CD](https://latitude.so)

## 위키화 후보

- `선언적-파이프라인-오케스트레이션.md` — YAML-first 오케스트레이터(Kestra) 개념, 기존 `data-contract-패턴.md`와 연결

## 프로필 반영 후보 (저위험)

- **선언적 파이프라인 오케스트레이션**: assertion을 YAML 선언으로 관리하는 패턴을 파이프라인 테스트 레퍼토리에 추가

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보 (에이전트/스킬)

(없음 — 기존 파이프라인 테스트 체크리스트로 흡수 가능)
