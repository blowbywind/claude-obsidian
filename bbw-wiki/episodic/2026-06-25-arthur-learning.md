---
date: 2026-06-25
bot: arthur
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 아서 자가학습 — 2026-06-25

## 오늘 배운 것
- **Tailwind CSS v4 CSS-First 및 Oxide 컴파일러**: JavaScript 설정 파일 없이 CSS 내 `@theme` 지시어로 디자인 토큰을 정의하며, Rust 기반 Oxide 컴파일러와 Lightning CSS 통합을 통해 Vite 빌드 성능을 향상시키고 native container queries 및 `@starting-style` 트랜지션을 지원함.
- **shadcn/ui CLI v4 AI 에이전트 및 RTL 지원**: `shadcn/skills`를 제공해 AI 코딩 에이전트에 프로젝트 상태를 전달함으로써 코드 생성 환각을 예방하고, `registry.json`을 통한 레지스트리 배포 및 물리 방향 클래스(`ml-*`)의 논리 방향 클래스(`ms-*`) 자동 RTL 변환 기능을 제공함.
- **WCAG 2.2 AA 모바일 접근성 최소 타겟 기준**: 터치 타겟 최소 크기를 24x24 CSS 픽셀로 규정하며, 키보드 포커스 가시성을 위해 최소 3:1 이상의 색상 대비율을 충족하도록 가이드함.
- **웹 접근성 수동 검증의 병행화**: 자동 진단 도구는 웹 접근성 문제의 약 20~40%만 검출할 수 있으므로, 실제 키보드 탐색과 스크린 리더 작동 여부에 대한 수동 검증 단계의 병행이 필수적임.
- **Adaptive UI 디자인 패러다임**: 사용자 실시간 맥락에 맞춰 디자인 시스템 컴포넌트를 동적으로 조합하는 Generative UI와, 빛·깊이감의 굴절과 유동적 투명도를 활용하는 Liquid Glass 시각 재질 스타일이 부상함.

## 출처
- [Tailwind CSS v4](https://tailwindcss.com)
- [shadcn/ui CLI v4](https://shadcn.com)
- [Generative UI - UXPin](https://uxpin.com)
- [Liquid Glass Trend - Orizon](https://orizon.co)
- [Calm UI Pattern - Envato](https://envato.com)
- [WCAG 2.2 Standard - AccessiTool](https://accessitool.com)
- [Accessibility Testing - Juicebox Interactive](https://juiceboxinteractive.com)

## 위키화 후보
- `Generative UI`: AI 기반 컴포넌트 실시간 동적 조합 및 화면 개인화 설계 패러다임
- `Liquid Glass`: 초현실적 깊이감, 굴절, 실시간 투명도를 반영하는 유동적 재질 시각 트렌드

## 프로필 반영 후보 (저위험)
- Tailwind CSS v4 `@theme` 토큰 관리 체계 및 `starting:` 트랜지션 활용 역량
- shadcn/ui CLI v4 `registry.json` 활용 커스텀 레지스트리 배포 및 RTL 변환 기능 적용 역량

## 승인 필요 (고위험)

## 신규 도구 후보 (에이전트/스킬)
- `[skill] shadcn-skills-sync` — `components.json` 및 의존성 설정을 기계가 읽기 쉬운 `shadcn/skills` 파일로 자동 업데이트하여 AI 코딩 에이전트와 동기화하는 도구
