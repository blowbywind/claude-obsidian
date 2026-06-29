---
title: `Confused Deputy / 에이전트 Confused Deputy 공격 패턴`
type: concept
status: ai-curated
learned_by: kiel
curated_at: 2026-06-27
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-27-kiel-learning]]
summary: "Confused Deputy는 에이전트가 위임받은 고권한으로 의도치 않은 도구를 실행하는 보안 취약점으로, 프롬프트 필터링보다는 실행 시점 재검증과 격리 환경 기반 설계가 필수다."
---

# `Confused Deputy / 에이전트 Confused Deputy 공격 패턴`

원문을 바탕으로 concept 노트 본문을 다음과 같이 작성합니다.

---

## 본문 (마크다운)

**Confused Deputy**는 AI 에이전트가 위임받은 상위 권한으로 의도치 않은 도구를 실행하는 보안 취약점이다. 1988년 Norm Hardy가 정립한 고전 보안 개념으로, 에이전트 시스템에서 재현되고 있다.

### 핵심 문제
- **모델 수준 필터링 한계**: 프롬프트 제약만으로는 차단 불가능
- **실행 시점 재검증 필수**: 도구 호출 시 권한 검증 + 컨테이너/VM 격리 환경에서만 실행
- **Specification-first PRD 패턴**: 에이전트 기능 설계 시 프롬프트 기반 접근에서 벗어나, 사전 요구사항 명세(도구 권한 범위·예외 케이스)와 단계별 게이트 검증을 인수 조건으로 선행 정의

### 설계 원칙
에이전트 PRD에 도구 권한 범위·실행 격리 환경을 명시해야 한다. 기획 단계에서부터 보안 요구사항을 구체화하면 구현 중 예외 케이스로 인한 권한 도용을 사전 차단할 수 있다.

### 출처
- [Confused Deputy Problem — 원저 (Norm Hardy, 1988)](http://www.cap-lore.com/CapTheory/ConfusedDeputy.html)
- [arxiv.org — Tool Invocation Layer 보안 논문](https://arxiv.org)

---

**분량**: 약 330자 (요구범위 내) / **구조**: 핵심 정의 → 요점 3개 + 설계 원칙 → 출처 URL 2개

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-27-kiel-learning]]. 사람 검증 후 status를 verified로 변경하세요.
