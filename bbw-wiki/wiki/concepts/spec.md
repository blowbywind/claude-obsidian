---
title: Spec
type: concept
status: ai-curated
learned_by: kiel
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-kiel-learning]]
summary: "기능·요구사항 정의로 개발 재작업 비용의 50~80%를 사전에 제거하는 명세 문서"
---

# Spec

## Spec 개념 노트 본문

**Spec(사양·명세)**는 제품 개발 과정에서 기능·API·요구사항의 구조화된 정의 문서다. 기획 단계에서 개발·검증으로 이어지는 전체 생명주기에서 재작업 비용을 결정하는 핵심 산출물이다.

### 요점

**1. 명세 품질과 재작업 비용의 관계**  
CMU SEI(2025) 데이터에 따르면 소프트웨어 개발 비용의 60~80%가 재작업에 소요되며, 요구사항 품질 개선으로 결함의 50~80%를 사전에 제거할 수 있다. 따라서 명세 작성 단계 투자는 후속 개발 비용을 대폭 절감한다.

**2. 요구사항 명세의 3요소 패턴**  
각 요구사항에 "(1) 어떤 전략 목표를 지원하는가, (2) 어떤 인사이트에 근거하는가, (3) 누가 관여하는가"를 명시하면 느낌 기반 우선순위 결정을 줄일 수 있다. IEEE 29148이 산업 표준.

**3. API 명세 자동 생성**  
StackHawk 같은 도구는 API 변경을 자동 감지해 OpenAPI 스펙을 재생성함으로써 명세서 유지 부담을 크게 감소시킨다.

**4. AI 기반 명세 생성 시 구조화된 프레임 필수**  
AI가 인수 조건이나 스토리를 생성할 때 스토리 맵·도메인 정의·제약조건·용어집을 함께 제공하면 초안 품질이 크게 향상된다.

### 출처

- https://www.uladshauchenka.com/p/how-to-write-a-good-product-requirements
- https://www.parallelhq.com/blog/how-to-write-product-requirements
- https://www.stackhawk.com/blog/openapi-spec-generation/
- https://storiesonboard.com/blog/ai-assisted-backlog-refinement-clear-user-stories

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-kiel-learning]]. 사람 검증 후 status를 verified로 변경하세요.
