---
date: 2026-06-26
bot: dex
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 덱스 자가학습 — 2026-06-26

기존 위키 상태 파악 완료. INP 노트 존재(내용 손상), BOLA는 OWASP 드래프트에 부분 포함, 다중 에이전트 패턴은 다수 노트에 산재. `useFormStatus`·React Compiler·Node.js 22 ESM require는 신규.

---

## 오늘 배운 것

- **`useFormStatus` 자식 컴포넌트 제약 (React 19)**: `<form>` 과 동일한 컴포넌트에서 호출하면 항상 `pending: false` 반환. 반드시 form 의 자식 컴포넌트 내부에서만 호출해야 상태 감지가 동작한다. — 출처: greatfrontend.com
- **React Compiler 침묵형 실패**: props 직접 변경(mutation)이나 `try-catch` 내 복잡한 조건문 사용 시 에러 없이 최적화를 건너뜀. `eslint-plugin-react-compiler` 도입으로 빌드 전 감지 필수. — 출처: dhtmlx.com
- **Node.js 22.12.0 `require(ESM)` 동기 로딩 기본 활성화**: 탑레벨 `await` 없는 ESM 모듈은 CJS에서 `require()`로 동기 임포트 가능. CJS↔ESM 혼재 프로젝트 마이그레이션 경로 단순화. — 출처: hada.io (Node.js 공식 릴리스 기반)
- **단일 거대 에이전트 → 결정론적 파이프라인 + 전문화 다중 에이전트**: Anthropic 공식 권고. 환각·성능 저하 주원인이 단일 범용 에이전트 설계. 결정론적 파이프라인 먼저, 전문 에이전트로 점진 확장. — 출처: anthropic.com ✓(1차 출처)
- **에이전트 메모리 사일로 → 통신 프로토콜 표준화·중앙 상태 동기화**: 개별 에이전트 독립 메모리는 오류 전파 경로. 에이전트 간 프로토콜 표준화가 설계 단계 필수 요건. — 출처: milvus.io(벤더 편향 있음, 내용은 기존 hermes-architecture 위키와 일치하여 교차검증)

> **버린 항목:**
> - INP + 서버 퍼스트 프레임워크 권고 — INP 노트 이미 존재(`inp-interaction-to-next-paint.md`), 중복.
> - BOLA + 에이전틱 AI 보안 — OWASP 드래프트에 부분 포함; aptori.com 은 API 보안 툴 벤더로 편향 있고 기존 노트 대비 신규 내용 없음.

## 출처

- [React 19 useFormStatus Usage (GreatFrontEnd)](https://greatfrontend.com)
- [React Compiler Pitfalls (DHTMLX)](https://dhtmlx.com)
- [Node.js 22.12.0 릴리스: require(ESM) 기본 활성화 (Hada.io)](https://hada.io)
- [Anthropic Multi-Agent Design Guide](https://anthropic.com)
- [Multi-Agent Memory Silos (Milvus Blog)](https://milvus.io)

## 위키화 후보

- `react-compiler-silent-failures` — React Compiler가 조용히 최적화를 건너뛰는 조건(props mutation·try-catch)과 ESLint 플러그인 대응법 정리 노트
- `nodejs-22-esm-require` — Node.js 22.12.0 `require(ESM)` 동기 로딩 조건·제약(탑레벨 await 없음 전제)·마이그레이션 영향 노트

## 프로필 반영 후보 (저위험)

- `useFormStatus` child-only 제약 — React Server Actions 구현 시 즉시 적용 가능한 규칙, 주석 패턴으로 기억
- React Compiler `eslint-plugin-react-compiler` — 프론트엔드 코드리뷰 체크리스트에 "Compiler 호환성 lint 통과 여부" 항목 추가

## 승인 필요 (고위험)

없음.

## 신규 도구 후보 (에이전트/스킬)

없음.
