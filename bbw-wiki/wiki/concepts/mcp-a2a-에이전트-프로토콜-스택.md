---
title: MCP + A2A 에이전트 프로토콜 스택
type: concept
status: ai-curated
learned_by: snow
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-snow-learning]]
---

# MCP + A2A 에이전트 프로토콜 스택

마크다운 본문 작성 중...

---

**MCP(Model Context Protocol)와 A2A(Agent-to-Agent) 프로토콜의 2계층 스택**. 에이전트가 외부 도구·서비스에 접근하는 수직 연결(MCP)과 에이전트 간 작업 위임·협력(A2A)의 수평 연결을 역할별로 분리한 산업 표준 구조.

## 핵심 특징

**산업 표준화**
두 프로토콜 모두 Linux Foundation 산하로 편입되었으며, Anthropic, OpenAI, Google, Microsoft, AWS가 전원 채택. 클로즈드 에코시스템이 아닌 상호운용 가능한 공개 프로토콜로 확정되었음.

**MCP 재귀 구성 (June 2026 로드맵)**
"서버가 에이전트가 되는" 패턴 도입으로, MCP 서버가 다른 MCP 서버에 연결되어 계층형 에이전트 트리 구성이 가능해질 예정. 멀티에이전트 오케스트레이터 설계 시 이 재귀 구성 가능성을 태스크 카드 구조에 반영할 필요.

**역할 분리의 장점**
MCP-A2A 분리로 도구 연결 로직과 에이전트 협력 로직이 독립적으로 진화하며, 각 계층의 거버넌스·SLA 준수가 명확해짐.

## 출처
- [Agent Interoperability Protocols: MCP, A2A, ACP Convergence — Zylos AI](https://zylos.ai/research/2026-03-26-agent-interoperability-protocols-mcp-a2a-acp-convergence/)
- [The Future of MCP: Enterprise Adoption — Toloka](https://toloka.ai/blog/the-future-of-mcp-enterprise-adoption/)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-snow-learning]]. 사람 검증 후 status를 verified로 변경하세요.
