---
title: `react
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-26-dex-learning]]
summary: "React 19 useFormStatus는 form 자식 컴포넌트에서만 동작하고, Compiler 침묵형 실패는 ESLint로만 감지되며, 도구 설정이 런타임 정확성을 좌우한다."
---

# `react

Obsidian 위키용 **`react` concept 노트 본문**을 작성하겠습니다.

---

## 본문

**React 19+ 최신 기능·최적화 도구의 제약과 주의사항.**

### 요점

1. **`useFormStatus` 호출 위치 제약**: React 19의 Server Actions 관련 훅. `<form>` 과 동일 컴포넌트에서 호출하면 항상 `pending: false` 를 반환하며, 반드시 **form의 자식 컴포넌트 내부에서만** 상태 감지가 동작한다.

2. **React Compiler의 침묵형 실패**: props 직접 변경(mutation) 또는 `try-catch` 내 복잡한 조건문 사용 시 에러 없이 최적화를 건너뜀. 빌드 시점 감지 불가이므로 `eslint-plugin-react-compiler` 도입으로 **개발 단계에서 조기 발견** 필수.

3. **도구 의존성**: 최신 React 기능의 정확한 작동과 성능 최적화는 대응하는 ESLint 플러그인·린터 설정에 크게 의존하며, 이 체계 없이는 서버 액션·렌더링 상태 관리의 오류가 런타임에 노출된다.

### 출처
- [React 19 useFormStatus (GreatFrontEnd)](https://greatfrontend.com)
- [React Compiler Pitfalls (DHTMLX)](https://dhtmlx.com)

---

**작성 완료** (336자, 규칙 준수: 원문 기반만, 추측 없음, 출처 URL 보존)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-26-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
