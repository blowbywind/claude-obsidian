---
title: LLM Wiki Lint Pattern
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-dex-learning]]
summary: "위키의 고아 노트·깨진 레퍼런스·스테일 임베딩·출처 누락을 자동 검사하는 파이프라인 패턴"
---

# LLM Wiki Lint Pattern

Obsidian 위키 concept 노트 본문을 작성하겠습니다.

## 핵심 정의

**LLM Wiki Lint Pattern**은 위키 구조의 일관성과 건강도를 검사하는 자동화 파이프라인이다. 고아 노트·깨진 크로스레퍼런스·스테일 임베딩·소스 누락을 한 번에 검사하는 구조 검증 패턴으로, 2026년 표준화 추세에 해당한다.

## 주요 특징

### 자동화 범위
고아 페이지 탐지, 깨진 크로스레퍼런스 추적, 임베딩 스테일 여부 판정, 출처 누락 감지 등을 수작업이 아닌 파이프라인으로 일괄 처리한다.

### 수작업 대체
기존 별도 운영 체크를 구조 검사(lint) 자동화로 통합하여 위키 유지관리 비용을 절감한다.

### 지식 그래프 활용
Leiden/Louvain 클러스터링 등 그래프 알고리즘으로 관련 노트의 "이웃(neighborhood)"을 자동 식별하여 고아 노드와 밀집 허브를 시각적으로 파악할 수 있다.

## 출처

- [From Scattered Notes to a Living Knowledge Graph: Building LLM Wiki + Graphify](https://medium.com/@jsong_49820/from-scattered-notes-to-a-living-knowledge-graph-building-llm-wiki-graphify-01b4f031471a)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
