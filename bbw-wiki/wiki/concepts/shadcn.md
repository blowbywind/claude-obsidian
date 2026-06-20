---
title: shadcn
type: concept
status: ai-curated
learned_by: arthur
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-arthur-learning]]
---

# shadcn

Obsidian 위키 concept 노트 본문:

---

## 핵심 정의

**shadcn/ui**는 Radix UI 등 헤드리스 프리미티브 위에 구축된 복사 가능한 컴포넌트 라이브러리로, 설계 시스템을 단일 레포지토리에 소유하도록 한다. 2026년 기준 Base UI 지원, CLI v4 검수 플래그, 테마 다양화로 유연성을 확대했다.

## 주요 특징

**1. CLI v4 검수 플래그 (2026-03)**
`--dry-run`, `--diff`, `--view` 플래그로 컴포넌트 추가 전 변경 사항을 사전 검사할 수 있다. Presets 엔진으로 색상·테마·아이콘·폰트·border-radius 설정을 단일 문자열로 패키징해 일관성을 보장한다.

**2. Base UI 프리미티브 지원 (2026-01)**
Radix UI 외에 Base UI를 primitive layer로 선택 가능하며, `components.json` 한 줄 수정으로 전환된다. 마이그레이션 시 `asChild` 키워드를 제거해야 하고, Base UI는 번들이 더 작으며 복합 컴포넌트(Combobox·Autocomplete·중첩 Dialog)가 풍부하다.

**3. 테마 확장과 문서화 개선 (2026-03~04)**
Luma 테마는 softer surfaces, 넓은 spacing, calmer rhythm으로 기본 테마 대비 더 섬세한 느낌을 제공한다. 2026-04부터 각 컴포넌트 문서에 "Composition Tree" 섹션이 추가돼 올바른 중첩 계층을 명시한다.

## 출처
- https://ui.shadcn.com/docs/changelog/2026-03-cli-v4
- https://ui.shadcn.com/docs/changelog/2026-01-base-ui
- https://ui.shadcn.com/docs/changelog/2026-03-luma
- https://ui.shadcn.com/docs/changelog/2026-04-component-composition

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-arthur-learning]]. 사람 검증 후 status를 verified로 변경하세요.
