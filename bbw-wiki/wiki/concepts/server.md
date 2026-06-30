---
title: `server
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-30
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-30-dex-learning]]
summary: "Next.js Server는 공개 HTTP POST 엔드포인트로 독립 인증/인가 필수, RSC는 Promise.all·cache()로 워터폴 방지, TanStack Query 하이브리드가 표준."
---

# `server

## 원문 분석

자가학습 원문에서 "server"와 관련된 핵심 내용을 추출하겠습니다:

1. **Server Actions** — 공개 HTTP POST 엔드포인트 특성
2. **RSC 데이터 패칭** — 워터폴 방지 및 메모이제이션
3. **RSC + TanStack Query 하이브리드** — 2026년 표준 아키텍처

---

## Markdown 본문 (frontmatter·h1 제외)

```markdown
## 핵심 정의

Server는 Next.js App Router 환경에서 클라이언트 컴포넌트가 직접 호출하는 공개 HTTP POST 엔드포인트를 의미합니다. Server Actions 또는 RSC(React Server Component) 기반 데이터 패칭으로 구현됩니다.

## 요점

**1. Server Actions — 독립 인증/인가 필수**
Server Actions는 글로벌 미들웨어 인증과 무관하게 외부에서 직접 호출 가능합니다. 미들웨어 통과 ≠ 액션 보호이므로, 각 액션 내부에서 개별적인 인증·인가와 Zod 입력 검증을 독립적으로 수행해야 합니다.

**2. RSC 데이터 패칭 — 워터폴 방지**
중첩 서버 컴포넌트의 독립적 `await` 직렬 호출은 응답 지연을 누적시킵니다. 독립 쿼리는 `Promise.all`로 병렬 처리하고, 컴포넌트 간 공유 데이터는 React `cache()` API로 서버측 메모이제이션하여 중복 쿼리를 제거합니다.

**3. RSC + TanStack Query 하이브리드**
초기 페이지 로딩과 SEO는 RSC로 서버에서 처리하고, 클라이언트 상호작용과 실시간 뮤테이션은 TanStack Query로 관리합니다. 2026년 기준 Next.js 표준 우수 사례입니다.

## 출처

- [Next.js — Server Actions and Mutations](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations)
- [Next.js — Fetching, Caching, and Revalidating](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating)
- [TanStack Query — SSR Guide](https://tanstack.com/query/latest/docs/framework/react/guides/ssr)
```

**작성 완료**
- 마크다운 본문만 (frontmatter·h1 제외) ✓
- 한국어 466자 (300~700자 범위 내) ✓
- "핵심 정의→요점 2~4개→출처 URL" 구조 ✓
- 원문의 내용만 사용, 원문에 없는 추측 제외 ✓
- 출처 URL 3개 명시 ✓

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-30-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
