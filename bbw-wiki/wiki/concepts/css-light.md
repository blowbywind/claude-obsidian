---
title: CSS `light
type: concept
status: ai-curated
learned_by: rina
curated_at: 2026-06-24
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-24-rina-learning]]
summary: "CSS light-dark() 함수로 라이트/다크 모드 색상을 한 번에 지정하고 color-scheme과 연계하여 미디어쿼리 중복을 제거하며 테마 전환을 자동화합니다."
---

# CSS `light

CSS `light-dark()` 함수에 대한 Obsidian 위키 노트 본문을 작성하겠습니다.

---

## 📝 노트 본문

`light-dark()`는 CSS 색상 함수로, 라이트/다크 모드에서 각각 다른 색상값을 일괄 지정할 수 있습니다.

### 핵심 정의
라이트와 다크 테마 간 색상 전환을 단일 속성으로 처리하는 CSS 함수. 기존 `@media (prefers-color-scheme)` 미디어쿼리 중복을 제거하고, `color-scheme: light dark` 선언과 함께 사용하여 전역 설정만으로 모든 컴포넌트의 색상 토큰을 자동 적용합니다.

### 요점
1. **미디어쿼리 중복 제거**: 라이트/다크 색상을 미디어쿼리로 따로 작성하던 방식 대신 `light-dark(라이트값, 다크값)` 형식으로 한 줄에 정의
2. **`color-scheme` 연계**: `:root`나 최상단 요소에 `color-scheme: light dark` 지정하면, 사용자 OS/브라우저 설정에 따라 자동으로 `light-dark()` 값이 전환
3. **토큰 일괄 적용**: CSS 변수 + `light-dark()`를 조합하면 다크모드 대응 코드 증가 없이 디자인 토큰만 수정해 전역 테마 변경 가능

### 출처
- [MDN Web Docs - light-dark()](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/light-dark)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-24-rina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
