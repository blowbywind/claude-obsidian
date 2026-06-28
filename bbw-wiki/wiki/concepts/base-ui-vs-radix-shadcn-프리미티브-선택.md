---
title: Base UI vs Radix (shadcn 프리미티브 선택)
type: concept
status: ai-curated
learned_by: arthur
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-arthur-learning]]
summary: "shadcn/ui가 Base UI(번들소형·복합컴포넌트풍부)와 Radix 프리미티브 지원하며, components.json으로 전환 가능."
---

# Base UI vs Radix (shadcn 프리미티브 선택)

## 핵심 정의

shadcn/ui는 2026년부터 Radix Primitives 외에 **Base UI를 선택 가능한 primitive layer**로 지원한다. Base UI는 MUI 팀과 Radix·Floating UI 창립자들이 참여해 개발 중이며, `components.json` 한 줄로 두 프리미티브 간 전환이 가능하다.

## 선택 기준

**Base UI의 장점**:
- 번들 사이즈가 더 작음
- Combobox, Autocomplete, 중첩 Dialog 등 복합 컴포넌트 기본 제공
- 2026년 기준 더 활발한 유지보수 중

**마이그레이션 방식**:
- `components.json`의 프리미티브 선택만 변경하면 블록도 자동 생성
- Radix → Base UI 전환 시 `asChild` 키워드를 전체 제거하고 점진적으로 컴포넌트별 교체 권장

## 출처

- [January 2026 - Base UI Documentation - shadcn/ui](https://ui.shadcn.com/docs/changelog/2026-01-base-ui)
- [shadcn vs Radix vs Base UI — 2026](https://dev.to/edriso/shadcn-vs-radix-vs-base-ui-which-one-should-a-junior-pick-in-2026-1jml)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-arthur-learning]]. 사람 검증 후 status를 verified로 변경하세요.
