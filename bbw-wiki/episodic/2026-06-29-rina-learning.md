---
date: 2026-06-29
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-29

교차검증 완료. 결과 종합합니다.

---

**검증 요약 (항목별 판정):**

| 항목 | 판정 | 사유 |
|---|---|---|
| CSS Anchor Positioning 베이스라인 | **중복** | 위키 `css-anchor-positioning-패턴.md` + 프로필 2026-06-20 기존 |
| shadcn 스트리밍 채팅 컴포넌트 | **폐기** | ui.shadcn.com 접근 불가, 출처 URL 미특정 |
| shadcn/cli v4 `shadcn/skills` | **부분 신규** | 기존 위키(cli-v4) Medium 출처 교차 확인. Presets/dry-run만 기록, AI 에이전트 측면 미포함 |
| `shadcn apply` 명령어 | **중복** | 위키 `shadcn-ui-luma-vs-rhea-스타일-비교.md` 기존 |
| shadcn RTL 자동 변환 | **폐기** | 출처 URL 미특정, 검증 불가 |
| Tailwind v4.2 Webpack 플러그인 | **폐기** | Tailwind 공식 문서(현재 v4.3)에서 `@tailwindcss/webpack` 미확인, `/blog/tailwindcss-v4-2` 404 |
| DOJ ADA Title II 마감일 | **폐기** | 연장 날짜(2027/2028) 기존 공지 일정(2026/2027)과 불일치, 검증 불가 |
| WCAG 3.0 신규 초안 | **부분 신규** | 위키에 타임라인만 있고 Gold/Silver/Bronze 점수제 미기록 |
| Intent-Based Design / Liquid Glass | **중복** | 위키 `2026-06-25-rina-intent.md`, `liquid-glass.md` 기존 |

---

## 오늘 배운 것
- `shadcn/ui CLI v4`(2026-03)의 `shadcn/skills` 기능: AI 코딩 에이전트가 컴포넌트 레지스트리·Radix/Base UI 프리미티브 컨텍스트를 직접 학습하도록 스킬 파일을 주입하는 기능. 기존 위키는 `--dry-run`/`--diff`·Presets만 기록했고 이 측면은 미포함 — 컴포넌트 커스텀 정확도에 직접 영향.
- WCAG 3.0 Working Draft는 기존 합격/불합격 2단 대신 **Bronze → Silver → Gold** 3단 점수제 채택 예정. 실무 기준은 여전히 WCAG 2.2 Level AA이며 최종 권고안 발효는 2028년 이후.
- 이번 리서치 5회 분량 중 검증 통과 항목은 위 2개. 나머지 7항목은 출처 미특정·문서 404·기존 위키 중복으로 폐기. (Tailwind webpack 플러그인 주장은 공식 문서와 직접 모순됨 — 주의.)

## 출처
- [shadcn/ui CLI v4 + AI Agent Skills + Presets — Medium(nakranirakesh)](https://medium.com/@nakranirakesh/shadcn-ui-march-2026-update-cli-v4-ai-agent-skills-and-design-system-presets-d30cf200b0e9)
- [WCAG 3.0 Working Draft — W3C](https://www.w3.org/TR/wcag-3.0/)

## 위키화 후보
- `shadcn-cli-v4-워크플로.md` 업데이트 — 기존 노트에 `shadcn/skills` AI 에이전트 컨텍스트 주입 항목 보완 (신규 노트 불필요, 기존 노트 갱신)

## 프로필 반영 후보 (저위험)
- `shadcn/ui 컴포넌트 작업 시 shadcn/skills 파일 주입으로 AI 에이전트 컨텍스트 정확도 향상 가능`

## 승인 필요 (고위험)
(없음)

## 신규 도구 후보 (에이전트/스킬)
(없음)
