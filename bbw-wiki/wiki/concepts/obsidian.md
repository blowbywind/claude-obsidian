---
title: `obsidian
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-19-dex-learning]]
summary: "마크다운 기반 로컬 지식관리 플랫폼으로 네트워크형 노트 구조와 YAML frontmatter-first 설계, Bases/Dataview 이원화 데이터 관리, LLM 통합을 특징으로 한다."
---

# `obsidian

## 핵심 정의

Obsidian은 마크다운 기반의 개인 지식 관리(PKM) 플랫폼으로, 로컬 저장소 중심의 네트워크형 노트 구조를 지원합니다. 2025년 네이티브 데이터베이스 뷰인 "Bases"를 출시하면서 단순 필터·정렬은 Bases로, 복잡한 쿼리는 Dataview/Datacore 플러그인으로 구분 운영하는 이원화 전략이 표준화됐습니다.

## 주요 특징

**데이터 관리 계층화**: Obsidian Bases는 YAML 프로퍼티 기반 GUI 테이블로 동작하여 기존 Dataview 의존도를 낮춥니다. Datacore는 동일 개발자의 후속 작품으로 React 기반 2–10× 성능 개선을 제공합니다. 2026년 현실적 권장은 "지금 당장 Dataview 교체 금지, 단순 use case별 점진 전환"입니다.

**구조 건강성과 LLM 통합**: 링크 없는 고아 노트는 지식 그래프에서 단절되어 AI 에이전트 탐색을 방해합니다. YAML frontmatter에 `summary: 1-2줄` 추가(frontmatter-first 원칙)하면 LLM이 전체 파일 로드 없이 관련 노트를 선별할 수 있어 토큰 소비와 환각 확률이 감소합니다.

**컨텍스트 과부하 주의**: 그래프 검색 시 관련성 높은 소수 경로만 주입해야 LLM 응답 품질이 최대화됩니다. 과다한 서브그래프는 오히려 성능 저하를 초래합니다.

## 출처
- https://obsidian.rocks/dataview-vs-datacore-vs-obsidian-bases/
- https://medium.com/@michael.hannecke/frontmatter-first-is-not-optional-context-window-survival-for-local-llms-in-opencode-15809b207977
- https://aicompetence.org/ai-enhanced-personal-knowledge-graphs/
- https://medium.com/@theo-james/ai-graph-based-personal-knowledge-management-c0e09ac55654

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-19-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
