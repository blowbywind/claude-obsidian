---
title: PostgreSQL Partial & Composite Index 패턴
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-roun-learning]]
---

# PostgreSQL Partial & Composite Index 패턴

## 요청 확인

Obsidian 위키 concept 노트 본문을 작성하겠습니다. 자가학습 원문의 "PostgreSQL Partial Index"와 "복합 인덱스 컬럼 순서" 섹션을 기반으로, 원문에 없는 내용은 추가하지 않고 제약사항을 준수합니다.

---

## 본문

**Partial Index**는 `WHERE is_active = true` 같은 조건절이 붙은 선택적 인덱스로, 전체 테이블이 아닌 조건을 만족하는 행만 인덱싱한다. 1026 MB 인덱스를 96 KB로 축소한 실사례처럼 인덱스 크기를 극적으로 줄이면서도 삽입/수정/삭제 비용은 전체 인덱스 대비 낮게 유지된다. **Composite Index**는 여러 컬럼을 함께 인덱싱하되, 첫 번째 컬럼으로 쿼리가 시작되지 않으면 인덱스를 활용할 수 없다. 고쓰기 테이블에서 인덱스 5개를 무분별하게 추가하면 INSERT가 2~3배 저하되므로 필요한 것만 선별해야 한다.

**설계 기준**: 인덱스를 추가하기 전에 쿼리 패턴을 분석해 첫 번째 검색 컬럼을 파악하고, 활성 데이터만 자주 조회하면 Partial Index로 크기를 절감하며, 쓰기 성능 트레이드오프를 검증한 후 적용한다. 프로덕션 배포 시에는 `CREATE INDEX CONCURRENTLY`로 테이블 잠금을 방지한다.

## 출처

- https://stormatics.tech/blogs/optimizing-postgresql-with-composite-and-partial-indexes
- https://zeonedge.com/blog/postgresql-performance-tuning-2026-indexes-query-optimization
- https://www.sachith.co.uk/postgresql-indexing-playbook-practical-guide-feb-12-2026/

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
