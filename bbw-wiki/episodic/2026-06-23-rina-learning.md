---
date: 2026-06-23
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-23

You've hit your Sonnet limit · resets Jun 27, 3am (UTC)


## 추가 학습 (12:17 UTC)
You've hit your Sonnet limit · resets Jun 27, 3am (UTC)


## 추가 학습 (12:18 UTC)
## 오늘 배운 것
- **EAA 법적 기준은 아직 WCAG 2.1 AA**: 유럽 접근성법(2025-06-28 시행)의 조화 표준(EN 301 549)에 WCAG 2.2가 아직 통합되지 않아, 법적 컴플라이언스 벤치마크는 **WCAG 2.1 AA**가 현행. (내 프로필 인사이트 "WCAG 2.2 AA가 현행 법적 기준"은 권장 목표로는 맞으나 *법적* 기준 표현은 부정확 → 수정 필요)
- **WCAG 2.2 신규 AA 포커스 기준 2종 — 컴포넌트 작업 시 적용**: `2.4.11 Focus Not Obscured(Minimum)` 포커스 요소가 sticky 헤더/푸터에 *완전히* 가려지면 안 됨, `2.4.13 Focus Appearance`는 AAA(혼동 주의). 다이얼로그는 열릴 때 포커스 내부 이동 + Esc 닫기 + 포커스 요소 부분가시성 필수.
- **CSS `interpolate-size: allow-keywords` + `calc-size()`** 로 `height: 0→auto` 트랜지션이 JS 측정 없이 가능(아코디언·드로어). 단 `interpolate-size`/`calc-size()`는 Chrome 선행, 타 엔진 추격 중 → fallback 필요. `@starting-style`·`transition-behavior: allow-discrete`는 2026년 전 엔진 안정.
- **스크롤 기반 애니메이션 2026 전 브라우저 지원**: `animation-timeline: scroll()`/`view()` 로 메인스레드 JS 없이 스크롤 연동 애니메이션. 단 비필수 애니는 기존 규칙대로 `motion-safe:` 래핑.
- **shadcn CLI v4(2026-03)**: `registry:base`로 디자인 시스템 전체(컴포넌트+CSS변수+폰트+config)를 단일 페이로드 배포, 폰트가 1급 registry 타입, `--diff`로 로컬 변경 병합형 업데이트 확인. MCP/skills로 에이전트가 Radix·Base UI 패턴 모두 인지.
- Tailwind v4 커스텀 클래스는 `@apply` 대신 `@utility`로 선언해야 `hover:`/`dark:`/반응형 변형 지원(내 기존 `@layer components` 규칙 보완).

## 출처
- [Tailwind CSS v4 Complete Guide 2026](https://devtoolbox.dedyn.io/blog/tailwind-css-v4-complete-guide)
- [shadcn/cli v4 Changelog (March 2026)](https://ui.shadcn.com/docs/changelog/2026-03-cli-v4)
- [2026 CSS Features You Must Know](https://blog.riadkilani.com/2026-css-features-you-must-know/) · [interpolate-size — MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/interpolate-size)
- [Understanding the EAA and WCAG 2.2 — OneTrust](https://www.onetrust.com/blog/understanding-the-european-accessibility-act-and-wcag-22/)
- [WCAG 2.4.11 Focus Not Obscured — W3C](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum)

## 위키화 후보
- `scroll-driven-animations-패턴` — `animation-timeline: scroll()/view()` 사용법 + motion-safe·브라우저 지원 fallback (기존 view-transitions 노트와 연결)
- `interpolate-size-calc-size-패턴` — height auto 트랜지션, Chrome 선행 지원 + fallback 전략

## 프로필 반영 후보 (저위험)
- `interpolate-size`/`calc-size()` 용어 + "아코디언·드로어 높이 트랜지션은 JS 측정 대신 interpolate-size 우선 검토(Chrome 선행, fallback 필수)"
- "다이얼로그/팝오버 구현 시 WCAG 2.2 SC 2.4.11(Focus Not Obscured) 체크 — sticky 요소에 포커스 요소 가려짐 금지" 추가

## 승인 필요 (고위험)
- 프로필 인사이트 [2026-06-19] "WCAG 2.2 Level AA가 현행 법적 기준" 문구를 **"권장 목표는 WCAG 2.2 AA, 단 EAA 법적 조화표준(EN 301 549)은 아직 WCAG 2.1 AA"** 로 정정 제안.

## 신규 도구 후보 (에이전트/스킬)
- (없음)


## 추가 학습 (18:31 UTC)
You've hit your Sonnet limit · resets Jun 27, 12pm (Asia/Seoul)


## 추가 학습 (18:31 UTC)
You've hit your Sonnet limit · resets Jun 27, 12pm (Asia/Seoul)
