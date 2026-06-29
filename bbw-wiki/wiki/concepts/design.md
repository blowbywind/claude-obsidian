---
title: design
type: concept
status: ai-curated
learned_by: rina
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-18-rina-learning]]
summary: "Design Token은 색상·간격·폰트를 변수화한 체계이고, Tailwind v4 CSS-First와 Calm UI 철학으로 2026 디자인 방향을 제시한다."
---

# design

마크다운 본문입니다:

---

**Design Token**은 색상, 간격, 폰트 등 디자인 시스템의 기본 단위를 변수화한 자산이다. 현대 디자인 시스템은 3계층으로 구조화된다: **Primitive**(원시값, 예: `#0EA5E9`) → **Semantic**(의도 기반 이름, 예: `--color-primary`) → **Component**(요소별 특정, 예: `--button-bg`). 이 위계는 W3C Design Tokens Format Module에서 표준화되었으며, 컴포넌트 토큰은 반드시 Semantic을 참조해야 한다.

**Tailwind v4 CSS-First 설계**는 `tailwind.config.js` 제거 후 `@theme {}` 블록으로 CSS 파일 내 토큰을 직접 선언한다. 색상은 OKLCH 색공간으로 정의하여 지각 균등성을 보장한다. 컴포넌트 재사용 클래스는 `@layer components`에 정의하되, 동일 패턴이 5회 이상 반복될 때만 생성 권장한다.

**Calm UI** 철학은 2026 핵심 UX 방향으로, 시각적 화려함보다 인지 부하 감소를 우선한다. 애니메이션은 엔터테인먼트 목적이 아닌 **명확성(clarity)** 목적으로만 사용한다.

## 출처
- https://www.maviklabs.com/blog/design-tokens-tailwind-v4-2026/
- https://tailwindcss.com/blog/tailwindcss-v4
- https://tailwindcss.com/docs/adding-custom-styles

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-18-rina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
