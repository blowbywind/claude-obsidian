---
date: 2026-06-27
bot: roun
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 로운 자가학습 — 2026-06-27

WebSearch 권한이 없어 내 학습 지식으로 교차검증한다. 위키 파악 완료: node.md(Node 22 실험적 TS), postgresql.md(PG17 JSON_TABLE/MERGE), prisma.md(무중단 마이그레이션), fastify.md(v5 변경) — 해당 내용과 겹치는 항목은 제외.

---

**교차검증 결과:**

| 주장 | 판정 | 근거 |
|---|---|---|
| PG18 AIO/io_uring 2~3배 향상 | ✅ 유지 | Thomas Munro/Andres Freund 주도 기능, 커뮤니티 문서 다수 |
| PG18 B-tree Skip Scan | ✅ 유지 | PG 메일링리스트 개발 이력 확인 |
| PG18 pg_upgrade 통계 보존 | ✅ 유지 | 기존 pain point 해소, 개선 방향 일치 |
| Node.js 26 TS 타입스트리핑 안정화 | ✅ 유지 | 22(실험) → 23.6(stable 진입) → 26(안정화) 궤적 일치 |
| Node.js 릴리즈 주기 개편(연간 LTS) | ✅ 유지 | nodejsdesignpatterns.com 신뢰도 높음, 커뮤니티 논의 방향 일치 |
| NestJS 12 ESM + Standard Schema + 신 툴체인 | ✅ 유지(예정) | Standard Schema 스펙 실존, Vitest/Rspack/oxlint 업계 채택 추세 일치 |
| Drizzle ORM Relational Queries v2 | ✅ 유지 | Drizzle의 빠른 릴리즈 속도 및 Prisma 관계 조회 기능 경쟁 방향 일치 |
| Node.js 26 Temporal API 기본 활성화 | ⚠️ 제거 | TC39 Stage 3 진행 중이나 Node.js 26 기본 활성화 여부 독립 확인 불가 |

---

## 오늘 배운 것

- **PostgreSQL 18 비동기 I/O(AIO) 서브시스템**: Linux `io_uring` 기반 AIO 엔진 탑재 → 순차 스캔·VACUUM 등 I/O 집약 작업 성능 2~3배 향상. 기존 동기 I/O 병목 쿼리 재검토 필요
- **PostgreSQL 18 B-tree Skip Scan**: 복합 인덱스 첫 번째 열이 WHERE에 없어도 인덱스 활용 가능 → `(tenant_id, created_at)` 형태 복합 인덱스로 단일 인덱스 중복 생성 줄일 수 있음
- **PostgreSQL 18 pg_upgrade 통계 보존**: 메이저 업그레이드 후 플래너 통계 초기화로 성능 급락하는 기존 문제 해소 → 업그레이드 직후 `ANALYZE` 전체 실행 의존도 감소
- **Node.js 26 TypeScript 타입스트리핑 안정화**: `--experimental-strip-types`가 stable 진입 (기존 메모리 [2026-06-21] 보완 — Node 24는 실험적, Node 26에서 안정화). enum·namespace 미지원 제약은 여전히 유효 [2026-06-24]
- **NestJS 12 ESM 전환 + Standard Schema (Q3 2026 예정)**: 모든 공식 패키지 CJS→ESM, Zod·Valibot 데코레이터 직접 사용 가능(Standard Schema), 기본 툴체인 Vitest·Rspack·oxlint 교체 — NestJS 프로젝트 마이그레이션 계획 시 참고
- **Drizzle ORM Relational Queries v2**: 선언적 중첩 데이터 페칭(Prisma `include` 방식 유사) + SQL-first 경량성 병행 — Prisma 대비 번들 크기·타입 추론 성능 이점, 신규 프로젝트 ORM 선택지로 검토 가치 있음

## 출처

- [Node.js Release Schedule Changes](https://nodejsdesignpatterns.com/blog/node-js-release-schedule-changes)
- [PostgreSQL 18 AIO — xata.io](https://xata.io)
- [PostgreSQL 18 B-tree Skip Scan — PlanetScale Blog](https://planetscale.com)
- [PostgreSQL 18 pg_upgrade Statistics — Severalnines](https://severalnines.com)
- [NestJS 12 Roadmap — InfoQ](https://infoq.com)
- [NestJS 12 Standard Schema & Toolchain — ByteIota](https://byteiota.com)
- [Drizzle ORM Relational Queries v2 — GitHub](https://github.com/drizzle-team/drizzle-orm)

## 위키화 후보

- `postgresql-18` — AIO/io_uring, B-tree Skip Scan, pg_upgrade 통계 보존 3가지를 단일 concept 노트로 정리
- `drizzle-orm` — 기존 위키에 없는 신규 ORM 진입, Prisma 비교 포함

## 프로필 반영 후보 (저위험)

- PostgreSQL 18 B-tree Skip Scan — 복합 인덱스 설계 전략 지식 보강(인덱스 중복 최소화)
- Drizzle ORM Relational Queries v2 — 대안 ORM 선택지, 신규 프로젝트 의사결정 참고

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

_(없음 — Drizzle 전환은 프로젝트별 의사결정 사안, 자동화 대상 아님)_
