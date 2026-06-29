---
title: `forced
type: concept
status: ai-curated
learned_by: arthur
curated_at: 2026-06-27
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-27-arthur-learning]]
summary: "운영체제 고대비 모드 활성 시 CSS 색상을 시스템 키워드로 자동 교체하는 forced-colors 미디어 쿼리로 WCAG 접근성 준수."
---

# `forced

`forced-colors` 개념 노트를 작성하겠습니다.

---

## 핵심 정의

`forced-colors`는 운영체제 고대비 모드(High Contrast Mode) 활성화 여부를 감지하는 CSS 미디어 쿼리입니다. `@media (forced-colors: active)` 문법으로 웹사이트가 OS 접근성 설정을 존중하도록 스타일을 분기할 수 있습니다.

## 핵심 요점

**1. 시스템 색상 키워드 강제 사용**  
고대비 모드 활성 시 개발자가 지정한 `color: #3498db` 같은 하드코딩 색상은 무시되고, 대신 `ButtonText`·`ButtonFace`·`CanvasText` 등 CSS 시스템 색상 키워드로 교체됩니다. `forced-colors: active` 블록 내에서는 명시적으로 이 키워드들을 사용해야 의도한 대비를 보장합니다.

**2. `prefers-reduced-motion`과 함께 OS 접근성 페어**  
동작 축소 선호(`prefers-reduced-motion`)와 대비 선호(`forced-colors`)는 모두 OS 시스템 수준 접근성 설정입니다. 둘 다 사용자 의도를 우선하므로 WCAG 준수 구현에서는 함께 고려해야 합니다.

**3. 하드코딩 색상 자동 교체 방지**  
고대비 모드에서 시각장애인이나 저시력자가 읽을 수 없는 색상 조합이 자동으로 강제 교체되도록 OS에서 관리하므로, 개발자는 `forced-colors` 미디어 쿼리로 선제적으로 시스템 색상을 따르도록 구현하면 예측 불가능한 스타일 깨짐을 방지할 수 있습니다.

## 출처

- [CSS Color Adjustment Module Level 1 — forced-colors (MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/forced-colors)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-27-arthur-learning]]. 사람 검증 후 status를 verified로 변경하세요.
