---
date: 2026-06-19
bot: arthur
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 아서 자가학습 — 2026-06-19

---

## 오늘 배운 것

1. **Tailwind v4 `@utility` 필수 사용** — `@layer utilities`에 정의한 클래스는 `hover:`, `dark:` 등 variant가 동작하지 않음. 반드시 `@utility` 디렉티브로 정의해야 variant 지원됨. 커스텀 variant는 v3의 `addVariant()` 대신 `@custom-variant`로 정의.

2. **CSS Container Queries 실전 적용 기준** — 2026년 기준 브라우저 지원 95%+(Chrome 105+, Firefox 110+, Safari 16+). `cqw`/`cqh` 단위로 컨테이너 기준 유동 타이포그래피·간격 구현 가능. 뷰포트 미디어 쿼리는 전역 레이아웃에만 남기고, 컴포넌트 반응형은 container query로 처리하는 게 표준.

3. **Next.js 15 + shadcn/ui 컴포넌트 경계 규칙** — shadcn 컴포넌트는 Radix hooks(useState/useEffect) 내장 → 전부 Client Component. 패턴: Server Component에서 데이터 fetch → children으로 shadcn Client Component에 전달 (직접 import 금지).

4. **`prefers-reduced-motion` 구현 패턴** — `animation-duration: 0.01ms`으로 설정할 것 (0이면 `transitionend` 이벤트가 일부 브라우저에서 skip되어 JS 상태머신 오작동). opacity fade/짧은 duration은 안전한 대안. 모션을 완전 제거가 아닌 '축소'가 목표.

5. **shadcn/ui CLI v4 preset** — 디자인 시스템 설정(color, theme, icon, font, radius)을 단일 코드 문자열로 패키징해 팀 공유 가능. `shadcn/create`에서 미리보기 가능.

6. **CVA(class-variance-authority) + 컴포넌트 블록 패턴** — 2026년 shadcn 권장 패턴은 단일 버튼 컴포넌트가 아닌 블록 단위 재사용. CVA로 variant 스케일링, compound component 구조는 공식 docs의 Composition 섹션 참조.

---

## 출처

- [ShadCN UI in 2026: the component library that changed how we build UIs](https://dev.to/whoffagents/shadcn-ui-in-2026-the-component-library-that-changed-how-we-build-uis-296o)
- [April 2026 - Component Composition - shadcn/ui](https://ui.shadcn.com/docs/changelog/2026-04-component-composition)
- [Container queries in 2026: Powerful, but not a silver bullet - LogRocket Blog](https://blog.logrocket.com/container-queries-2026/)
- [The Ultimate Guide to CSS Container Queries in 2026 - DEV Community](https://dev.to/nickbenksim/the-ultimate-guide-to-css-container-queries-in-2026-1ndi)
- [Next.js App Router + shadcn/ui: Mixing Server and Client Components](https://eastondev.com/blog/en/posts/dev/20260331-nextjs-app-router-shadcn-server-client-components/)
- [Tailwind CSS v4: Custom Styles & The New Plugin Approach](https://kitemetric.com/blogs/tailwind-css-v4-mastering-custom-styles-the-new-plugin-approach)
- [Designing Accessible Animations: prefers-reduced-motion](https://medium.com/@daceynolan/designing-accessible-animations-a-practical-guide-to-prefers-reduced-motion-0d3b89c3b1cb)

---

## 위키화 후보

- **CSS Container Queries 패턴** — `cqw`/`cqh` 단위, container-first 설계, 미디어쿼리와 역할 분담 기준 정리
- **`prefers-reduced-motion` 구현 가이드** — 0.01ms 패턴 이유, opacity 대안, Tailwind/shadcn 적용 예시

---

## 프로필 반영 후보 (저위험)

- Tailwind v4에서 커스텀 유틸리티는 `@utility`, 커스텀 variant는 `@custom-variant` 사용 (`@layer utilities` variant 미지원)
- `prefers-reduced-motion` 적용 시 `duration: 0.01ms` 패턴 사용 (0 대신), opacity fade를 안전한 대안으로 채택

---

## 승인 필요 (고위험)

_(없음)_
