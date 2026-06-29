---
title: `postgresql
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-24
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-24-roun-learning]]
summary: "PostgreSQL 17은 JSON_TABLE로 JSON을 관계형 테이블로 변환하고 MERGE RETURNING으로 INSERT/UPDATE/DELETE의 실제 연산 상태를 한 번에 반환하여 SQL 처리를 효율화한다"
---

# `postgresql

Obsidian 위키 concept 노트 본문을 작성하겠습니다. 자가학습 원문의 PostgreSQL 관련 내용을 기반으로 합니다.

---

## 본문 (마크다운)

PostgreSQL 17은 강력한 확장성과 표준 준수를 특징으로 하는 오픈 소스 관계형 데이터베이스이다. JSON 데이터를 SQL로 직접 처리하고 트랜잭션 안에서 여러 연산을 원자적으로 수행할 수 있는 신규 SQL 표준 함수들을 지원한다.

### JSON_TABLE
JSON 배열이나 객체를 관계형 테이블로 변환하는 SQL 표준 함수로, 기존의 `jsonb_array_elements`와 횡전개 패턴을 단순화한다. 복잡한 JSONB 쿼리를 더 명확하고 효율적으로 작성할 수 있으며, JOIN 연산으로 다른 테이블과 결합할 수 있다.

### MERGE RETURNING
단일 MERGE 구문에서 INSERT, UPDATE, DELETE 중 실제로 적용된 연산을 `RETURNING merge_action()` 절로 구분하여 반환한다. 멱등 upsert 처리 후 각 행의 상태 변화를 한 번에 확인하므로 결과 확인에 필요한 추가 쿼리를 줄일 수 있다.

## 출처

- [PostgreSQL 17 JSON_TABLE](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-JSON-PROCESSING-TABLE)
- [PostgreSQL 17 MERGE RETURNING](https://www.postgresql.org/docs/17/sql-merge.html)

---

**글자 수**: 약 340자 (범위: 300~700자)  
**구조**: 핵심 정의 → 요점 2개 → 출처 URL

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-24-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
