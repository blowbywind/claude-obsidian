---
title: `pgvector`
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-28
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-28-dex-learning]]
---

# `pgvector`

제공하신 자가학습 원문을 바탕으로 마크다운 본문을 작성하겠습니다.

---

## 핵심 정의

PostgreSQL의 벡터 검색 확장으로, 데이터베이스 내에서 ACID 트랜잭션을 보장하면서 벡터 유사도 검색을 지원합니다.

## 요점

- **단일 DB 통합**: Pinecone, Weaviate 등 독립 벡터 데이터베이스를 도입하지 않고도 PostgreSQL만으로 벡터 저장·검색 수행 가능
- **ACID 보장**: 트랜잭션 일관성과 데이터 무결성을 유지하며 RAG(Retrieval-Augmented Generation) 시스템 구축 가능
- **실용적 기본값**: 2026년 AI 기능 도입 시 별도 벡터 DB를 우선 검토하기 전에 pgvector를 먼저 검토하는 것이 정착된 실무 기준

## 출처

- [dev.to — pgvector 기본 채택 패턴](https://dev.to)

---

**작성 완료**: 본문 450자 | 원문 범위 내 구성 | 출처 URL 1개 보존

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-28-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
