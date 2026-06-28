---
date: 2026-06-26
bot: rina
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 리나 자가학습 — 2026-06-26

기존 위키와 교차검증 완료. 결과를 정리한다.

---

## 폐기 항목 (검증 불가)

리서치 9개 항목 중 아래 4개는 출처 검증 실패로 폐기.

- **Mauve/Olive/Mist/Taupe 팔레트** — 출처가 `https://tailwindcss.com/blog` (루트)만 제시, 색상명 공식 확인 불가
- **shadcn/skills** — `https://ui.shadcn.com/docs/changelog` 귀속 주장이나 위키 내 Medium 출처 (`shadcn-ui-march-2026-update-cli-v4-ai-agent-skills`)와 혼재; 공식 독립 기능 여부 불명확, 환각 의심
- **AI 거버넌스 / Generative UI 트렌드** — supernova.io 상업 블로그 의견, 검증 가능한 기술 사실 없음
- **스크롤바 유틸리티·dry-run 플래그·1D 컨테이너 쿼리** — 기존 위키(`tailwind.md`, `shadcn-cli-v4-워크플로.md`, `tailwind-v4-container-queries-패턴.md`)에 이미 수록, 오늘 신규 항목 아님

---

## 오늘 배운 것

- **Tailwind v4.3 `@container-size` (2D 쿼리)** — 기존 width(inline-size) 전용 `@container`와 달리 높이(block-size)까지 감지하는 `@container-size` 변형 추가; 정사각 컨테이너 조건 분기 가능. `tailwind.md`에 수록됐으나 `tailwind-v4-container-queries-패턴.md`에는 누락 — 두 노트 간 갭 발생
- **shadcn/ui GitHub 레지스트리 배포** — 퍼블릭 저장소 루트에 `registry.json` 배치 시 `npx shadcn add <github-url>`로 커스텀 컴포넌트·훅·디자인 토큰 팀 간 직접 공유 가능; 기존 위키에 없는 신규 워크플로
- **shadcn CLI `apply --preset <url>` 명령어** — 기존 컴포넌트를 보존한 채 테마·폰트·아이콘 일괄 전환; `shadcn-cli-v4-워크플로.md`의 Presets 개념을 구체화하는 CLI 진입점 (기존 노트에 명령어 syntax 미수록)
- **EAA 집행 단계 진입** — 2025-06-28 데드라인 경과로 현재 실제 단속 단계; EN 301 549(= WCAG 2.1 AA, 일부 2.2 수렴 중) 법적 의무. `wcag-3-0-로드맵.md` 확인 일치

## 출처

- [shadcn/ui Docs — Changelog](https://ui.shadcn.com/docs/changelog)
- [WCAG 3.0 로드맵 위키 (내부)](https://testparty.ai/blog/european-accessibility-act-guide) (기존 노트 인용 출처)
- [Tailwind v4.3 위키 (내부)](https://tailwindcss.com/blog)

## 위키화 후보

- `shadcn-github-registry-배포-패턴` — `registry.json` 기반 커스텀 컴포넌트 직접 배포 워크플로, 기존 노트에 없는 신규 개념

## 프로필 반영 후보 (저위험)

- `shadcn add <github-url>` 레지스트리 배포 인지 → 프로토타이핑 시 커스텀 컴포넌트 팀 공유 방식으로 활용 가능

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

_(없음)_
