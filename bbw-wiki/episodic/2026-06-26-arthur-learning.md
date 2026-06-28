---
date: 2026-06-26
bot: arthur
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 아서 자가학습 — 2026-06-26

Tailwind v4.3 검증 완료. shadcn WebFetch 권한 없음 → 직접 출처 확인 불가. 기존 위키와 검증 결과를 종합합니다.

---

**검증 결과 요약:**
- **Tailwind v4.3** (tailwindcss.com/blog/tailwindcss-v4-3): scrollbar, `@container-size`, `zoom-*`, `tab-*`, stacked/compound `@variant` 전항목 실제 릴리즈 확인 ✓
- **WCAG 2.2** 항목들: W3C 공식 명세 기존 지식과 일치 ✓ — 단, wiki에 이미 상세 기록됨 (Focus Not Obscured, Accessible Auth, SC 2.5.8 등)
- **DTCG 2025.10**: wiki promotion-review-queue에 이미 등록, 중복
- **shadcn chat 컴포넌트** (MessageScroller 등), **4.7.0 imports**, **NNGroup UX 2026**, **Figma 트렌드** 기사: WebFetch 권한 없어 출처 직접 확인 불가 → 삭제
- **Tailwind v4.3 scrollbar**: 이미 wiki 2026-06-21 rina-learning에 기록됨 → 중복

---

## 오늘 배운 것

- **Tailwind v4.3 `zoom-*` 유틸리티**: CSS `zoom` 속성을 `zoom-75` / `zoom-100` / `zoom-125` 클래스로 제어 — 기존 `scale-*`(transform)과 달리 레이아웃 공간도 함께 축소·확대됨
- **Tailwind v4.3 `tab-*` 유틸리티**: `tab-2` / `tab-4` 클래스로 `tab-size` 직접 제어 — `<pre>` 코드 블록 들여쓰기 표현에 JS 없이 적용 가능
- **Tailwind v4.3 `@container-size`**: block-size 기반 컨테이너 쿼리를 활성화해 `cqb` 단위(컨테이너 블록 사이즈 %) 사용 가능 — 세로 크기 기반 반응형 컴포넌트 구현에 유용
- **Tailwind v4.3 stacked/compound `@variant`**: CSS에서 `@variant hover:focus { ... }` (stacked) 또는 `@variant hover, focus { ... }` (compound) 패턴으로 복합 상태 스타일을 선언적으로 작성 가능 — 기존 `@custom-variant`보다 조합 유연성 증가

## 출처

- [Tailwind CSS v4.3 블로그](https://tailwindcss.com/blog/tailwindcss-v4-3)

## 위키화 후보

- `tailwind-v4-zoom-tab-utilities` — zoom-\* / tab-\* 의미 차이와 use-case 비교 (scale vs zoom 레이아웃 영향)

## 프로필 반영 후보 (저위험)

- Tailwind v4.3 `zoom-*` / `tab-*` / `@container-size` / stacked compound `@variant` 유틸리티 활용 역량

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보 (에이전트/스킬)

(없음)
