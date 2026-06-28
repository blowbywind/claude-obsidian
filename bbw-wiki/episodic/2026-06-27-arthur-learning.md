---
date: 2026-06-27
bot: arthur
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 아서 자가학습 — 2026-06-27

WebSearch 권한이 없다. 위키 grep 결과와 자체 지식으로만 교차검증한다.

---

**검증 전처리 요약:**

| 항목 | 판정 | 근거 |
|---|---|---|
| Intent-based / Ambient 디자인 | **중복** | wiki/concepts/_drafts, 2026-06-25 리나 학습 이미 있음 |
| Liquid Glass / Glassmorphism 2.0 | **중복** | wiki/concepts/liquid-glass.md, 2026-06-21 리나 학습 |
| scrollbar-* 유틸리티 (v4.3) | **중복** | wiki/concepts/tailwind.md에 이미 서술됨 |
| zoom-*, tab-*, @container-size (v4.3) | **중복** | 프로필 [2026-06-26] 반영 완료 |
| shadcn/skills, --preset, RTL 변환 | **중복** | 프로필 [2026-06-24], [2026-06-25] 반영 완료 |
| Tailwind v4.2 mauve/olive/mist/taupe | **검증 불가** | 전일(2026-06-26) 리나도 "공식 확인 불가" 판정, WebSearch 실패 |
| Tailwind v4.2 `pbs-*`/`mbs-*` 논리적 속성 | **검증 불가** | 출처 URL이 임시 Google grounding 리다이렉트, WebSearch 실패 |
| Accessibility-First Architecture | **부분 검증** | 개념 실재하나 "주류" 주장은 출처 없음 → 핵심만 채택 |
| `forced-colors` + OS 접근성 연동 | **신규 검증** | CSS Color Adjustment Level 1 표준, MDN 문서화 실재 |

---

## 오늘 배운 것

- **`forced-colors` 미디어 쿼리**: `prefers-reduced-motion`과 쌍을 이루는 OS 접근성 설정 존중 패턴. `@media (forced-colors: active)` 내에서 `ButtonText`·`ButtonFace` 등 CSS 시스템 색상 키워드를 사용해야 고대비 모드에서 하드코딩 색상 강제 교체를 방지할 수 있음. 기존 프로필의 `prefers-reduced-motion` 적용 원칙과 같은 계층에 위치.
- **접근성 우선 아키텍처 방향성**: WCAG 색상 대비·포커스·ARIA 기준을 Primitive 토큰 정의 시점에 매핑(예: `--color-interactive` 토큰 자체가 4.5:1 대비 보장)하면 컴포넌트 단에서 별도 검증 불필요. 기존 프로필의 "Primitive → Semantic 2단 계층"과 결합하면 접근성이 자동 상속되는 구조 가능.
- **리서치 결과 품질 판정**: vertexaisearch grounding API 리다이렉트 URL은 검증 불가 출처 — 해당 형식의 URL을 1차 출처로 수락 금지.

## 출처

- [CSS Color Adjustment Module Level 1 — forced-colors (MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/forced-colors)

## 위키화 후보

- `forced-colors` 미디어 쿼리 — `prefers-reduced-motion`과 함께 OS 접근성 페어 패턴으로 wiki/concepts/accessibility.md에 추가 가치 있음

## 프로필 반영 후보 (저위험)

- `forced-colors: active` + CSS 시스템 색상 키워드 패턴을 기존 `prefers-reduced-motion` 항목과 묶어 "OS 접근성 미디어 쿼리 페어" 항목으로 추가

## 승인 필요 (고위험)

_없음_

## 신규 도구 후보 (에이전트/스킬)

_없음_
