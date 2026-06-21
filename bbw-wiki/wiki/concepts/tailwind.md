---
title: `tailwind
type: concept
status: ai-curated
learned_by: rina
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-rina-learning]]
---

# `tailwind

Obsidian 위키 큐레이터로서 자가학습 원문의 "tailwind" 개념 노트 본문을 작성하겠습니다.

---

## 핵심 정의

**Tailwind CSS v4.3** (2026-05-08 출시)은 유틸리티 우선 CSS 프레임워크의 최신 버전으로, 스크롤바 커스텀·컨테이너 쿼리·부정 변형 등 CSS 근시일 기능을 퍼스트파티 유틸리티로 제공하여 JavaScript 의존도를 낮추고 브라우저 호환성을 확보한 버전입니다.

## 요점

1. **`scrollbar-*` 유틸리티**: `scrollbar-auto`, `scrollbar-thin`, `scrollbar-none`으로 scrollbar-width를 제어하며, 색상 유틸리티와 gutter 예약을 지원해 기존 써드파티 플러그인(`tailwind-scrollbar`) 대체 가능.

2. **`@container-size` 확장**: 기존 inline-size 기반 `@container`와 달리 너비·높이 기반 size 컨테이너 쿼리 추가로 정사각 컨테이너 조건 분기 가능.

3. **`not-*` 변형**: 특정 variant·selector·미디어 쿼리와 매치되지 않을 때만 스타일 적용(예: `not-hover:opacity-50`으로 호버 상태 제외).

4. **`color-mix()` 내장**: 논리적 프로퍼티 유틸리티 확장으로 동적 색상 혼합 지원.

## 출처 URL

- https://tailwindcss.com/blog
- https://devtoolbox.dedyn.io/blog/tailwind-css-v4-complete-guide

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-rina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
