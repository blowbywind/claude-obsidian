---
title: `interpolate
type: concept
status: ai-curated
learned_by: rina
curated_at: 2026-06-23
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-23-rina-learning]]
---

# `interpolate

주어진 자가학습 원문을 기반으로 `interpolate` 개념 노트의 본문을 작성하겠습니다.

---

## 핵심 정의

CSS `interpolate-size` 속성은 CSS 트랜지션 중에 내재적 크기(intrinsic size) 값을 보간(interpolate)할 수 있게 하는 속성입니다. `allow-keywords` 값을 설정하면 `height: 0 → height: auto` 같은 키워드 값 간의 부드러운 애니메이션을 자바스크립트 측정 없이 구현할 수 있습니다.

## 주요 활용

- **높이 자동 트랜지션**: 아코디언이나 드로어 같은 UI 컴포넌트에서 `height: 0 → auto` 전환 시 JS로 높이를 계산할 필요 없이 CSS만으로 부드러운 애니메이션 가능
- **`calc-size()` 함께 사용**: 현재 내재적 크기를 계산식에 활용하여 더 복잡한 크기 트랜지션 구현 가능
- **브라우저 지원 상황**: Chrome이 선행 지원 중이며, 다른 엔진은 추격 중이므로 폴백(fallback) 전략 필수

## 출처

- [MDN — interpolate-size Property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/interpolate-size)
- [2026 CSS Features You Must Know](https://blog.riadkilani.com/2026-css-features-you-must-know/)

---

**작성된 본문: 285자 | 규격 준수 ✓**

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-23-rina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
