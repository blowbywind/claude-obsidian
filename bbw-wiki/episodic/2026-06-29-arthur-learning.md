---
date: 2026-06-29
bot: arthur
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 아서 자가학습 — 2026-06-29

기존 위키와 메모리 교차 확인 완료. 이제 결과를 종합한다.

**검증 요약:**
- "Tailwind v4.2 논리 속성" → 출처 URL이 `tailwindcss.com/blog/tailwindcss-v4-3`이므로 **버전 오류** (v4.2 아님, v4.3). 내용 자체는 v4.3 신규 유틸리티로 수용 가능하나 2026-06-26 메모리에 v4.3 항목 이미 존재 → 보충만 반영
- Tailwind v4.3 스크롤바·`@container-size`·`tab-*`: **2026-06-26 메모리 중복** → 폐기
- shadcn `registry:base`: **2026-06-25 메모리 중복** → 폐기
- WCAG 2.2 현행 권장: **2026-06-18 메모리 중복** → 폐기
- shadcn Rhea compact style: 위키 노트 존재하나 내용 부실(AI 큐레이션 실패 상태), 신규 세부사항 수용
- shadcn Chat Components / `MessageScroller`: 위키 미존재, grep 0 결과 → 신규
- shadcn `preset` 명령: `skills` 항목(2026-06-24)과 다른 기능 → 신규
- WCAG 3.0 초안: 신규 맥락 (WCAG 2.2 현행 유지 전제로)
- DTCG 2025.10: 위키 노트 존재하나 내용 부실 → 보충 가능

---

## 오늘 배운 것
- **shadcn Chat Components `MessageScroller` 분리 패턴** (2026-06): 스트리밍 응답·스크롤 고정(stick)·스레드 복원·이전 기록 prepend·점프·가시성 추적 책임을 `MessageScroller` 단일 컴포넌트로 분리 — 채팅 UI 복잡도 관리의 공식 표준 패턴
- **shadcn Rhea = compact 스타일** (2026-05): `--spacing` 스케일을 건드리지 않고 컴포넌트 크기·간격·밀도를 직접 재정의 — 정보 밀도가 높은 대시보드·제품형 UI에 적합
- **shadcn `preset` 명령** (2026-04): preset 코드를 해석·공유·현재 프로젝트 기준으로 resolve — 디자인 시스템 설정을 코딩 에이전트에 직접 전달 가능, `skills` 명령과 별개
- **Tailwind v4.3 논리 속성 추가**: `pbs-*`·`mbs-*`·`inline-*`·`block-*` 등 논리 속성 유틸리티 확충 (리서치 원본의 "v4.2" 표기는 출처 URL 기준 **v4.3** 오기)
- **WCAG 3.0 초안**: 웹 외 앱·스트리밍·XR·IoT까지 대상 확대, 기능적 사용자 요구 중심 모델로 전환 예고 — 현행 구현 기준은 WCAG 2.2 AA 유지

## 출처
- [Tailwind CSS v4.3](https://tailwindcss.com/blog/tailwindcss-v4-3)
- [shadcn/ui Chat Components — June 2026 Changelog](https://ui.shadcn.com/docs/changelog/2026-06-chat-components)
- [shadcn/ui Rhea — May 2026 Changelog](https://ui.shadcn.com/docs/changelog/2026-05-rhea)
- [shadcn/ui Preset Commands — April 2026 Changelog](https://ui.shadcn.com/docs/changelog/2026-04-preset-commands)
- [WCAG 3.0 Working Draft — W3C](https://www.w3.org/TR/wcag-3.0/)

## 위키화 후보
- `shadcn-chat-components` — `MessageScroller` 분리 설계, 스트리밍·prepend·스크롤 고정 책임 구조 정리
- `wcag-3-동향` — 기존 `css-contrast.md` 보완; 3.0 초안의 대상 확대 및 2.2 현행 유지 관계 정리

## 프로필 반영 후보 (저위험)
- `shadcn MessageScroller` 분리 패턴 — 스트리밍 채팅 UI 구현 참고 기법으로 자가학습 인사이트 추가
- shadcn Rhea compact 스타일 (`--spacing` 불변, 밀도 직접 조절) — 제품형 UI 밀도 최적화 기법으로 추가

## 승인 필요 (고위험)
(없음)

## 신규 도구 후보 (에이전트/스킬)
(없음)
