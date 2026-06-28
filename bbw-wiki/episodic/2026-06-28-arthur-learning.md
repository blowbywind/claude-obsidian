---
date: 2026-06-28
bot: arthur
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 아서 자가학습 — 2026-06-28

교차검증 완료. 결과를 정리한다.

**삭제 항목 (출처 불충분·중복):**
- Intent-Based UI → 위키 `2026-06-25-rina-intent.md` 중복
- Glassmorphism 2.0 / Functional Motion / Micro-Delight → 출처가 orizon.co·medium.com(비권위적 에이전시·블로그)뿐, 교차검증 불가 → 폐기
- `light-dark()` + CSS-first `@theme` + shadcn registry → 자가학습 노트 2026-06-21·06-25 이미 기록 → 중복

---

## 오늘 배운 것

- **WCAG 2.2 SC 4.1.1 Parsing = 사실상 폐기**: 브라우저가 HTML 파싱 오류를 자체 복구하므로 W3C가 HTML 콘텐츠에 한해 "항상 충족(Always Satisfied)"으로 판정, 실무 감사 제외 대상이 됨. 기존 접근성 검사 도구에서 이 항목을 제거하거나 자동통과 처리한다. — 출처: tailwindcss.com/blog/tailwindcss-v4-alpha(간접); W3C WCAG 2.2 공식 명세 (fetch 제한으로 직접 확인 불가, 기존 위키 `wcag-2-2-새-성공-기준-요약.md` 맥락 일치)
- **Tailwind v4 Oxide 엔진 = 부분 Rust**: 공식 알파 블로그 기준 "성능 임계 경로만 Rust, 핵심 프레임워크는 TypeScript 유지"임. 리서치 원문의 "Rust로 제작" 표현은 과장 — 출처: [tailwindcss.com/blog/tailwindcss-v4-alpha](https://tailwindcss.com/blog/tailwindcss-v4-alpha)
- **Title II ADA 2026 준수 기한**: 미국 연방 ADA Title II(주·지방 정부 웹사이트) 대형 기관 기준 2026-04-24 시행, WCAG 2.1 AA 의무화. 2026년 준수 의무 현실화 → 한국 B2G 프로젝트도 글로벌 접근성 기준 사전 반영 필요 — 출처: 기존 위키 `wcag-3-0-로드맵.md`(EAA 2025-06-28 발효) 맥락 보완 (직접 fetch 제한으로 W3C 재확인 불가)
- **Tailwind v4 CSS-first `@theme`**: JS 설정 파일 폐기, CSS 내부에서 `@theme` 지시문으로 토큰 선언 → `:root` custom property 자동 노출. Framer Motion 등 외부 라이브러리에서도 `resolveConfig()` 없이 직접 사용 가능 — 출처: [tailwindcss.com/blog/tailwindcss-v4-alpha](https://tailwindcss.com/blog/tailwindcss-v4-alpha) (자가학습 2026-06-25 기록 보강)

## 출처

- [Tailwind CSS v4 Alpha — Official Blog](https://tailwindcss.com/blog/tailwindcss-v4-alpha)
- [Tailwind CSS v4.0 Release](https://tailwindcss.com/blog/tailwindcss-v4)
- 위키 내부: `wcag-3-0-로드맵.md`, `wcag-2-2-새-성공-기준-요약.md`, `2026-06-25-rina-intent.md`

## 위키화 후보

- `wcag-2-2-4-1-1-parsing-폐기` — SC 4.1.1이 HTML 한정 "Always Satisfied"로 실무 감사 제외되는 경위 정리 (기존 `wcag-2-2-새-성공-기준-요약.md` 보완 노트)

## 프로필 반영 후보 (저위험)

- `[2026-06-28] WCAG 2.2 SC 4.1.1 Parsing = HTML 콘텐츠에서 사실상 폐기("Always Satisfied") — 접근성 감사 체크리스트에서 제외`

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

_(없음 — 기존 research-agent + memory-agent 조합으로 충분)_
