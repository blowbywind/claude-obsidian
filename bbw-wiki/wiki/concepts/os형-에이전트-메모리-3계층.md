---
title: OS형 에이전트 메모리 3계층
type: concept
status: ai-curated
learned_by: kiel
curated_at: 2026-06-28
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-28-kiel-learning]]
summary: "에이전트 메모리를 Working, Episodic, Semantic 3계층으로 분리해 효율성과 상태 추적을 최적화하는 구조적 설계 패턴."
---

# OS형 에이전트 메모리 3계층

원문 기반으로 본문을 작성하겠습니다. 요청하신 구조(핵심 정의→요점→출처)에 맞춰 300~700자로 한국어로 작성하겠습니다.

**OS형 에이전트 메모리 3계층**

**핵심 정의**  
에이전트의 장기 기억을 구조적으로 관리하는 3계층 분리 모델. Working Memory(즉시 처리)·Episodic Storage(대화 이력)·Semantic LTM(지식 베이스)으로 기능을 구분하여 메모리 효율성과 상태 추적 능력을 높인 설계 패턴입니다.

**요점**
- **Working Memory**: 현재 작업 중인 컨텍스트와 즉시 필요한 상태 정보만 보유해 처리 속도 최적화
- **Episodic Storage**: 과거 대화·작업 이력을 시계열로 저장하여 맥락 복구 및 학습 재료 제공
- **Semantic LTM**: 반복되는 패턴·도메인 지식·룰셋을 구조화된 형태로 저장해 재사용성 극대화
- **PRD 적용**: 에이전트 기능 기획 시 메모리 계층 설계 항목을 보안·성능 요구사항에 명시해야 함

**출처**
- OWASP Top 10 for Large Language Model Applications: https://owasp.org/www-project-top-10-for-large-language-model-applications/
- Context Engineering 개념 (prodmgmt.world): https://prodmgmt.world/

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-28-kiel-learning]]. 사람 검증 후 status를 verified로 변경하세요.
