---
title: `prisma
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-roun-learning]]
summary: "Prisma 마이그레이션은 트랜잭션 제약으로 CREATE INDEX CONCURRENTLY와 무중단 스키마 변경을 못하므로 Expand-Contract 패턴으로 우회한다."
---

# `prisma

## prisma concept 노트 본문

**Prisma ORM의 마이그레이션 시스템은 기본적으로 모든 작업을 트랜잭션으로 감싸서 실행되므로, 프로덕션 환경에서 대용량 테이블에 무중단 스키마 변경 시 제약이 있다.**

### 요점

1. **CREATE INDEX CONCURRENTLY 차단**: Prisma는 마이그레이션을 트랜잭션 내에서 수행하는데, PostgreSQL의 `CREATE INDEX CONCURRENTLY`는 트랜잭션 외부에서만 실행 가능하다. 따라서 프로덕션 배포 전 `prisma migrate diff`로 생성된 SQL을 미리 검토하고 필요 시 수동으로 실행해야 한다.

2. **Expand-Contract 패턴 적용**: 무중단 스키마 마이그레이션은 3단계로 진행한다 — ① 새 컬럼 추가(Expand) → ② 애플리케이션이 구·신 컬럼을 병행 처리 → ③ 구 컬럼 제거(Contract). `ALTER COLUMN TYPE` 같은 테이블 전체 잠금 작업도 이 패턴으로 우회 가능하다.

### 출처

- [Prisma Migrations Zero-Downtime — DEV](https://dev.to/whoffagents/prisma-migrations-in-production-zero-downtime-strategies-and-rollback-patterns-3nf1)
- [Zero-Downtime Schema Migrations in Production PostgreSQL — DEV](https://dev.to/software_mvp-factory/zero-downtime-schema-migrations-in-production-postgresql-b29)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
