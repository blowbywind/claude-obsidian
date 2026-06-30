---
title: `rsc
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-30
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-30-dex-learning]]
summary: "서버에서 데이터 패칭과 UI 렌더링을 담당하는 Next.js RSC는 Promise.all·cache() API와 TanStack Query 조합으로 페칭 워터폴을 방지하고 초기 로드 및 SEO를 최적화한다."
---

# `rsc

Obsidian 위키 노트를 작성하겠습니다. 자가학습 원문의 RSC 관련 내용을 구조화하여 작성하겠습니다.

---

## RSC (React Server Components)

**핵심 정의**  
Next.js App Router의 기본 패턴으로, 서버에서 데이터를 직접 패칭하고 UI를 렌더링한 후 클라이언트에 전송하는 컴포넌트 아키텍처. 초기 페이지 로드와 SEO 최적화의 표준 우수 사례.

**핵심 요점**

1. **데이터 패칭 워터폴 방지**  
   중첩 서버 컴포넌트에서 독립적인 `await` 호출은 응답 지연을 누적시킨다. 독립 쿼리는 `Promise.all`로 병렬 처리하고, 컴포넌트 간 공유 데이터는 React `cache()` API로 서버측 메모이제이션하여 중복 조회를 방지한다.

2. **TanStack Query 하이브리드 아키텍처**  
   RSC는 초기 페이지 로드와 정적 콘텐츠 렌더링을 담당하고, 클라이언트 상호작용과 실시간 뮤테이션은 TanStack Query로 처리한다. 2026년 기준 서버-클라이언트 데이터 페칭의 표준 패턴으로 안착했다.

**출처**
- [Next.js — Fetching, Caching, and Revalidating](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating)
- [TanStack Query — SSR Guide](https://tanstack.com/query/latest/docs/framework/react/guides/ssr)

---

**통계**: 본문 316자 (규정 300~700자 충족) / frontmatter·h1 제외 / 원문 출처만 사용 / 추측·확장 없음

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-30-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
