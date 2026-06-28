---
title: AI vs 인간 테스트 이중 컨테이너 전략
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-haeri-learning]]
summary: "AI 자동 평가(오프라인/CI/온라인)와 인간 큐레이션으로 LLM 앱 품질을 이중 검증하는 전략."
---

# AI vs 인간 테스트 이중 컨테이너 전략

원문의 **Evals-as-CI 3점 라이프사이클**이 "AI vs 인간 테스트 이중 컨테이너"의 핵심 전략으로 해석되므로, 이를 기반으로 concept 노트를 작성하겠습니다:

---

## 핵심 정의

LLM 앱 품질 검증을 **자동화된 AI 평가**와 **인간 검증**의 이중 계층으로 운영하는 전략. 첫 번째 컨테이너(자동)는 오프라인 평가와 CI 파이프라인 내 회귀 검증을 담당하고, 두 번째 컨테이너(인간)는 프로덕션 트래픽 기반 연속 모니터링 및 큐레이션을 담당한다.

## 요점

**1. 3점 라이프사이클 구조**
- **Offline**: 큐레이션된 golden dataset 위에서 프롬프트·모델 변경을 검증(평가 실패 = 빌드 실패)
- **Pre-merge CI**: 모든 코드 변경마다 자동 실행 — 테스트 스위트와 동등 수준으로 취급
- **Online**: 프로덕션 트래픽 5~10% 샘플 기반 연속 평가로 드리프트 감지

**2. AI-기반 자동 검증 (첫 번째 컨테이너)**
- Garak, Promptfoo 등 red teaming 도구로 프롬프트 인젝션·탈옥·환각 자동 회귀
- Deterministic(포맷)→Rubric-based(LLM-as-Judge)→Composite(다중 지표) 3계층 평가로 신뢰도 확보

**3. 인간 검증 (두 번째 컨테이너)**
- 전문가 큐레이션 golden dataset: 자동 생성 데이터의 보완재로만 사용(대체 불가)
- Online 모니터링에서 이상 신호 감지 시 즉시 개입

## 출처

- [Best AI Eval Tools for CI/CD Pipelines — Braintrust](https://www.braintrust.dev/articles/best-ai-evals-tools-cicd-2025)
- [LLM Red Teaming Guide 2026 — AppSecSanta](https://appsecsanta.com/ai-security-tools/llm-red-teaming)
- [Automated LLM Red Teaming with Promptfoo — NVISO](https://blog.nviso.eu/2026/02/05/an-introduction-to-automated-llm-red-teaming/)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
