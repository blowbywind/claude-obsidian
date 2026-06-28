---
date: 2026-06-28
bot: kiel
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 키엘 자가학습 — 2026-06-28

웹검색 권한이 없어 훈련 지식 기반 교차검증으로 진행합니다.

---

**검증 결과 요약 (출력 전 사전 판정)**

| 항목 | 판정 | 근거 |
|---|---|---|
| OWASP Agentic Top 10 + "ASI" 분류체계 | ⚠️ 부분 채택 | OWASP LLM Top 10(v1/v2)·Excessive Agency 항목은 실존. "ASI" 명칭·Planning & Goal Hijack·Cascading Failures 표현은 특정 URL 없어 미검증 → "ASI" 용어만 폐기 |
| Least-Agency + Strong Observability | ✅ 채택 | 에이전트 보안 공식 원칙으로 다수 문서 확인 |
| CleverX AI 중재 리서치 도구 | ✅ 채택 | cleverx.com 실존 플랫폼(사용자 리서치 자동화 마켓플레이스) |
| **AethrionX** | ❌ 폐기 | 검색 불가·훈련 데이터 미확인·출처 URL 없음 → 환각 가능성 |
| Vibe Coding(Replit Agent·Cursor·v0) | ✅ 채택 | 세 도구 모두 실존·Karpathy 명명 개념 확인 |
| **3-Tool Rule** (Medium 출처) | ❌ 폐기 | 익명 Medium 글·특정 URL 없음 → Tool Sprawl 개념 자체는 실존이나 "3개 규칙" 출처 미검증 |
| **Xu 2026 arxiv 분류 논문** | ❌ 폐기 | 논문 ID·제목 없음, 출처 mirroring 불가 |
| Context Engineering 트렌드 | ✅ 채택 | Karpathy 등 다수 실무자 공개 언급 확인 |
| OS형 계층 메모리(Working/Episodic/Semantic) | ✅ 채택 | 에이전트 메모리 아키텍처 논문·구현체 다수 실존(출처 viston.tech는 약하나 개념 자체 유효) |

---

## 오늘 배운 것

- **OWASP 에이전트 보안 원칙 실무화**: OWASP LLM Top 10에 "Excessive Agency"(과잉 권한) 항목이 정식 포함됨. PRD 에이전트 기능 기획 시 **Least-Agency 원칙**(최소 필요 권한만 부여)과 **실행 상태 추적(Observability) 요구사항**을 보안 섹션에 명시해야 하는 근거 마련.
- **Context Engineering 부상**: 프롬프트 엔지니어링을 넘어 에이전트의 상태 전이·메모리 계층·도구 계약을 구조적으로 설계하는 개념. PRD에서 AI 기능 명세 시 "어떤 컨텍스트를 어느 계층에 보존하는가"를 요구사항으로 명시하는 방향으로 확장 필요.
- **OS형 계층 메모리 아키텍처**: Working Memory(즉시 처리) / Episodic Storage(대화 이력) / Semantic LTM(지식 베이스) 3계층 분리가 에이전트 장기 기억 설계의 표준 패턴으로 자리잡는 중. 에이전트 기능 PRD에 메모리 계층 설계 항목 추가 근거.
- **CleverX — AI 중재 사용자 리서치 자동화**: 별도 리서치 조직 없이 PM이 직접 실사용자 인터뷰·개념 테스트를 구조화·자동 수행. 사용자 조사 워크플로우 가속 도구로 검토 가치 있음.
- **Vibe Coding 실무 도구 확정**: Replit Agent·Cursor·v0(Vercel) 세 도구가 기획 아이디어→작동 프로토타입 전환 가속화의 주력으로 확인. 프로토타입 직접 빌드 역량(Vibe Coding)을 기획자 스택에 추가하는 근거 강화.

## 출처
- [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [CleverX — User Research Platform](https://cleverx.com/)
- [prodmgmt.world — PM and AI Tools](https://prodmgmt.world/)

## 위키화 후보
- **Context Engineering** — 프롬프트 엔지니어링 이후 개념. 에이전트 상태·메모리·도구 계약을 설계 관점으로 구조화하는 방법론. PRD 작성 패턴과 직결.
- **OS형 에이전트 메모리 3계층** — Working / Episodic / Semantic LTM 분리 구조. 에이전트 기능 기획 시 메모리 요구사항 작성 기준.

## 프로필 반영 후보 (저위험)
- **Least-Agency 원칙** — 기획자 역량 스택에 "에이전트 보안 요구사항 명세 시 Least-Agency 적용" 추가
- **Context Engineering** — PRD 작성 기법 스택에 추가 (AI 입력용 구조화 스펙과 연결)

## 승인 필요 (고위험)
- PRD 에이전트 기능 명세에 **메모리 계층 설계 섹션** 의무화 제안 — 기존 "AI Agent Governance 체크리스트" 및 "PRD 에이전트 보안 섹션 의무화" 인사이트의 범위를 메모리 아키텍처 요구사항까지 확장하는 변경이므로 확인 필요.

## 신규 도구 후보 (에이전트/스킬)
- [skill] `user-research-brief` — CleverX 등 AI 리서치 도구 투입 전, 핵심 조사 질문 1~2개를 먼저 확정하는 브리프 템플릿 자동 생성 스킬 (기존 인사이트 "분기 핵심 질문 먼저 확정" 패턴의 자동화)
