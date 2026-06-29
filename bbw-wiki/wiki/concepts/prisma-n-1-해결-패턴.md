---
title: Prisma N+1 해결 패턴
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-18-roun-learning]]
summary: "Prisma의 N+1 쿼리 문제 원인, include/select/배칭 해결 전략, 30k건 이상 대규모 데이터 메모리 스파이크 주의사항."
---

# Prisma N+1 해결 패턴

Obsidian 위키 Concept 노트 본문입니다:

## 개념

**N+1 쿼리 문제**: 루프 안에서 개별 항목마다 데이터베이스 쿼리를 실행할 때 초기 쿼리 1회 + 각 항목당 쿼리 N회가 발생하여 성능이 급격히 저하되는 ORM 안티패턴. Prisma에서 흔히 발생한다.

## 핵심 요점

### 1. 성능 차이
100건 기준으로 개별 쿼리 방식은 약 2초, 관계 데이터를 한 번에 조회(JOIN)하면 약 50ms. 40배 이상 성능 격차가 발생한다.

### 2. Prisma 해결 전략
- `include()`: 관계 데이터를 한 번에 로드
- `select()`: 필요한 필드만 지정하여 `include()`보다 메모리 효율적
- `findUnique()`: 같은 이벤트 루프(tick) 내에서 자동으로 쿼리를 배칭(dataloader 처리)하므로 N+1 회피 가능

### 3. 대규모 데이터 함정
중첩된 관계를 가진 30k~40k건 이상의 데이터를 조회할 때 메모리가 4.2GB까지 스파이크하는 사례 발생. 깊은 관계 조회는 raw query나 페이지네이션을 병행해야 한다.

## 참고 자료

- [Prisma Query Optimization](https://www.prisma.io/docs/orm/prisma-client/queries/query-optimization-performance)
- [N+1 Query Problem with Prisma | Furkan Baytekin](https://furkanbaytekin.dev/blogs/n1-query-problem-fixing-it-with-sql-and-prisma-orm)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-18-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
