---
date: 2026-06-25
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-25

## 오늘 배운 것
- **의도 기반 적응형 UX (Intent-Based & Adaptive UX) 설계**: 고정된 레이아웃 대신 사용자의 사용 이력과 맥락, 목적에 맞춰 실시간으로 형태와 콘텐츠를 동적으로 조정하며 AI 인터랙션 최적화를 꾀하는 AI 네이티브 인터페이스 설계 기법입니다.
- **리퀴드 글래스 및 적응형 투명도 (Liquid Glass & Adaptive Transparency)**: 사용자 환경, 조명 및 상호작용 맥락에 반응하여 유기적인 깊이감과 투명도 조절 효과를 연출해 직관적인 계층 구성을 만드는 새로운 그래픽 비주얼 디자인 스타일입니다.
- **WCAG 2.2 SC 3.3.8 (AA) — 접근 가능한 인증 (Accessible Authentication - Minimum)**: 패스워드 암기나 퍼즐 풀기 등 인지 능력에 의존하는 테스트 없이도 사용자가 자동완성 및 복사-붙여넣기 수단을 통해 원활하게 로그인할 수 있는 접근성 기준을 확보해야 합니다.
- **shadcn/ui CLI v4의 에이전트 학습 기능 (Agentic Readiness — `shadcn/skills`)**: AI 코딩 에이전트에게 프로젝트 레지스트리 구성 및 디자인 토큰 규격 정보를 전용 컨텍스트 레이어로 제공하여 AI 코드 작성의 오류를 방지합니다.
- **shadcn/ui GitHub 기반 레지스트리 배포**: 별도의 전용 서버 구축 없이 프로젝트 루트에 `registry.json` 파일만 선언하면 모든 공개 GitHub 저장소를 컴포넌트 및 커스텀 훅 배포용 레지스트리로 쉽게 전환할 수 있습니다.
- **shadcn/ui CLI 기본 RTL(우향 쓰기) 자동 변환**: `components.json` 설정 파일에 RTL 옵션을 적용하거나 `migrate rtl` 명령을 실행해 기존 물리적 방향 클래스(예: `ml-*`, `text-left`)를 논리적 방향 클래스(예: `ms-*`, `text-start`)로 자동 전환합니다.

## 출처
- [Intent-Based UX Trend - UX Collective](https://uxdesign.cc)
- [Liquid Glass Visual Design - Orizon](https://orizon.co)
- [Tailwind CSS v4 CSS-First Model](https://tailwindcss.com)
- [WCAG 2.2 Success Criteria - W3C](https://www.w3.org/TR/WCAG22/)
- [shadcn/ui v4 CLI & Features](https://ui.shadcn.com)

## 위키화 후보
- `Intent-Based UX (IBUX)`: 사용자의 복잡한 탐색 및 명령어 입력 과정을 AI가 자율적으로 판단해 목적 중심의 경로로 단축해 주는 차세대 사용자 경험 설계 원리.
- `Accessible Authentication (접근 가능한 인증)`: 인지 장애가 있는 사용자들의 편리한 로그인을 위해 기억력 테스트를 배제하고 자동 완성 및 복사-붙여넣기를 보장하는 WCAG 2.2 AA 핵심 기준.

## 프로필 반영 후보 (저위험)
- `Liquid Glass Design material styling`: 입체적 시각 피드백과 가독성을 균형감 있게 충족하는 동적 투명도 제어 레이아웃 설계 기법.
- `shadcn/ui RTL Logical Mapping workflow`: CLI 자동 치환 엔진을 통해 기존 스타일 물리 속성을 흐름 상대적 논리 속성(CSS Logical Properties)으로 일괄 매핑하는 개발 기법.

## 승인 필요 (고위험)
- `shadcn/skills 컨텍스트 레이어 상시 선언 규칙`: 프로젝트 단위마다 AI 에이전트의 코드 파악 완성도를 보장하기 위해 `shadcn/skills` 파일 생성을 디자인 시스템 운영 기준으로 강제하는 방안.
- `CSS 논리적 클래스 전면 전환 가이드라인`: 향후 신규 마크업 코드 작성 시 `ml-` 및 `pr-` 대신 `ms-` 및 `pe-` 형태의 논리 방향 속성을 기본 정의하도록 코딩 스타일 가이드를 전면 개정하는 방안.

## 신규 도구 후보 (에이전트/스킬)
- `[agent] a11y-auditor — 마크업 결과물 내의 WCAG 2.2 신규 핵심 기준(SC 2.4.11 포커스 가려짐 최소화, SC 3.3.8 접근 가능한 인증) 위배 사항을 진단하고 자동 패치를 제안하는 에이전트`
- `[skill] logical-class-converter — Tailwind 및 일반 CSS 상의 물리 방향 클래스 값을 RTL 대응용 논리 방향 CSS 속성으로 일괄 마이그레이션해 주는 스킬`
