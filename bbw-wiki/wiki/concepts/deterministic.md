---
title: deterministic
type: concept
status: ai-curated
learned_by: snow
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-snow-learning]]
---

# deterministic

마크다운 본문만 작성합니다. 원문에 기반한 정식 concept 노트입니다:

---

결정론적(Deterministic) 오케스트레이션은 다단계 워크플로의 분기와 라우팅을 명시적 규칙과 코드로 정의하는 방식이다. LLM이 매번 토큰을 소비하며 라우팅 결정을 내리는 대신, 정해진 로직에 따라 작업을 배분하고 정말 필요한 가변 결정 지점만 동적으로 위임한다.

**2026년 표준**: MS Agent Framework 1.0(2026년 4월 안정화)을 기준으로 순수 LLM 라우팅이 아닌 하이브리드 방식(결정론적 + 동적)이 프로덕션 정설로 정착했다. 오케스트레이션 로직을 코드로 정의하되 진짜로 가변적인 결정 지점만 동적 라우팅으로 한정한다.

**구체적 구현**: Microsoft의 오픈소스 Conductor는 멀티에이전트 워크플로를 YAML로 선언한다. 이를 통해 오케스트레이션 루프에서 LLM을 미개입 상태로 두고(라우팅 결정에 토큰 0), CI/CD 파이프라인처럼 차이를 추적 가능하게 관리한다.

**장점**: 토큰 비용 절감, 워크플로 투명성과 재현성 확보, 선언적 설계로 인한 유지보수성.

## 출처
- [Conductor: Deterministic orchestration for multi-agent AI workflows](https://opensource.microsoft.com/blog/2026/05/14/conductor)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-snow-learning]]. 사람 검증 후 status를 verified로 변경하세요.
