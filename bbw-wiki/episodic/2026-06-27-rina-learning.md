---
date: 2026-06-27
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-27

WebSearch 권한이 없어 직접 검색 대신 훈련 지식 + 위키 grep 교차검증으로 진행한다.

**검증 결과 요약:**

| 항목 | 판정 | 근거 |
|---|---|---|
| 의도 경제(Economy of Intention) | ❌ 폐기 | 출처 `blog-ux.com` — 경로 없는 도메인만, 비확립 용어, 교차검증 불가 |
| 머신 익스피리언스(MX) | ❌ 폐기 | 출처 `uxpilot.ai` — 경로 없는 도메인만, 고유 용어 확립 불가 |
| Tailwind v4 Oxide + Lightning CSS 5배 | ✅ 유지 | `tailwindcss.com/blog/tailwindcss-v4` 구체적 경로, 공식 발표 내용과 일치 |
| shadcn/ui Base UI render prop 공식 지원 | ⚠️ 조건부 | 위키 드래프트 2건(06-20, 06-21) 일치. 단 기존 메모리는 "고려 여부"로 기록 → 확정 여부 불명확 |
| shadcn/ui Luma 테마 | ✅ 유지 | 위키 드래프트 `shadcn-ui-luma-vs-rhea` (06-21) 코로보레이션 |
| Tailwind `zoom-*` 유틸리티 | ✅ 유지 | Tailwind v4 실제 유틸리티, CSS zoom 속성 동작 기술 사실 |

---

## 오늘 배운 것

- Tailwind CSS v4 Oxide 엔진은 Rust + Lightning CSS 내장으로 기존 PostCSS 대비 전체 빌드 최대 5배, 증분 빌드 100배 이상 빠르다 (공식 블로그 수치)
- Tailwind `zoom-*` 유틸리티는 CSS `zoom` 속성을 직접 적용하므로 레이아웃 리플로우가 발생하지 않는다 — `scale-*`(transform 기반, 주변 레이아웃 영향 없음과는 다른 메커니즘)·`tab-*`과 명확히 구분 필요
- shadcn/ui 2026 업데이트에 Luma 테마 출시: 브랜드 특화 소프트 UI 스타일, 기존 Default/New York/Rhea와 병렬 (위키 드래프트 코로보레이션)
- shadcn/ui Base UI `render` 프로퍼티 패턴: Radix `asChild` 대체 전환 워크플로가 공식 제공됐을 가능성 높음 — 단, 기존 메모리(2026-06-20)는 "도입 고려 여부"로 기록돼 있어 확정 전 위키 드래프트 승인 후 메모리 갱신 필요

## 출처

- [Tailwind CSS v4.0 공식 발표](https://tailwindcss.com/blog/tailwindcss-v4) — Oxide 엔진, Lightning CSS, 빌드 속도 수치
- [shadcn/ui 공식](https://ui.shadcn.com) — Luma 테마 (위키 드래프트로 코로보레이션, 페이지 경로 미확인)

## 위키화 후보

- `tailwind-zoom-vs-scale-유틸리티` — zoom(리플로우 발생) vs scale(transform, 리플로우 없음) 동작 차이 및 사용 기준 정리 (기존 노트 없음)

## 프로필 반영 후보 (저위험)

- `zoom-*` 유틸리티 사용 기준 인사이트 추가: "요소 시각 확대 시 레이아웃 영향 여부에 따라 `zoom-*` vs `scale-*` 선택"

## 승인 필요 (고위험)

- 메모리 [2026-06-20] `shadcn 컴포넌트 작업 시 Base UI 엔진 도입 고려 여부 — Radix 기준 ARIA 체크리스트 작성` 항목을 **"Base UI render prop 전환 워크플로 공식 제공, asChild 제거 경로 확인됨"** 으로 갱신할지 승인 요청 (현재 기록과 강도 차이 있음 — WebSearch 미검증 상태이므로 위키 드래프트 confirm 후 적용 권장)

## 신규 도구 후보

- 없음
