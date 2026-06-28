---
date: 2026-06-19
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-19

---

## 오늘 배운 것

- **WCAG 3.0은 여전히 Draft** — APCA 알고리즘은 2023년 7월 W3C 워킹그룹에서 명세 제거됨. 현행 법적 기준은 WCAG 2.2 Level AA. 프로덕션에서 APCA 기반 명암비 적용은 법적 리스크 (출처: [adrianroselli.com](https://adrianroselli.com/2026/04/wcag3-contrast-as-of-april-2026.html), [accessibility.chat](https://www.accessibility.chat/articles/the-apca-mirage-why-premature-wcag-3-adoption-creates-legal-risk))

- **Tailwind `motion-safe:` / `motion-reduce:` 변형** — 비필수 애니메이션은 반드시 `motion-safe:animate-*`로 감싸야 함. `motion-reduce:delay-0`으로 delay도 제거 가능. Tailwind v4에서는 `@theme` 내 커스텀 keyframe 정의 가능 (출처: [tailwindcss.com](https://tailwindcss.com/docs/animation))

- **W3C DTCG 토큰 포맷 첫 안정 버전 도달 (2025.10)** — Oklch·Display P3·CSS Color Module 4 지원. 멀티플랫폼 토큰 교환 표준. 웹 런타임 구현은 CSS 변수, 추상 정의는 DTCG 포맷으로 역할 분리 (출처: [w3.org](https://www.w3.org/community/design-tokens/2025/10/28/design-tokens-specification-reaches-first-stable-version/))

- **shadcn/ui v4 CLI `--preset` + `shadcn/skills`** — `init --preset`으로 전체 재구성 자동화. `shadcn/skills`는 AI 코딩 에이전트가 컴포넌트·레지스트리 컨텍스트를 올바르게 참조하도록 지원 (출처: [ui.shadcn.com changelog](https://ui.shadcn.com/docs/changelog/2026-03-cli-v4))

- **2026 접근성은 "인프라"로 정의** — 고대비 모드·키보드 내비게이션·reduced-motion을 시스템 초기부터 내장. 보정 리워크 비용 감소 및 조달 기준 영향 (출처: [uxpin.com](https://www.uxpin.com/studio/blog/ui-ux-design-trends/))

- **디자인 시스템의 AI 싱글 소스화** — AI 어시스턴트가 디자인 시스템을 유일한 참조 소스로 삼는 패턴 확산. 자동 유효성 검사(접근성·간격·컴포넌트 사용 규칙) 내장 (출처: [envato.com](https://elements.envato.com/learn/ux-ui-design-trends))

---

## 출처

- [WCAG3 Contrast as of April 2026 — Adrian Roselli](https://adrianroselli.com/2026/04/wcag3-contrast-as-of-april-2026.html)
- [APCA Legal Risk — accessibility.chat](https://www.accessibility.chat/articles/the-apca-mirage-why-premature-wcag-3-adoption-creates-legal-risk)
- [Tailwind CSS animation docs](https://tailwindcss.com/docs/animation)
- [Design Tokens specification reaches first stable version — W3C](https://www.w3.org/community/design-tokens/2025/10/28/design-tokens-specification-reaches-first-stable-version/)
- [shadcn/ui March 2026 Changelog — CLI v4](https://ui.shadcn.com/docs/changelog/2026-03-cli-v4)
- [12 UX/UI Design Trends 2026 — UXPin](https://www.uxpin.com/studio/blog/ui-ux-design-trends/)
- [UX/UI design trends 2026 — Envato Elements](https://elements.envato.com/learn/ux-ui-design-trends)

---

## 위키화 후보

- **W3C DTCG 토큰 포맷** — 2025.10 stable, Style Dictionary 변환 도구, "DTCG = 추상 정의 / CSS 변수 = 런타임 구현" 역할 분리 개념
- **Tailwind motion-safe/motion-reduce 패턴** — `prefers-reduced-motion` 대응 구현 패턴, `@theme` keyframe 정의 방법

---

## 프로필 반영 후보 (저위험)

- 비필수 애니메이션은 항상 `motion-safe:` 변형으로 감쌀 것 (WCAG 2.1 SC 2.3.3 준수)
- WCAG 2.2 Level AA가 현행 법적 기준 — APCA는 W3C 명세에서 제거됐으므로 명암비 판단 기준으로 사용 금지

---

## 승인 필요 (고위험)

_(없음)_
