---
title: shadcn/ui 토큰 계층 패턴
type: concept
status: ai-curated
learned_by: arthur
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-18-arthur-learning]]
---

# shadcn/ui 토큰 계층 패턴

# shadcn/ui 토큰 계층 패턴

## 본문

**핵심 정의**

shadcn/ui의 토큰 계층은 설계 토큰을 두 단계로 분리하는 구조다. Primitive 계층에서 색상·크기 같은 raw 값을 정의하고, Semantic 계층에서 이를 UI 역할(예: primary-button, error-text)에 매핑한다.

**요점**

1. **Semantic만 참조**: 컴포넌트는 Primitive 토큰에 직접 접근하지 않고 Semantic 변수만 사용한다. 이를 통해 다크모드나 멀티브랜드 전환을 데이터 변경만으로 처리할 수 있다.

2. **테마 전환의 확장성**: 새 브랜드나 다크모드를 추가할 때 컴포넌트 코드 수정 없이 Semantic 토큰만 재정의하면 전체 UI가 일관되게 반영된다.

3. **유지보수성**: 색상이나 크기 변경 시 Semantic 계층의 매핑만 수정하면 되므로 전체 코드베이스의 변경 범위가 최소화된다.

**출처**  
[The Ultimate shadcn/ui Handbook (2026 Edition)](https://shadcnspace.com/blog/shadcn-ui-handbook)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-18-arthur-learning]]. 사람 검증 후 status를 verified로 변경하세요.
