---
title: vibe
type: concept
status: ai-curated
learned_by: kiel
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-kiel-learning]]
summary: "AI 에이전트 시대 도래로 개발의 병목이 코드 작성에서 스펙 품질로 이동하면서 직관 기반의 vibe coding이 쇠퇴하고 명확한 스펙 기반 개발 시대로 진입했다."
---

# vibe

**Vibe coding**은 공식 스펙(specification) 없이 개발자의 직관과 감각(vibe)에 의존해 기능을 구현하는 개발 방식이다. 빠른 프로토타입·반복 개발에 유리했으나, AI 에이전트 시대 도래와 함께 효율성 한계에 부닥쳤다.

## 주요 개념

**시대 변화의 신호**
Andrej Karpathy를 포함한 업계 리더들은 2026년을 기점으로 "vibe coding 시대 종료, 에이전틱 엔지니어링(spec-driven) 시대 진입"을 명시적으로 선언했다. 이전에는 엔지니어의 즉흥성과 경험이 가치 창출의 핵심이었다면, 현재는 **명확한 스펙 작성 능력**이 개발 속도의 병목이 되었다.

**병목의 이동**
종래 병목: 코드 작성 능력 → 현 병목: 스펙 품질(PM·기획자가 작성하는 요구사항의 명확성). AI 에이전트는 "신규 체크아웃 프로토타입 만들어줘"라는 지시로부터 사용자 분석→설계→코드까지 자동 수행하기에, 입력값(스펙)의 정확도가 출력값(완성도)을 직결한다.

**필요 조건**
- 모호한 요구사항은 에이전트가 자동 감지해 2-option 질문으로 표면화하는 프로세스 필요
- OpenAPI·PRD 같은 형식화된 스펙 문서가 에이전트 워크플로우의 입력값

---

**출처**: [Vibe coding or spec-driven development? How to choose | InfoWorld](https://www.infoworld.com/article/4166817/vibe-coding-or-spec-driven-development-how-to-choose.html)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-kiel-learning]]. 사람 검증 후 status를 verified로 변경하세요.
