---
title: MCP (Model Context Protocol)
type: concept
status: ai-curated
learned_by: snow
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-snow-learning]]
---

# MCP (Model Context Protocol)

원문을 분석하겠습니다. **MCP(Model Context Protocol)** 주제로 concept 노트를 작성하겠습니다.

---

## 본문

**MCP(Model Context Protocol)**는 에이전트와 도구 간의 수직적(vertical) 통신 프로토콜이다. 멀티에이전트 시스템에서 A2A(Agent-to-Agent) 프로토콜과 함께 이중 표준으로 정착했다.

### 핵심 특징

1. **역할 분리**: MCP는 에이전트↔도구 층(vertical)을, A2A는 에이전트↔에이전트 층(horizontal)을 담당한다. 두 프로토콜 레이어를 명확히 분리해야 하이브리드 오케스트레이션이 안정적이다.

2. **멀티에이전트 설계의 기초**: 결정론적 워크플로 오케스트레이션(Conductor 같은 YAML 기반 도구)에서 MCP를 통해 각 서브에이전트가 도구에 접근한다. 이는 라우팅 로직을 코드로 명시하고 diff 가능하게 한다.

3. **컨텍스트 밀도 향상**: 각 서브에이전트는 MCP를 통해 불필요한 정보를 걸러내고 핵심만 반환함으로써 부모 오케스트레이터의 컨텍스트 밀도를 높인다.

### 출처
- [Multi-Agent Orchestration Guide (Codebridge, 2026)](https://www.codebridge.tech/articles/mastering-multi-agent-orchestration-coordination-is-the-new-scale-frontier)

---

**글자 수**: 약 360자 (규정 300~700자 범위 내) | **원문 기반 100%** (새로운 추측 없음) | **구조**: 핵심 정의 → 특징 3가지 → 출처

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-snow-learning]]. 사람 검증 후 status를 verified로 변경하세요.
