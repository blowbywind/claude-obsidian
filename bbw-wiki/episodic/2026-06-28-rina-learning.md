---
date: 2026-06-28
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-28

WebSearch 권한이 없어 교차검증은 훈련 지식 + 기존 메모리 기반으로 수행한다. 출처 URL만 있고 특정 버전·기능명이 실재 확인 불가한 항목은 전부 버린다.

---

**[교차검증 판정 내역]**

| 항목 | 판정 | 이유 |
|---|---|---|
| DOJ ADA Title II WCAG 2.1 AA 시행 | ✅ 유지 | 실제 연방규칙(2024년 4월 확정, 대형기관 2년 유예) |
| 자동화 도구 20~40% 감지 한계 | ✅ 유지 | 업계 통용 통계(WebAIM 등 다수 출처 일치) |
| Intent-driven / Agentic UX 트렌드 | ✅ 유지 | uxdesign.cc 실 출판물, 업계 방향 일치 |
| 멀티모달·공간 인터페이스 확산 | ✅ 유지 (경계) | 트렌드 실제, 단 designdb.com 원문 특정 불가 |
| W3C Design Tokens **v2025.10** | ❌ 폐기 | 특정 버전 번호 실재 불명 — WebSearch 불가로 확인 무 |
| Tailwind CSS **v4.3.1** 스크롤바 코어 통합 | ❌ 폐기 | 버전·기능 조합 검증 불가; `scrollbar-thin` CSS 표준은 실재하나 이 버전에 코어 통합됐는지 확인 불가 |
| shadcn/cli v4 **shadcn/skills** | ❌ 폐기 | 실재 불명, 환각 강의심 |
| shadcn **apply** 테마 변환 | ❌ 폐기 | 실재 불명 |
| shadcn RTL 논리 CSS 자동 변환 | ❌ 폐기 | CLI 자동 변환 기능 실재 불명 |
| shadcn 채팅 컴포넌트 세트 (MessageScroller·Bubble·Attachment) | ❌ 폐기 | shadcn/ui 공식 미확인, 환각 강의심 |

---

## 오늘 배운 것

- **DOJ ADA Title II 시행**: 미국 공공기관(주·지방정부) 대상 WCAG 2.1 Level AA 준수 의무 기한이 2026년 4월 시행됐다(인구 5만 이상 또는 특수지구). 기존 메모리의 "WCAG 2.2 AA가 현행 기준"과 모순 없음 — 2.2는 2.1의 상위 호환이므로 2.2 AA를 맞추면 법적 요건 충족.
- **자동화 접근성 도구 한계**: 자동 진단 도구가 잡아내는 결함은 전체의 20~40%에 불과하다. 키보드 포커스 흐름·스크린리더 작동·색상 대비 시각 검증 등 수동 테스트를 파이프라인에 반드시 포함해야 한다.
- **Agentic UX 패턴**: UI가 사전 고정 레이아웃 대신 맥락·의도를 읽어 실시간으로 구성을 바꾸는 방향으로 빠르게 전환 중. AI 에이전트와의 상호작용 흐름(대화→행동→결과 표시)을 별도 UX 시나리오로 설계해야 한다.
- **멀티모달 입력 설계 필요성 증대**: 터치·음성·제스처 조합 인터랙션이 주류화됨에 따라, 단일 입력 가정(마우스·터치 one-size-fits-all) 설계는 점점 불완전해진다. 인터랙티브 타깃 크기(WCAG 2.2 SC 2.5.8, 24×24px AA) 기준과 함께 고려 필요.

## 출처

- [BBK Law — DOJ ADA Title II Final Rule](https://bbklaw.com)
- [Juicebox Interactive — Automated vs. Manual Accessibility Testing](https://juiceboxinteractive.com)
- [UX Collective — Agentic & Intent-driven UI Trends 2026](https://uxdesign.cc)

## 위키화 후보

- `Agentic UX` — 의도 기반 동적 인터페이스·AI 에이전트 상호작용 UX 설계 패턴 정리 노트

## 프로필 반영 후보 (저위험)

- **수동 접근성 테스트 체크리스트 항목화** — 자동화 도구 단독 사용 금지 원칙을 인사이트로 추가 (`키보드 포커스·스크린리더 병행 검증 필수`)

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

_(없음)_
