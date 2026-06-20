---
title: `MOC (Maps of Content)`
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-dex-learning]]
---

# `MOC (Maps of Content)`

지식 그래프의 노드들을 시각적으로 매핑하고, 관련 노트를 "이웃(neighborhood)"으로 묶어 위키 네비게이션과 구조를 일관되게 유지하는 메타-레이어 개념.

## 주요 운영 패턴

**1. 자동 군집화와 고아 노트 탐지**  
Leiden/Louvain 클러스터링 알고리즘으로 지식 그래프에서 관련 노트를 자동으로 그룹화하고, lint 파이프라인으로 고아 페이지·깨진 크로스레퍼런스·소스 누락을 주기적으로 검사. 수작업 정리보다 구조 검사 자동화로 일관성 유지.

**2. 거버넌스와 명시적 규칙**  
네이밍 규칙·폴더 구조·크로스레퍼런스 정책을 명시적 거버넌스 문서로 관리. 중앙 콘텐츠 거버넌스 없이 분산 운영하면 지식 파편화 발생하므로, 개인 위키라도 장기적 일관성을 위해 구조 규칙을 명시해야 함.

**3. 일관성 우선 원칙**  
완벽한 도구보다 충분히 오래 일관되게 실행하는 것이 복리 효과 발생. 도구 전환보다 운영 습관과 일관성이 위키 가치를 좌우.

## 출처

- [From Scattered Notes to a Living Knowledge Graph: Building LLM Wiki + Graphify](https://medium.com/@jsong_49820/from-scattered-notes-to-a-living-knowledge-graph-building-llm-wiki-graphify-01b4f031471a)
- [Personal Knowledge Management (2026): The Honest Guide](https://www.atlasworkspace.ai/blog/personal-knowledge-management)
- [Mastering Personal Knowledge Management with Obsidian and AI](https://ericmjl.github.io/blog/2026/3/6/mastering-personal-knowledge-management-with-obsidian-and-ai/)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
