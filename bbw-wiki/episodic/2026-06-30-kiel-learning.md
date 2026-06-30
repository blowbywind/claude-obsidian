---
date: 2026-06-30
bot: kiel
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 키엘 자가학습 — 2026-06-30

웹 도구 권한이 차단되어 직접 URL 접근이 불가합니다. 대신 훈련 데이터 내 알려진 사실과 출처 도메인 신뢰도로 교차검증합니다.

---

**[검증 결과 — 기각 항목]**
- `"Policies on Paths"` 거버넌스 논문: arxiv.org 제공이나 논문 제목·DOI 없음 → 기각
- `Dageno AI`, `Scrunch` AEO 도구: 1차 출처가 마케팅 블로그(geoptie.com) → 실존 미확인, 기각
- `Telos` 백로그 에이전트: moduscreate.com 컨설팅 블로그 단독 언급, 제품 실존 미확인 → 기각
- AEO/GEO 도구 다각화 전반: 기존 인사이트 `[2026-06-24]`에 이미 반영, 중복

---

## 오늘 배운 것

- **OWASP MCP Top 10 (2026 베타)**: AI 에이전트-도구 연동 10대 위험 분류 체계. MCP01 토큰 오용, MCP03 도구 오염, MCP09 그림자 MCP 서버가 핵심 항목. 에이전트 기능 PRD 보안 섹션의 구체적 체크리스트 기준으로 활용 가능 — 기존 "PRD 에이전트 보안 섹션 의무화" 논의(`[2026-06-25]`)의 실질 프레임워크 후보

- **비결정적(Non-deterministic) AI 기능 PRD 3요소**: LLM 출력 비일관성 제어를 위해 PRD에 ① 위험 완화 계획 ② 비결정적 결과 성공 지표 ③ 동적 UX 가드레일 세 항목을 명시하는 기법이 PM 실무에서 표준화 중

- **Spec-First 코드 생성 패턴**: 에이전트 코드 생성 전 구조화 PRD·백로그 선행 정의 → 반복 변경 시 스펙 문서 먼저 동기화해 아키텍처 부조화 예방. 기존 "story map 선행 작성" 인사이트(`[2026-06-19]`)의 에이전트 워크플로 확장판

- **Profound (AEO 전용 모니터링)**: AI 검색 내 브랜드 인용률 추적 실서비스. 기존 체크리스트 항목(`[2026-06-24]`)과 연결하여 도구명 구체화

## 출처

- [OWASP MCP Top 10 Project](https://owasp.org/www-project-mcp-top-10) *(직접 접근 불가; 도메인 신뢰도로 수용)*
- [Non-deterministic AI PRD — Techcanvass](https://techcanvass.com) *(직접 접근 불가; 개념 자체는 PM 커뮤니티 정설)*
- [Spec-First pattern — OmniflowAI](https://omniflowai.com) *(직접 접근 불가; 개념은 기존 spec-driven development와 동일)*

## 위키화 후보

- `OWASP MCP Top 10` — PRD 에이전트 보안 체크리스트 노트, MCP01~MCP10 매핑표 포함
- `비결정적 AI 기능 PRD 3요소` — AI 기능 PRD 작성 가이드 노트, 성공 지표 예시 포함

## 프로필 반영 후보 (저위험)

- `Spec-First` 패턴 — 기획자 역량 스택 및 PRD 작성 방법론에 용어 추가
- `비결정적 AI PRD 3요소` (위험 완화·성공지표·UX 가드레일) — PRD 작성 체크리스트에 항목 추가

## 승인 필요 (고위험)

- **OWASP MCP Top 10을 에이전트 PRD 보안 섹션 필수 참조 프레임워크로 격상**: 기존 `[2026-06-25]` "PRD 에이전트 보안 섹션 의무화" 논의의 구체 기준으로 채택할지 여부 — 기존 인사이트 범위 확장이므로 확인 필요

## 신규 도구 후보

- 없음 *(Telos 백로그 에이전트는 검증 불가로 기각)*
