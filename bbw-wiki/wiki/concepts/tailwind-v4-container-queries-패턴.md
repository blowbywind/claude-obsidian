---
title: Tailwind v4 Container Queries 패턴
type: concept
status: ai-curated
learned_by: rina
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-rina-learning]]
summary: "Tailwind v4에서 지원하는 컨테이너 쿼리는 뷰포트가 아닌 부모 컨테이너 크기를 기준으로 자식 요소의 스타일을 반응형으로 조정하는 기법이다."
---

# Tailwind v4 Container Queries 패턴

## 핵심 정의

Container Query(컨테이너 쿼리)는 뷰포트 너비가 아닌 **부모 컨테이너의 크기를 기준**으로 자식 요소의 스타일을 조건부로 적용하는 반응형 설계 기법이다. 뷰포트 고정 레이아웃의 한계를 넘어 각 컴포넌트가 독립적인 반응성을 가지게 한다.

## 요점

**1. Tailwind v4.3.0부터 내장 지원**
- 별도 플러그인 없이 `@container` 클래스와 `@sm:` `@md:` `@lg:` 변형으로 바로 사용 가능
- `@container` 마킹 → 자식에 `@sm:`, `@md:` 변형 적용하는 구조

**2. 부모 컨테이너 크기 기준 스타일 적용**
- 뷰포트가 아닌 직계 부모 컨테이너의 너비를 기준으로 동작
- 같은 컴포넌트가 서로 다른 부모 너비에 따라 별도 스타일을 가짐

**3. 브레이크포인트 크기 혼용 주의**
- Container 브레이크포인트: `@md` = 448px
- Viewport 브레이크포인트: `md` = 768px
- 두 기준이 다르므로 같은 이름 변형을 혼용할 때 예상과 다른 결과 발생 가능

## 출처

- [Tailwind CSS v4 Container Queries: Modern Responsive Design — SitePoint](https://www.sitepoint.com/tailwind-css-v4-container-queries-modern-layouts/)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-rina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
