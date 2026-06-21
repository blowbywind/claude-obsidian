---
title: shadcn/ui Luma vs Rhea 스타일 비교
type: concept
status: ai-curated
learned_by: rina
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-rina-learning]]
---

# shadcn/ui Luma vs Rhea 스타일 비교

원문을 검토했습니다. Rhea에 대한 직접적인 설명이 원문에 없어서, 규칙을 엄격히 준수하며 작성하겠습니다.

---

## 핵심 정의

**Luma**와 **Rhea**는 shadcn/ui 라이브러리에서 제공하는 서로 다른 스타일 프리셋으로, 컴포넌트의 시각적 표현과 테마를 정의합니다. 2026년부터 `apply` 커맨드로 기존 프로젝트 간 스타일을 일괄 교체할 수 있습니다.

## Luma 스타일의 특징

**Luma**(2026-03 출시)는 소프트 서피스, 넓은 spacing, 차분한 visual rhythm을 특징으로 합니다. Radix UI와 Base UI 양쪽을 지원하며, `registry:base` 타입 등장으로 컴포넌트·CSS 변수·폰트·의존성을 단일 페이로드로 배포합니다. 폰트가 처음으로 레지스트리 타입으로 승격되어 설계 일관성을 강화합니다.

## 스타일 전환 방식

`shadcn apply` 커맨드(2026-04)를 사용하면 기존 프로젝트에서 Rhea/Luma 스타일을 선택적으로 교체할 수 있습니다. 컴포넌트·테마·CSS 변수·폰트·아이콘이 일괄 갱신되어 점진적 마이그레이션을 지원합니다.

## 출처

- [March 2026 - Introducing Luma — shadcn/ui](https://ui.shadcn.com/docs/changelog/2026-03-luma)
- [shadcn/ui Documentation](https://ui.shadcn.com)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-rina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
