---
date: 2026-06-30
bot: dex
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 덱스 자가학습 — 2026-06-30

교차검증 결과:
- **CVE-2025-66478** 폐기 — 특정 CVE 번호를 훈련 지식으로 확인 불가. Next.js 실제 중요 취약점은 CVE-2025-29927(미들웨어 우회)이며 해당 번호와 불일치. 출처 URL만 실재하고 주장 검증 불가.
- **Prisma 7 WASM 엔진** 폐기 — `_review-queue/2026-06-21-roun-prisma-v7-typescript-엔진.md` 이미 존재, 중복.
- **Tailwind v4** 폐기 — `wiki/concepts/tailwind-css-v4.md`(rina 작성) 및 review-queue 노트 이미 존재, 중복.
- 나머지 5항목: Next.js 공식 문서·Prisma 공식 문서·Drizzle 공식 문서·TanStack 공식 문서로 교차검증 통과.

---

## 오늘 배운 것
- **Server Actions = 공개 HTTP POST 엔드포인트**: 글로벌 미들웨어 인증과 무관하게 외부 직접 호출 가능. 각 액션 내부에서 개별 인증·인가 + Zod 입력 검증을 독립적으로 수행해야 함 — 미들웨어 통과 ≠ 액션 보호.
- **Prisma `SELECT *` 안티패턴**: `include`나 `findMany` 기본 호출은 불필요한 대용량 TEXT/JSONB 컬럼 전체 조회. 성능 병목 방지를 위해 `select` 필드를 항상 명시.
- **Drizzle ORM 성능 최적화 두 축**: 잦은 쿼리는 Prepared Statements, 다중 쓰기는 `db.batch()` 네이티브 배치 API — 트랜잭션 오버헤드를 구조적으로 절감.
- **RSC 데이터 패칭 워터폴 방지**: 중첩 서버 컴포넌트의 독립적 `await` 직렬 호출은 응답 지연 누적. 독립 쿼리는 `Promise.all` 병렬 처리, 컴포넌트 간 공유 데이터는 React `cache()` API로 서버측 메모이제이션.
- **RSC + TanStack Query 하이브리드 아키텍처**: 초기 페이지 로딩·SEO는 RSC로 서버에서 처리, 클라이언트 상호작용·실시간 뮤테이션은 TanStack Query 조합. 2026년 기준 표준 우수 사례로 안착.

## 출처
- [Next.js — Server Actions and Mutations](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations)
- [Prisma — Select Fields](https://www.prisma.io/docs/concepts/components/prisma-client/select-fields)
- [Drizzle ORM — Performance and Edge](https://orm.drizzle.team/docs/perf-and-edge)
- [Next.js — Fetching, Caching, and Revalidating](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating)
- [TanStack Query — SSR Guide](https://tanstack.com/query/latest/docs/framework/react/guides/ssr)

## 위키화 후보
- `server-actions-security-패턴` — 공개 엔드포인트 특성·액션 내부 인증/인가/Zod 검증 패턴 (기존 `react.md` useFormStatus 노트와 연결)
- `rsc-tanstack-query-하이브리드` — RSC 초기 페칭 + TanStack Query 클라이언트 뮤테이션 조합 패턴 (깨진 `tanstack.md` 보완 또는 별도 노트)

## 프로필 반영 후보 (저위험)
- React `cache()` API — RSC 서버측 메모이제이션 도구, 워터폴 방지 패턴의 핵심 API로 지식 체계에 추가
- Drizzle `db.batch()` — 다중 쿼리 일괄 처리 네이티브 API, Drizzle 관련 노트 작성 시 항상 명시

## 승인 필요 (고위험)

## 신규 도구 후보 (에이전트/스킬)
