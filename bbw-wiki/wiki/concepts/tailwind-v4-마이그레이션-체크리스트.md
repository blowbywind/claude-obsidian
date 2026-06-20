---
title: Tailwind v4 마이그레이션 체크리스트
type: concept
status: ai-curated
learned_by: arthur
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-18-arthur-learning]]
---

# Tailwind v4 마이그레이션 체크리스트

## Tailwind v4 마이그레이션 체크리스트

Tailwind CSS v3에서 v4로 업그레이드할 때 설정·클래스명·성능 변경을 체계적으로 점검하는 문서.

### 핵심 체크 항목

**1. 설정 파일 마이그레이션**
- `tailwind.config.js` 삭제
- CSS 파일에서 `@import "tailwindcss"` 추가
- `@theme` 디렉티브로 토큰 정의로 전환

**2. 클래스명 변경 확인 및 적용**
- `flex-shrink-0` → `shrink-0`
- `bg-gradient-to-*` → `bg-linear-to-*`
- (IDE 검색/치환 또는 `@tailwindcss/upgrade` CLI 활용)

**3. 성능 및 신기능 검증**
- Lightning CSS(Rust) 기반 incremental 빌드 100배 향상 확인
- Container Queries(`@min-*`, `@max-*`) 코어 포함으로 반응형 단순화 검토
- `prefers-reduced-motion`과 `:focus-visible`로 WCAG 2.2 AA 기준 충족 점검

## 출처

- [Tailwind CSS v4.0 공식 릴리즈 노트](https://tailwindcss.com/blog/tailwindcss-v4)
- [Tailwind CSS v4 Migration Guide 2026](https://www.digitalapplied.com/blog/tailwind-css-v4-migration-new-features-guide)
- [Web Accessibility 2026 — Frontend Survival Guide](https://www.codewithseb.com/blog/web-accessibility-2026-eaa-ada-wcag-guide)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-18-arthur-learning]]. 사람 검증 후 status를 verified로 변경하세요.
