---
title: css
type: concept
status: ai-curated
learned_by: arthur
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-arthur-learning]]
summary: "CSS @layer는 specificity에 무관하게 명시적 우선순위로 스타일 충돌을 예방하는 cascade layers 표준이다."
---

# css

CSS @layer는 **cascade layers**를 정의하는 CSS 표준으로, 셀렉터 specificity에 무관하게 스타일 우선순위를 명시적으로 제어한다.

## 핵심 개념

디자인 시스템에서 표준 레이어 순서를 따르면 스타일 충돌을 예방하고 유지보수성을 높일 수 있다:

1. **레이어 우선순위 구조**: `reset` → `defaults` → `tokens` → `layouts` → `components` → `utilities` → `overrides` 순으로 정의하면 specificity wars 없이 예측 가능한 스타일 적용이 가능하다.

2. **Tailwind v4와의 시너지**: Cascade Layers를 Tailwind와 함께 사용하면 유틸리티 클래스와 컴포넌트 스타일 간 충돌을 자동 방지하고, 설정 파일만으로 전체 시스템 스타일 순서를 관리할 수 있다.

3. **Variable Fonts와의 조합**: CSS 변수로 `font-weight`, `font-width`, `optical-size` 축을 토큰화하면, 단일 파일로 타이포그래피 브랜드 일관성과 성능 최적화를 동시에 달성한다.

## 출처

- https://www.designsystemscollective.com/mastering-css-cascade-layers-for-scalable-design-systems-981fdab2a961
- https://fontalternatives.com/blog/variable-fonts-brand-systems-2026/

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-arthur-learning]]. 사람 검증 후 status를 verified로 변경하세요.
