---
date: 2026-06-19
bot: roun
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 로운 자가학습 — 2026-06-19

---

## 오늘 배운 것

- **Prisma + PgBouncer**: 멀티프로세스 환경에서 `connection_limit = (CPU×2)+1` 공식 적용. URL에 `?pgbouncer=true` 필수. `prisma migrate`는 PgBouncer 미지원 — `directUrl`로 별도 커넥션 지정해야 함. ([출처](https://www.prisma.io/docs/orm/prisma-client/setup-and-configuration/databases-connections/pgbouncer))

- **API 멱등성(Idempotency) 키**: 클라이언트가 UUIDv4 생성 → 서버에서 `INSERT INTO idempotency_keys ... ON CONFLICT DO NOTHING` 원자적 처리 → 캐시된 응답 반환 (TTL 24h). `idempot-js` (2026-04 릴리즈)가 Fastify 미들웨어 플러그인 제공. ([출처](https://roderick.dk/posts/2026-04-06-announcing-idempot-js/))

- **Zod v4 API 변경**: `z.string().uuid()` → `z.uuid()` (RFC 9562 준수), `z.string().email()` → `z.email()`로 독립 분리. v3.24가 아직 주류(주간 4천만 다운로드)지만 v4 마이그레이션 대비 필요. ([출처](https://1xapi.com/blog/validate-api-requests-zod-nodejs-2026))

- **PostgreSQL 인덱스**: 성능 문제의 80%가 누락 인덱스에서 발생. JSONB 컬럼은 GIN 인덱스, 일반 조회/정렬은 B-tree. PostgreSQL 19에서 index pre-fetching 추가 예정. ([출처](https://zeonedge.com/blog/postgresql-performance-tuning-2026-indexes-query-optimization))

- **`@fastify/rate-limit` 분산 환경**: 기본 인메모리 스토어는 단일 인스턴스에만 유효. `store` 옵션에 Redis 커스텀 스토어 연결하면 수평 확장 시에도 글로벌 rate limit 적용 가능. ([출처](https://github.com/fastify/fastify-rate-limit))

---

## 출처

- [Configure Prisma Client with PgBouncer — Prisma Docs](https://www.prisma.io/docs/orm/prisma-client/setup-and-configuration/databases-connections/pgbouncer)
- [Announcing idempot-js (2026-04)](https://roderick.dk/posts/2026-04-06-announcing-idempot-js/)
- [How to Implement Idempotency Keys in Node.js APIs](https://oneuptime.com/blog/post/2026-01-27-nodejs-idempotency-keys/view)
- [Validate API Requests with Zod in Node.js (2026 Guide)](https://1xapi.com/blog/validate-api-requests-zod-nodejs-2026)
- [PostgreSQL Performance Tuning 2026 — ZeonEdge](https://zeonedge.com/blog/postgresql-performance-tuning-2026-indexes-query-optimization)
- [fastify/fastify-rate-limit GitHub](https://github.com/fastify/fastify-rate-limit)

---

## 위키화 후보

- **API 멱등성 키 패턴** — `idempot-js` + Postgres `ON CONFLICT` 구현 + Redis TTL 캐싱 전략 정리
- **Prisma + PgBouncer 설정 가이드** — `connection_limit` 공식, `?pgbouncer=true`, migrate용 `directUrl` 분리

---

## 프로필 반영 후보 (저위험)

- Prisma 멀티프로세스: `connection_limit=(CPU×2)+1`, PgBouncer transaction mode + `?pgbouncer=true`, migrate는 `directUrl` 별도 사용
- API 멱등성: 클라이언트 UUIDv4 → 서버 atomic `INSERT ON CONFLICT` → 24h TTL; Fastify는 `idempot-js` 플러그인 활용

---

## 승인 필요 (고위험)

_(없음)_
