---
title: Tool
type: concept
status: ai-curated
learned_by: kiel
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-18-kiel-learning]]
summary: "LLM의 외부 상호작용을 구체화한 인터페이스로, tool-DC 패턴 정확화와 도메인별 전문 도구 선택으로 에이전트 역량을 극대화한다."
---

# Tool

**Tool**은 LLM의 역량을 특정 작업으로 구체화한 외부 시스템 또는 기능이다. API 호출, 데이터 검색, 외부 서비스 연계 등으로 에이전트가 실제 세계와 상호작용하게 한다.

## 핵심 특징

**1. Tool-DC 패턴** — LLM의 tool calling을 try→check→retry 루프로 구조화함으로써 에이전트의 정확성을 높인다. 이는 API 명세가 **에이전트 친화적으로 설계**되어야 함을 의미한다. 불명확한 인터페이스나 복잡한 파라미터는 에이전트의 호출 실패를 유발한다.

**2. 도메인별 도구 확대** — 2026년 현재 PRD 자동 생성(ChatPRD, Figma AI), DevOps 통합(Copilot4DevOps), 경쟁 분석(Crayon, Klue) 등 각 업무 영역에 전문화된 LLM 기반 도구가 등장하고 있다. 이들은 수동 문서화를 경쟁 열위 요소로 만들고 있다.

**3. 도구 선택의 원칙** — 단순히 도구 수집이 아닌, 분기당 1~2개 핵심 질문을 먼저 정의한 뒤 그에 맞는 도구를 선택하는 것이 PM 표준 실무다. 예: 경쟁 분석은 전문 CI(Crayon/Klue) + ad-hoc 합성(Claude/Perplexity) 조합으로 접근한다.

## 출처

- https://www.chatprd.ai/learn/prd-for-ai-codegen
- https://www.figma.com/solutions/ai-prd-generator/
- https://www.buildthisnow.com/blog/guide/mechanics/ai-research-june-2026
- https://cleverx.com/blog/10-best-ai-tools-for-competitive-analysis-in-2026-for-product-managers/
- https://www.figma.com/resource-library/ai-competitor-analysis-tools/

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-18-kiel-learning]]. 사람 검증 후 status를 verified로 변경하세요.
