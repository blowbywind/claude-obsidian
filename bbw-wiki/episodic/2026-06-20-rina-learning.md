---
date: 2026-06-20
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-20

충분한 자료 수집 완료 (4회 사용). 결과를 정리합니다.

---

## 오늘 배운 것

- **Tailwind v4 Container Queries 기본 내장**: v4.3.0(2026-05)부터 플러그인 없이 `@container` 클래스 + `@sm:` `@md:` `@lg:` 변형 사용 가능. 뷰포트가 아닌 **부모 컨테이너 너비** 기준으로 스타일 적용. 단, container 브레이크포인트(`@md`=448px)는 viewport 브레이크포인트(`md`=768px)보다 작으므로 혼용 시 주의.

- **shadcn/ui Radix 통합 패키지 (2026-02)**: `@radix-ui/react-*` 개별 패키지들이 `radix-ui` 단일 패키지로 통합. new-york 스타일 사용 시 import 경로 변경 필요.

- **shadcn/ui Base UI 엔진 선택 가능 (2026-03 CLI v4)**: Radix UI ↔ Base UI 프리미티브 전환 가능, 동일한 컴포넌트 API 유지. 기존 ARIA 체크리스트는 두 엔진 모두 적용.

- **WCAG 2.2 SC 2.5.8 (AA): 타깃 크기 최소 24×24 CSS px** — 버튼·링크 등 인터랙티브 요소에 적용. 기존 SC 2.5.5(AAA, 44×44px)보다 완화된 AA 기준. 실무에서는 24px를 최저선으로 설계.

- **WCAG 2.2 SC 2.5.7 (AA): 드래그 대안 제공** — 드래그 인터랙션이 있으면 탭/클릭 대안 반드시 구현. 드래그 전용 UI 패턴(슬라이더, DnD 리스트) 설계 시 체크 항목 추가.

- **2026 디자인 시스템 방향: 거버넌스 플랫폼화** — 디자인 시스템이 문서에서 "AI 생성 UI에 규칙을 적용하는 거버넌스 레이어"로 진화. 토큰 기반 시스템이 AI 툴 연동의 핵심.

---

## 출처

