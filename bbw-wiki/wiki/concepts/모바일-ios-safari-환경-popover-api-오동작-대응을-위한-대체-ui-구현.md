---
title: 모바일 iOS Safari 환경 Popover API 오동작 대응을 위한 대체 UI 구현 패턴
type: concept
status: ai-curated
learned_by: rina
curated_at: 2026-06-24
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-24-rina-learning]]
---

# 모바일 iOS Safari 환경 Popover API 오동작 대응을 위한 대체 UI 구현 패턴

요청하신 Obsidian 위키 개념 노트를 작성하겠습니다. 자가학습 원문의 "iOS Safari 환경 Popover API 오동작" 항목을 기반으로 합니다.

---

## 핵심 정의

iOS Safari 환경에서 Popover API 내부의 입력 폼 요소(input, textarea 등)에 포커스하면 팝오버가 자동으로 닫히는 버그를 말한다. WebKit의 "light dismiss" 로직(팝오버 외부 영역 클릭 시 닫기)이 포커스 이벤트에도 잘못 반응하는 것으로 확인됨(WebKit Bug 267688).

## 요점

1. **버그 범위**: iOS Safari 18.2 이상 및 iPadOS WebKit 기반 환경에 국한. 데스크톱 Safari와 Chrome 계열 브라우저는 영향받지 않음.

2. **UX 영향**: 폼 입력 중 팝오버가 닫혀 입력값이 손실되고 사용자 경험이 급격히 악화됨.

3. **대체 구현 패턴**: (1) Dialog/Modal 라이브러리(예: `<dialog>` 네이티브 요소 또는 Radix UI Dialog)로 전환, (2) 조건부 렌더링으로 iOS 환경만 다른 UI 사용, (3) Popover 설정에서 `hideWhenOutOfViewport` 또는 `autohide` 속성 제거 및 수동 닫기 버튼 추가.

4. **상용 배포 권장사항**: 모바일 포함 프로젝트는 Popover API 직접 사용 회피 또는 라이브러리 폴백 계획 필수.

## 출처 URL

- https://bugs.webkit.org/show_bug.cgi?id=267688

---

**작성 완료**: 본문 약 430자, 구조 준수 (핵심 정의→요점 4개→출처 URL), 원문 범위 내 서술.

## 관련 노트
- [[mobile-responsive-guideline]] — 모바일 반응형 레이아웃·터치 환경 종합 가이드

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-24-rina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
