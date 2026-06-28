---
date: 2026-06-24
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-24

I will start by checking the existing wiki documents to understand what is already recorded and avoid duplicates. I'll search `/home/bbw/obsidian-vault/bbw-wiki`.
I will now check the contents of `/home/bbw/obsidian-vault/bbw-wiki/wiki` to find existing files and categories.
I will search the wiki files to check if there are any existing documents related to the topics under review: DTCG, Liquid Glass, Generative UI, shadcn v4, CSS Anchor positioning, Popover API, light-dark(), or WCAG 2.2.
I will perform a broader search in the workspace to see if terms like "Tailwind", "shadcn", or "WCAG" are mentioned anywhere.
I will run a web search to check browser support for CSS Anchor Positioning, specifically whether Safari 18.2 or other WebKit engines support it, and if a JS positioning fallback is required.
I will search for the status of Tailwind CSS v4 support in shadcn/ui and how the data-slot system works.
I will run a web search on browser support and usage guidelines for the CSS `light-dark()` function.
I will run a web search to verify the details about WCAG 2.2 Success Criteria 2.5.8 (Target Size (Minimum)) and 2.5.7 (Dragging Movements).
I will run a web search to check for any reported issues with the Popover API on iOS where focusing an input field inside a popover causes it to close.
## 오늘 배운 것
- **Tailwind v4 & shadcn/ui의 CSS-first 및 `data-slot` 스타일 구성**: `tailwind.config.js` 없이 CSS `@theme` 구조를 사용하며, 컴포넌트 스타일 확장 시 `data-slot` 특성 선택자를 사용해 스타일을 깔끔하게 유지합니다.
- **CSS Anchor Positioning의 브라우저 지원 제약**: Safari 및 iOS WebKit 환경에서의 미지원으로 인해, 상용 서비스 배포 시 Floating UI 등 JavaScript 포지셔닝 폴백을 적용해야 합니다.
- **iOS Safari 환경 Popover API 입력 폼 오류**: iOS에서 Popover 내부 입력 폼에 포커스할 때 팝오버가 꺼지는 버그(WebKit Bug 267688)가 있어 모바일 대응 시 라이브러리 대체 등 예외 처리가 필요합니다.
- **CSS `light-dark()` 함수 활용 다크모드 경량화**: 미디어쿼리 중복을 피하고 `:root` 등에 `color-scheme: light dark`를 지정하여 직관적으로 다크모드 디자인 토큰 값을 일괄 적용합니다.
- **WCAG 2.2 모바일 접근성 설계 준수**: 기획/디자인 시스템 설계 단계부터 최소 터치 영역 24x24 CSS px 확보(SC 2.5.8) 및 드래그 동작에 대한 탭/클릭 대체 수단(SC 2.5.7) 구현 가이드를 적용합니다.

## 출처
- [W3C WCAG 2.2 Quick Reference](https://www.w3.org/WAI/WCAG22/quickref/)
- [MDN Web Docs - light-dark()](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/light-dark)
- [WebKit Bugzilla - Popover light dismiss on input focus](https://bugs.webkit.org/show_bug.cgi?id=267688)
- [Can I Use - CSS Anchor Positioning](https://caniuse.com/css-anchor-positioning)

## 위키화 후보
- CSS `light-dark()` 함수와 `color-scheme`을 연계한 멀티 테마 디자인 토큰 표준 가이드라인
- 모바일 iOS Safari 환경 Popover API 오동작 대응을 위한 대체 UI 구현 패턴

## 프로필 반영 후보 (저위험)
- Tailwind CSS v4 CSS-first 테마 및 `data-slot` 스타일링 패턴 활용 능력
- WCAG 2.2 기준에 맞춘 터치 타깃 및 드래그 인터랙션 설계 능력

## 승인 필요 (고위험)

## 신규 도구 후보 (에이전트/스킬)
- [skill] tailwind-v4-migrator — 기존 Tailwind v3 디자인 시스템 프로젝트를 v4 CSS-first 및 data-slot 구조로 자동 변환하고 유효성을 검증하는 스킬
