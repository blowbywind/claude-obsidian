---
title: Next.js 16.x 변경 요약
type: concept
status: ai-curated
learned_by: lian
curated_at: 2026-06-24
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-24-lian-learning]]
---

# Next.js 16.x 변경 요약

Next.js 16.x 변경 요약 concept 노트를 작성하겠습니다.

---

**핵심 정의**

Next.js 16.x는 Turbopack을 기본 번들러로 안정화하고, 서버 캐싱을 명시적으로 제어하는 Cache Components(`use cache` 지시어)를 도입하며, AI 에이전트용 DevTools MCP를 통합한 메이저 릴리스입니다.

**주요 변경사항**

1. **Turbopack 기본 번들러**  
   Webpack 대신 Turbopack이 기본 번들러로 설정되어 빌드 성능 대폭 개선.

2. **Cache Components & `use cache` 지시어**  
   서버 컴포넌트에서 `use cache` 지시어로 캐싱을 명시적으로 제어. 암묵적 캐싱 모델에서 명시적 옵트인으로 전환.

3. **DevTools MCP (AI 디버깅)**  
   AI 에이전트용 통합 디버깅 인터페이스: 브라우저 + 서버 로그 한 곳에서 조회.

4. **`middleware.ts` → `proxy.ts` 리네임 & AGENTS.md 기본 포함**  
   Next.js 16.2부터 프로젝트 템플릿에 AGENTS.md(AI 에이전트 명세)가 자동 생성.

**출처**
- https://nextjs.org/blog/next-16
- https://nextjs.org/blog/next-16-2
- https://nextjs.org/blog/next-16-2-ai

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-24-lian-learning]]. 사람 검증 후 status를 verified로 변경하세요.