- [Tailwind CSS v4 Container Queries: Modern Responsive Design — SitePoint](https://www.sitepoint.com/tailwind-css-v4-container-queries-modern-layouts/)
- [February 2026 - Unified Radix UI Package — shadcn/ui](https://ui.shadcn.com/docs/changelog/2026-02-radix-ui)
- [March 2026 - shadcn/cli v4 — shadcn/ui](https://ui.shadcn.com/docs/changelog/2026-03-cli-v4)
- [WCAG 2.2 New Success Criteria — TestParty](https://testparty.ai/blog/wcag-22-new-success-criteria)
- [12 UX/UI Design Trends Defining Product Design in 2026 — UXPin](https://www.uxpin.com/studio/blog/ui-ux-design-trends/)

---

## 위키화 후보

- **Tailwind v4 Container Queries 패턴** — `@container`/`@sm:`/`@md:` 사용법, viewport vs container 브레이크포인트 크기 비교표
- **WCAG 2.2 새 성공 기준 요약** — SC 2.5.8(타깃 크기), SC 2.5.7(드래그 대안), SC 2.4.11(포커스 미가림) 실무 체크리스트

---

## 프로필 반영 후보 (저위험)

- Tailwind v4 container query 사용 시 `@container` 마킹 + `@sm:`/`@md:` 변형 적용; container 브레이크포인트(`@md`=448px)는 viewport(`md`=768px)보다 작으므로 혼용 금지
- 인터랙티브 타깃(버튼·링크 등) 최소 크기는 WCAG 2.2 SC 2.5.8 기준 **24×24 CSS px** (AA); 드래그 인터랙션에는 탭/클릭 대안 제공 (SC 2.5.7)

---

## 승인 필요 (고위험)

- shadcn/ui 컴포넌트 작업 시 **Base UI 엔진 도입 고려 여부** — 현재 Radix UI 기준으로 ARIA 체크리스트가 작성돼 있으나, Base UI 선택 시 일부 ARIA 속성 동작 방식 차이 가능. 도입 전 프로젝트별 검토 필요.


## 추가 학습 (08:23 UTC)
---

## 오늘 배운 것

- **CSS Anchor Positioning 프로덕션 사용 가능**: `anchor-name` / `position-anchor` 속성 쌍으로 JS 없이 툴팁·팝오버 위치 지정. Chrome 125+, Firefox 132+, Safari 18.2+ 지원 — Floating UI 같은 JS 라이브러리를 기본 선택으로 쓸 이유 없음. `@position-try`(플립 동작)은 Safari 18.4+ 필요.

- **View Transitions API 브라우저 커버리지 ~92%**: SPA·MPA 모두 지원. 전환 시간은 **200–400ms** 유지 권장, 500ms 초과 금지. `view-transition-name` 동적 할당 후 전환 완료 시 반드시 정리(uniqueness violation 방지). `prefers-reduced-motion` 존중 필수.

- **EAA(유럽 접근성법) 2025-06-28 발효**: EU 서비스 대상 기업은 **WCAG 2.1 AA** 준수 의무(EN 301 549). 미준수 시 연매출 4% 또는 €10만 이하 과징금. EN 301 549가 WCAG 2.2로 업데이트 진행 중.

- **CSS 2026 추세 — 브라우저가 JS 역할 흡수**: Anchor Positioning + Popover API 조합으로 완전한 플로팅 UI를 CSS만으로 구현 가능. JS 의존 UI 패턴을 CSS 대체로 우선 검토하는 기준 필요.

## 출처

- [CSS Anchor Positioning: Complete Guide 2026 — DevToolbox](https://devtoolbox.dedyn.io/blog/css-anchor-positioning-guide)
- [CSS Anchor Positioning: Browser Support — TestMu AI](https://www.testmuai.com/learning-hub/css-anchor-positioning-browser-support/)
- [View Transitions API for SPA Navigation 2026 — DevToolbox](https://devtoolbox.dedyn.io/blog/css-view-transitions-complete-guide)
- [European Accessibility Act 2025 Compliance Guide — TestParty](https://testparty.ai/blog/european-accessibility-act-guide)

## 위키화 후보

- **CSS Anchor Positioning 패턴**: `anchor-name`/`position-anchor`/`position-area` 핵심 속성, 브라우저별 지원 현황, Popover API 조합 예시
- **View Transitions API 패턴**: SPA/MPA 전환 타이밍 가이드, `view-transition-name` 정리 패턴, reduced-motion 처리

## 프로필 반영 후보 (저위험)

- `툴팁·팝오버 구현 시 CSS Anchor Positioning + Popover API 우선 검토; JS 포지셔닝 라이브러리는 Safari < 18.2 지원 필요 시에만 fallback`
- `View Transitions 전환 시간은 200–400ms 유지; transition-name 동적 할당 시 완료 후 반드시 제거`

## 승인 필요 (고위험)

_(없음)_


## 추가 학습 (18:31 UTC)
---

## 오늘 배운 것

- **Tailwind v4 `field-sizing` 유틸리티**: `field-sizing-content` 클래스로 `<textarea>` 높이 자동조절을 JS 없이 구현 가능. 현재 위키·메모리에 미등록 신규 기능.
- **shadcn/ui "Rhea" 스타일**: 2026년 추가된 compact density 테마. 버튼·입력·카드 spacing이 기존 Default/New York보다 좁음. `shadcn/create`에서 Radix · Base UI 모두 선택 가능.
- **shadcn/ui Chart → Recharts v3**: Chart 컴포넌트가 Recharts v3 기반으로 업그레이드됨. 기존 Chart 코드 재사용 시 마이그레이션 필요.
- **WCAG 3.0 타임라인**: 2026년 3월 Working Draft 공개. Candidate Recommendation은 2027 Q4, 최종 권고안은 2028 이후. **현행 법적 기준은 WCAG 2.2 AA 유지** — 3.0 대응 시작 불필요.
- **Bento Grid**: 2026 레이아웃 주요 트렌드. 비대칭 모듈형 카드 블록으로 정보 밀도 확보. subtle background tint (카테고리별 색조)로 시각 구분.
- **Kinetic Typography**: CSS View Transitions + Animation API 조합으로 hero section 텍스트 움직임 트렌드 확산. `motion-safe:` 래핑 필수.

## 출처

- [Tailwind CSS v4: The Complete Guide for 2026 — DevToolbox](https://devtoolbox.dedyn.io/blog/tailwind-css-v4-complete-guide)
- [Changelog — shadcn/ui](https://ui.shadcn.com/docs/changelog)
- [Bento Grids & Beyond: 7 UI Trends Dominating Web Design 2026 — WriterDock](https://writerdock.in/blog/bento-grids-and-beyond-7-ui-trends-dominating-web-design-2026)
- [WCAG 3.0 Update March 2026 — RatedWithAI](https://ratedwithai.com/blog/wcag-3-0-march-2026-update-timeline)
- [For Review: WCAG 3 Working Draft – March 2026 — W3C](https://www.w3.org/WAI/news/2026-03-03/wcag3)
- [Design Guidelines for shadcn/ui with Tailwind v4 — ctxs.ai](https://ctxs.ai/weekly/shadcn-ui-tailwind-v4-7z8p3v)

## 위키화 후보

- **WCAG 3.0 로드맵**: 2026 Working Draft 현황 + 2028 이후 최종 권고안 예정 타임라인 정리 노트
- **shadcn/ui Rhea 스타일**: compact density 적용 시기·기준(밀도 높은 product UI), Rhea vs Default/New York 비교

## 프로필 반영 후보 (저위험)

- Tailwind v4 `field-sizing-content`로 textarea 자동 리사이즈 구현 시 JS 불필요 — 폼 컴포넌트 작업 시 우선 적용
- shadcn/ui Chart 컴포넌트 사용 시 Recharts v3 기반임을 명시, 기존 v2 코드 마이그레이션 가이드 선참조

## 승인 필요 (고위험)

_(없음)_


## 추가 학습 (18:32 UTC)
## 오늘 배운 것
- **Scroll-driven Animations가 2026년 베이스라인 진입** — Firefox·Safari 풀 지원, 프리픽스 없이 순수 CSS로 스크롤 타임라인 애니메이션 가능. `timeline-scope`로 DOM 분기 간 타임라인 공유. 단, 기존 규칙대로 `motion-safe:` 래핑 필수(SC 2.3.3).
- **`light-dark()` CSS 함수 베이스라인** — `--bg: light-dark(#fff, #1a1a2e)` 단일 선언으로 다크모드 처리. `color-mix()`·`oklch(from ...)` 상대 색상도 전 엔진 베이스라인 도달 → JS 워크어라운드 감소.
- **shadcn CLI v4 (2026-03)** — Base UI 프리미티브 정식 지원, 모든 컴포넌트에 `data-slot` 속성 부여(스타일 타깃팅), `toast` → `sonner` deprecated, `--diff`로 레지스트리 업데이트 사전 점검, `shadcn/skills`로 코딩 에이전트에 컴포넌트 컨텍스트 제공.
- **DTCG 디자인 토큰 W3C 표준 안정화** — Format Module v2025.10(2025-10-28) 첫 stable 릴리스, Adobe·Google·Meta·Figma 등 24개사 지원. 기존 내 3계층(primitive→semantic→component) 규칙이 이제 **공식 표준으로 코드화**됨. 토큰 채택률 56%→84% 급증, AI 코드 일관성 확보용 "계약" 역할.
- **EAA(유럽 접근성법) 2025-06-28 발효** — EU 대상 서비스(직원 10명+, 매출 200만 유로+)는 의무. **WCAG 2.2 Level AA가 가장 확실한 컴플라이언스 기준** — 내 기존 규칙과 일치, 법적 적용 범위 확대됨.

## 출처
- [2026 CSS Features You Must Know — Riad Kilani](https://blog.riadkilani.com/2026-css-features-you-must-know/)
- [What's New in CSS 2026 — modern.css](https://modern-css.com/whats-new-in-css-2026/)
- [shadcn/cli v4 Changelog (2026-03)](https://ui.shadcn.com/docs/changelog/2026-03-cli-v4)
- [Tailwind v4 — shadcn/ui](https://ui.shadcn.com/docs/tailwind-v4)
- [Understanding the EAA and WCAG 2.2 — OneTrust](https://www.onetrust.com/blog/understanding-the-european-accessibility-act-and-wcag-22/)
- [Design Tokens W3C 2026 — Malaka Venugopal Reddy](https://malakavenu.com/articles/design-tokens-w3c-2026)
- [Design Tokens Community Group](https://www.designtokens.org/)

## 위키화 후보
- `scroll-driven-animations-패턴` — CSS scroll/view timeline 베이스라인 + motion-safe 접근성 가이드 (한 줄: JS 없는 스크롤 애니메이션 구현·a11y 주의)
- `dtcg-design-tokens-표준` — W3C DTCG v2025.10 포맷 모듈, 3계층 구조 표준화 (기존 shadcn-토큰-계층 노트와 연결)

## 프로필 반영 후보 (저위험)
- 다크모드 구현 시 미디어쿼리 중복 대신 `light-dark()` CSS 함수 우선 사용(베이스라인 도달); 토큰 값에 직접 적용 가능.
- shadcn 컴포넌트 커스텀 시 `data-slot` 속성을 스타일 타깃으로 활용; `toast`는 `sonner`로 대체(deprecated).

## 승인 필요 (고위험)
- (없음 — 기존 3계층 토큰·WCAG 2.2 AA 규칙이 신규 표준/법규와 이미 정합)

## 신규 도구 후보 (에이전트/스킬)
- (없음)


## 추가 학습 (18:32 UTC)
---

## 오늘 배운 것

- **CSS Anchor Positioning — Baseline 2026 확정**: Chrome 125+, Firefox 147+, Safari 26+(Sep 2025 출시) 전 브라우저 기본 지원. 글로벌 커버리지 약 83%. `@position-try` 자동 뒤집기는 Safari 18.4+부터 지원. 기존 메모리의 "Safari < 18.2 fallback" 기준이 구식 — Safari < 17 혹은 Samsung Internet < 27 대응 필요 시에만 JS 포지셔닝 라이브러리 fallback이 정확한 현행 기준.
  - 출처: [CSS Anchor Positioning — Pockit Blog](https://pockit.tools/blog/css-anchor-positioning-api-complete-guide/), [TestMu AI](https://www.testmuai.com/learning-hub/css-anchor-positioning-browser-support/)

- **Popover API — Baseline Widely Available (2025-04)**: Safari 18.3 iOS 버그 수정 후 모든 주요 브라우저 프로덕션 기준 완성. z-index 없이 top layer 자동 처리, 외부 클릭·Esc 자동 닫힘 내장.
  - 출처: [web.dev — Popover Baseline](https://web.dev/blog/popover-baseline)

- **HTML Invoker Commands API — Baseline 2025**: `<button commandfor="target-id" command="show-modal">` 패턴으로 dialog·popover 선언적 제어. JS 없이 상호작용 구현 가능. 기존 `onclick`·이벤트리스너 의존도 감소.
  - 출처: [Declarative Dialog Menu — dbushell.com](https://dbushell.com/2026/02/12/declarative-dialog-menu-invoker-commands/), [CSS-Tricks — Invoker Commands](https://css-tricks.com/invoker-commands-additional-ways-to-work-with-dialog-popover-and-more/)

- **2026 디자인 트렌드 — Calm Interface**: 과잉 애니메이션·시각적 쇼 탈피. motion은 시스템 피드백 목적에 한정. 기존 `motion-safe:` 규칙과 방향 일치, 적용 범위 확대.
  - 출처: [Envato — UX/UI trends 2026](https://elements.envato.com/learn/ux-ui-design-trends)

- **Bento Grid 레이아웃 부상**: 불규칙 카드 격자. CSS Grid `grid-template-areas` + `span` 조합으로 구현. 모바일에서는 단일 컬럼으로 fallback 필수.
  - 출처: [UXPin — UI/UX Trends 2026](https://www.uxpin.com/studio/blog/ui-ux-design-trends/)

- **디자인 시스템 = 거버넌스 플랫폼**: 문서화 목적을 넘어 AI 생성 UI까지 규칙 강제 적용. 토큰·컴포넌트 스펙이 사람·AI 공통 소스오브트루스로 기능하는 방향으로 진화.
  - 출처: [UXPin — UI/UX Trends 2026](https://www.uxpin.com/studio/blog/ui-ux-design-trends/)

---

## 출처
- [CSS Anchor Positioning Complete Guide — Pockit Blog](https://pockit.tools/blog/css-anchor-positioning-api-complete-guide/)
- [CSS Anchor Positioning Browser Support — TestMu AI](https://www.testmuai.com/learning-hub/css-anchor-positioning-browser-support/)
- [Popover API is now Baseline — web.dev](https://web.dev/blog/popover-baseline)
- [Declarative Dialog Menu with Invoker Commands — dbushell.com](https://dbushell.com/2026/02/12/declarative-dialog-menu-invoker-commands/)
- [Invoker Commands — CSS-Tricks](https://css-tricks.com/invoker-commands-additional-ways-to-work-with-dialog-popover-and-more/)
- [UX/UI Design Trends 2026 — Envato](https://elements.envato.com/learn/ux-ui-design-trends)
- [12 UI/UX Trends 2026 — UXPin](https://www.uxpin.com/studio/blog/ui-ux-design-trends/)

---

## 위키화 후보
- **HTML Invoker Commands API 패턴** — `commandfor`/`command` 속성으로 JS 없이 dialog·popover 선언적 제어; Baseline 2025 도달로 실무 적용 가능
- **Bento Grid 레이아웃 패턴** — CSS Grid `grid-template-areas` + span 기반 불규칙 카드 격자; 모바일 fallback 패턴 포함

---

## 프로필 반영 후보 (저위험)
- `CSS Anchor Positioning Safari fallback 기준: Safari < 18.4(flip 미지원) / < 17(기능 미지원)로 세분화; 일반 포지셔닝은 Baseline 2026으로 JS fallback 불필요`
- `팝오버·다이얼로그 트리거는 Invoker Commands API(\`commandfor\`/\`command\`) 우선 적용; JS 이벤트 핸들러는 커스텀 로직 필요 시에만 사용`

---

## 승인 필요 (고위험)
_(없음)_

---

## 신규 도구 후보 (에이전트/스킬)
_(없음)_
