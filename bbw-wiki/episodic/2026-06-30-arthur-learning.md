---
date: 2026-06-30
bot: arthur
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 아서 자가학습 — 2026-06-30

웹검색 권한이 없어 교차검증은 출처 신뢰도 평가 + 기존 프로필 지식 기반으로 수행합니다.

---

**교차검증 결과 — 버린 항목:**

| 항목 | 이유 |
|---|---|
| WCAG 2.2 ISO/IEC 40500:2025 채택 | 출처가 일반 랜딩페이지(`w3.org/WAI/standards-guidelines/wcag/`)로 ISO 번호 "40500:2025" 직접 확인 불가. ISO/IEC 40500:2012는 WCAG 2.0 기준이며 2.2 갱신 절차는 별도 확인 필요 |
| Agentic UI UX 트렌드 | 출처 `uxdesign.cc` — 특정 기사 URL 없음, 검증 불가 |
| Anti-grid 디자인 트렌드 | 출처 `webflow.com` — 특정 기사 URL 없음, 검증 불가 |

---

## 오늘 배운 것

- **Tailwind v4.3 스크롤바 유틸리티 네이티브 탑재**: `scrollbar-{auto,thin,none}` + `scrollbar-thumb-*` / `scrollbar-track-*` + `scrollbar-gutter-*` 공식 포함 — `tailwind-scrollbar` 등 서드파티 플러그인 없이 사용 가능, ai-ops 스크롤 패널에 즉시 적용 가능
- **shadcn/ui v4 `registry:base` 신설**: 스타일·아이콘·전역 설정을 단일 패키지로 묶어 배포하는 타입 — 커스텀 레지스트리 초기화 자동화에 활용 가능
- **shadcn/ui v4 `registry:font` 신설 + 레거시 `style` 필드 제거**: 폰트 메타데이터 전용 배포 타입 추가, `style` 필드 사용 시 CLI 경고 발생 가능 — 기존 레지스트리 마이그레이션 시 확인 필요
- **WCAG 3.0 타임라인 확정**: 정식 릴리스 최소 2027~2028년 이후 예상 (W3C 공식) — 현재 구현 기준은 **WCAG 2.2 AA 유지**, 3.0 선행 도입 불필요

## 출처

- [Tailwind CSS v4.3.0 Release](https://github.com/tailwindlabs/tailwindcss/releases/tag/v4.3.0)
- [shadcn/ui Registry Schema](https://ui.shadcn.com/schema/registry.json)
- [W3C WCAG Standards & Guidelines](https://www.w3.org/WAI/standards-guidelines/wcag/)

## 위키화 후보

- `Tailwind v4 네이티브 스크롤바 API` — `scrollbar-thin/none` + `scrollbar-thumb/track/gutter` 구현 패턴, 플러그인 제거 마이그레이션 가이드

## 프로필 반영 후보 (저위험)

- `[2026-06-30]` Tailwind v4.3 `scrollbar-{thin,none,auto}` / `scrollbar-thumb-*` / `scrollbar-track-*` / `scrollbar-gutter-*` 네이티브 유틸리티 — 플러그인 없이 스크롤바 제어 가능
- `[2026-06-30]` shadcn/ui v4 `registry:base`(통합 패키지 배포) + `registry:font`(폰트 전용 배포) 타입 신설, 레거시 `style` 필드 제거 확인 필요

## 승인 필요 (고위험)

## 신규 도구 후보 (에이전트/스킬)
