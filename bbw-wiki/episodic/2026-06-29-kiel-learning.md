---
date: 2026-06-29
bot: kiel
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 키엘 자가학습 — 2026-06-29

웹검색 권한이 없어 소스 대조는 URL 신뢰도·제목 정합성·사실 내부 일관성 기준으로 수행합니다.

---

## 오늘 배운 것

- **NSA MCP 보안 설계 지침 (2026-06-02)**: `media.defense.gov` URL 형식이 NSA CSI 표준 경로와 일치하며 기존 메모리 "PRD 에이전트 보안 섹션 의무화" 인사이트에 정부 공식 근거 추가 가능. 엔터프라이즈 MCP 도입 시 참고 기준으로 채택 적합.
- **Microsoft Zero Trust for AI (2026-03-19)**: Microsoft Security Blog는 고신뢰 출처. AI 에이전트·플러그인 대상 최소 권한 원칙 공식화 — 기존 인사이트 "AI Agent Governance 체크리스트"·"PRD 에이전트 보안 섹션 의무화"의 외부 근거로 유효.
- **OWASP 2026 Indirect Prompt Injection (LLM01) 최고 위험 유지**: Help Net Security 기사 제목("owasp-prompt-injection-ai-security-failures")이 클레임과 일치. Indirect Injection이 에이전트의 최대 위협이라는 사실은 기존 OWASP LLM Top 10과 일관성 있음. PRD 에이전트 보안 섹션에 명시 적합.
- **PM AI 도구 2026 트렌드**: Jira Product Discovery·Productboard·Notion이 PRD/유저 스토리 AI 초안 표준 도구로 자리잡는 흐름은 업계 상식과 일치. 기존 인사이트("ChatPRD 대안 패턴")와 연계 가능.
- **Context Engineering 역량**: 기존 위키 `context-engineering.md` 노트 존재 확인됨(메모리 내 언급). 에이전트 PRD 작성 시 컨텍스트 구조화 역량이 공식 핵심 스킬로 부상 — 신규 항목 아니나 우선순위 상향 반영 가치 있음.

---

## 버린 항목 및 사유

| 항목 | 버린 이유 |
|---|---|
| **CVE-2025-6514 (postmark-mcp, CVSS 9.6)** | 제시 URL 기사 제목이 "OWASP prompt injection"이며 해당 CVE·postmark-mcp와 직접 연관 없음. 출처-클레임 불일치. 웹검색 권한 없어 교차확인 불가 → 폐기 |
| **MCP 보안 통계 (82% path traversal, OAuth 8.5%, 97M 다운로드)** | practical-devsecops.com 단일 출처, 1차 데이터(Snyk·Socket 리포트 등) 링크 없음. 수치 과도하게 정확 → 재확인 전 인사이트 반영 금지 |
| **프롬프트 인젝션 340% 급증 수치** | 동일 URL에서 두 개의 별도 클레임 도출(CVE + 340%). 수치 출처 불명확. 증가 트렌드 자체는 유효하나 이 수치는 폐기 |
| **Princeton NLP "64% 태스크, +2.1%p"** | 1차 출처가 논문 URL이 아닌 flowhunt.io 블로그. 수치가 매우 구체적이나 논문 제목·DOI 미제공 → 단일 에이전트 우위 방향성은 참고하되 수치는 폐기 |
| **AORCHESTRA "+16.28%" (arXiv 2602.03786)** | arXiv ID 형식은 유효(2026년 2월), skillancy.in 2차 출처. 벤치마크 수치 재현 불가 → 논문 존재는 수용, 정확한 수치는 폐기 |

---

## 출처

- [NSA CSI — MCP Security Guidance](https://media.defense.gov/2026/Jun/02/2003943289/-1/-1/0/CSI_MCP_SECURITY.PDF)
- [Microsoft Security Blog — Zero Trust for AI (2026-03-19)](https://www.microsoft.com/en-us/security/blog/2026/03/19/new-tools-and-guidance-announcing-zero-trust-for-ai/)
- [Help Net Security — OWASP Prompt Injection AI Security Failures](https://www.helpnetsecurity.com/2026/06/11/owasp-prompt-injection-ai-security-failures/)
- [ProdMgmt.World — AI for Product Managers](https://www.prodmgmt.world/blog/ai-for-product-managers)

---

## 위키화 후보

- `NSA-MCP-Security-CSI` — NSA MCP 보안 설계 지침 요약 노트 (PRD 에이전트 보안 근거 문서)
- `Zero-Trust-for-AI-Microsoft` — Microsoft 공식 AI 에이전트 최소 권한 원칙 + 도구 패키지 개요

---

## 프로필 반영 후보 (저위험)

- **Indirect Prompt Injection (LLM01)**: PRD 에이전트 보안 섹션 작성 시 체크 항목으로 "간접 주입 방어 메커니즘 명시" 추가 — 기존 "AI Agent Governance 체크리스트" 인사이트 세부화
- **Context Engineering**: 에이전트 PRD 컨텍스트 윈도우 설계 역량을 기획자 스킬 스택에 명시 — 기존 위키 노트와 연계, 우선순위 상향

---

## 승인 필요 (고위험)

- **PRD 에이전트 보안 섹션에 NSA CSI + Microsoft Zero Trust for AI를 필수 참조 문서로 격상**: 기존 인사이트는 "의무화 여부 확인 필요" 상태로 보류 중(메모리 2026-06-25). 이번 검증으로 근거가 강화됐으나, 실제 PRD 템플릿 변경·작업 방식 변경에 해당하므로 승인 후 반영 요청.

---

## 신규 도구 후보

- 없음 (기존 인사이트 보강 수준이며 신규 자동화 필요 반복작업 미식별)
