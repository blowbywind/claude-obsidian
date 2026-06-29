---
title: Expand
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-roun-learning]]
summary: "Expand-Contract 패턴은 프로덕션 무중단으로 스키마 마이그레이션을 진행하는 기법으로, 신규 컬럼 추가→앱 동시 처리→기존 컬럼 제거의 3단계를 거친다."
---

# Expand

## 개념 노트 작성

마크다운 본문 (frontmatter/h1 제목 제외):

---

**Expand-Contract** 패턴은 프로덕션 환경에서 스키마 마이그레이션 중 서비스 중단 없이 데이터 구조를 변경하는 기법이다. 테이블 전체를 잠금하는 `ALTER COLUMN TYPE`의 한계를 우회한다.

**패턴의 단계:**
1. **Expand 단계** — 새로운 컬럼을 추가한다. 테이블 잠금이 짧으므로 프로덕션 배포 가능.
2. **전환 단계** — 애플리케이션이 기존 컬럼과 신규 컬럼을 동시에 처리한다. 쓰기는 둘 다, 읽기는 신규 컬럼 우선.
3. **Contract 단계** — 기존 컬럼을 제거한다. 모든 데이터 마이그레이션 완료 후 진행.

**사용 시점:**
- 컬럼 타입 변경이 필요한 경우 (예: `VARCHAR` → `UUID`)
- 컬럼 추가/제거 시 다운타임을 허용할 수 없는 프로덕션 배포
- Prisma 마이그레이션 시 `CREATE INDEX CONCURRENTLY` 등 트랜잭션 제약을 우회할 때

이 패턴을 통해 데이터 일관성을 유지하면서도 무중단 스키마 진화를 달성한다.

**참고:**
- [Zero-Downtime Schema Migrations in Production PostgreSQL](https://dev.to/software_mvp-factory/zero-downtime-schema-migrations-in-production-postgresql-b29)
- [Prisma Migrations: Zero-Downtime Expand-Contract](https://dev.to/whoffagents/prisma-migrations-in-production-zero-downtime-deployments-with-expand-contract-2l1p)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
