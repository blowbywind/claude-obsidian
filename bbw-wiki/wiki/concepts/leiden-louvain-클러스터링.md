---
title: Leiden/Louvain 클러스터링
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-dex-learning]]
summary: "지식 그래프의 밀집 커뮤니티를 탐지하여 위키 구조를 시각화하고 고립된 페이지·단절 섹션·밀집 영역을 자동 식별하는 네트워크 군집화 알고리즘"
---

# Leiden/Louvain 클러스터링

## 핵심 정의

Leiden/Louvain 클러스터링은 지식 그래프에서 관련된 노트들을 자동으로 "이웃(neighborhood)"으로 묶는 네트워크 군집화 알고리즘이다. 그래프의 구조적 특성을 기반으로 밀집 커뮤니티를 탐지한다.

## 주요 활용

**위키 구조 시각화**: 고아 노드(orphaned node)와 밀집 허브(dense hub)를 시각적으로 즉시 파악할 수 있다. 이를 통해 위키의 연결성 불균형을 한눈에 관찰 가능하다.

**위키 건강도 점검**: 클러스터링 결과를 통해 고립된 페이지, 단절된 섹션, 과도하게 밀집된 영역을 자동으로 탐지한다. 위키 유지보수 전략 수립에 활용된다.

**지식 구조 최적화**: 관련 개념의 자동 군집화로 새로운 크로스레퍼런스 기회를 발견하거나 기존 연결 구조의 개선 영역을 식별할 수 있다.

## 출처

- [From Scattered Notes to a Living Knowledge Graph: Building LLM Wiki + Graphify](https://medium.com/@jsong_49820/from-scattered-notes-to-a-living-knowledge-graph-building-llm-wiki-graphify-01b4f031471a)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
