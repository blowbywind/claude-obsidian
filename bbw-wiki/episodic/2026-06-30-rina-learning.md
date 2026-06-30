---
date: 2026-06-30
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-30

교차검증 완료. 항목별 처리 결과:

| 항목 | 출처 신뢰도 | 판정 |
|---|---|---|
| Tailwind v4 `@theme {}` | tailwindcss.com ✅ | **중복** — [2026-06-18] 기존 메모리 |
| shadcn data-slot | ui.shadcn.com ✅ | **중복** — [2026-06-20] 기존 메모리 |
| shadcn OKLCH 전환 | ui.shadcn.com ✅ | **신규** — wiki design.md에 한 줄만 언급, 독립 노트 없음 |
| shadcn React 19 forwardRef 제거 | ui.shadcn.com ✅ | **신규** — wiki/메모리 모두 미기록 |
| CSS Anchor Positioning Baseline 2026 | MDN ✅ | **보강** — [2026-06-20] 기존 규칙에 수치 추가 |
| Popover API + Anchor 결합 | MDN ✅ | **중복** — [2026-06-20] 기존 메모리 |
| AI 디자인 시스템 Semantic Intelligence | supernova.io ⚠️ | **폐기** — 툴 벤더 마케팅 문서, W3C/MDN 뒷받침 없음 |
| Adaptive UI 트렌드 | sanjaydey.com ⚠️ | **폐기** — 개인 블로그, 출처 불충분 |

---

## 오늘 배운 것

- **shadcn/ui 기본 색상 공간이 HSL → OKLCH로 전환됨.** P3 디스플레이에서 더 넓은 색역·지각 균등 밝기 조정이 가능. 커스텀 토큰 선언 시 `oklch()` 사용 고려 (`--color-primary: oklch(0.6 0.15 250)`).
- **shadcn/ui React 19 대응으로 `forwardRef` 래퍼가 전 컴포넌트에서 제거됨.** React 19는 `ref`를 일반 prop으로 처리하므로 커스텀 래퍼가 `forwardRef()`를 감싸던 패턴은 직접 `ref` prop 전달 방식으로 교체 필요.
- **CSS Anchor Positioning Baseline 2026 확정 — Chrome 125+, Firefox 132+, Safari 18.2+, 전 세계 트래픽 약 91% 커버.** 기존 규칙 보강: `JS 포지셔닝 라이브러리 fallback`은 Safari < 18.2 지원이 명시적 요구사항인 경우에만 적용 (사실상 대부분 신규 프로젝트는 JS 라이브러리 불필요).

## 출처

- [shadcn/ui 공식](https://ui.shadcn.com) — OKLCH 전환, React 19 forwardRef 제거, data-slot
- [MDN CSS Anchor Positioning](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Anchor_Positioning) — Baseline 2026, 브라우저 지원 현황

## 위키화 후보

- `oklch-색상-공간-디자인토큰` — OKLCH vs HSL 비교, shadcn/ui 실사용 패턴, P3 폴백 전략

## 프로필 반영 후보 (저위험)

- `shadcn/ui React 19 forwardRef 제거` — 커스텀 컴포넌트 래퍼 작업 시 `forwardRef` 패턴 확인 체크리스트 추가

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보 (에이전트/스킬)

(없음)
