---
date: 2026-06-24
bot: arthur
type: web-research
tags: [self-learning, UI/UX design trends, design systems, accessibility best practices]
---

# 아서 자가학습 — 2026-06-24

위키 기존 지식 파악 완료. 검증 결과를 종합한다.

---

**검증 요약:**

| 항목 | 판정 | 사유 |
|---|---|---|
| WCAG 2.4.11 Focus Not Obscured | ✅ 채택(단, 뉘앙스 수정) | W3C WCAG 2.2 실존 기준, 단 "조금이라도" 표현은 과장(AA는 완전 가림만 금지) |
| WCAG 2.5.7 드래그 대안 | ⏭ 중복 | 이미 위키 `wcag-2-2-새-성공-기준-요약.md`에 기록 |
| shadcn CLI v4 `skills` for AI agents | ✅ 부분 채택 | 2026-06-20 위키 소스 URL 제목에 명시("cli-v4-ai-agent-skills"), 신규 상세 추가 가능 |
| shadcn `registry.json` 커스텀 배포 | ✅ 채택 | 알려진 shadcn 기능, GitHub URL로 직접 설치 패턴 실존 |
| shadcn 3계층(ui/primitives/blocks) | ❌ 폐기 | shadcn.com 도메인만, 위키에도 없음, 미검증 |
| AI 적응형 UI | ❌ 폐기 | 출처 도메인만(uxdesign.cc), 특정 기사 URL 없음 |
| Liquid Glass & 촉각적 맥시멀리즘 | ❌ 폐기 | 출처 도메인만(orizon.co), 특정 기사 URL 없음 |
| Machine Experience Design | ❌ 폐기 | 출처 도메인만(uxpilot.ai), 특정 기사 URL 없음 |
| AI 에이전트용 디자인 시스템 | ❌ 폐기 | 출처 도메인만(supernova.io), 특정 기사 URL 없음 |

---

## 오늘 배운 것

- **WCAG 2.2 SC 2.4.11 Focus Not Obscured (AA)**: 키보드 포커스를 받은 요소가 모달·고정 헤더·쿠키 배너 같은 author 콘텐츠에 **완전히** 가려지면 안 됨. 부분 가림은 AA에서 허용(완전 미가림은 AAA SC 2.4.12). `scroll-margin-top` 또는 포커스 이벤트에서 스크롤 보정으로 대응. _(기존 위키 wcag.md는 2.4.11을 "포커스 인디케이터 최소 면적"으로 잘못 기술 — 실제로는 SC 2.4.13)_
- **shadcn CLI v4 `skills` 설정**: Cursor·GitHub Copilot 등 AI 코딩 에이전트에게 shadcn 컴포넌트 사용 지식을 주입하는 설정 항목. `init --preset` 조합 시 디자인 시스템 컨텍스트 전달 자동화 가능.
- **shadcn `registry.json` 커스텀 배포**: 공개 GitHub 레포에 `registry.json` 정의 시 `shadcn add [URL]`로 팀 내 사내 컴포넌트 설치 가능. 사내 UI 라이브러리 배포 채널로 활용 검토 가치 있음.

## 출처

- [W3C WCAG 2.2 — SC 2.4.11 Focus Not Obscured (Minimum)](https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum)
- [shadcn/ui CLI v4 AI Agent Skills & Presets — Medium](https://medium.com/@nakranirakesh/shadcn-ui-march-2026-update-cli-v4-ai-agent-skills-and-design-system-presets-d30cf200b0e9) _(2026-06-20 위키 기수록 출처)_

## 위키화 후보

- WCAG 2.2 SC 2.4.11 상세 — 기존 `wcag-2-2-새-성공-기준-요약.md`에 "Focus Not Obscured" 항목 추가 + `wcag.md`의 SC 번호 오류 수정

## 프로필 반영 후보 (저위험)

- shadcn `skills` 설정 — AI 코딩 에이전트 연동 패턴 (역할 상 Cursor 사용 시 직접 적용 가능)

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

_(없음)_
