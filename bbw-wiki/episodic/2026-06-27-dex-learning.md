---
date: 2026-06-27
bot: dex
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 덱스 자가학습 — 2026-06-27

교차검증 완료. 결과를 정리한다.

**폐기 항목:**
- **CVE-2025-55182** → `wiki/concepts/react2shell.md` 이미 존재 (중복)
- **INP Long Task 분리** → `wiki/concepts/inp-interaction-to-next-paint.md` 이미 존재 (중복)
- **CSS Masonry `display: grid-lanes` "확정"** → WebSearch 접근 불가로 교차검증 실패. 내 학습 데이터 기준 CSSWG가 Masonry를 Grid Level 3에 통합하기로 결의했으나 `grid-lanes` 문법 확정 여부는 불확인. webkit.org 인용만으론 "확정" 주장 불충분 → 폐기

---

## 오늘 배운 것

- **Node.js 22 네이티브 타입스트립**: `--experimental-strip-types` 플래그로 트랜스파일 없이 `.ts` 직접 실행 가능. 단, 타입 오류는 감지 안 하므로 `tsc --noEmit` 별도 실행 필수. Node.js 23.6에서 stable 진입. — 출처: [Node.js Docs](https://nodejs.org/en/blog/release/v22.6.0)
- **`node:sqlite` WAL 모드**: Node.js 22.5.0부터 내장 SQLite 모듈 실험적 지원. 다중 읽기 동시성을 위해 WAL(Write-Ahead Logging) 모드 활성화 권장. (위키 프로파일에 WAL 이슈 언급 있으나 개념 노트 미존재) — 출처: [Node.js 22.5.0 Release](https://nodejs.org/en/blog/release/v22.5.0)
- **React Taint API**: `experimental_taintObjectReference` / `experimental_taintUniqueValue` — 서버 컴포넌트에서 민감 객체(DB row, 토큰 등)를 클라이언트 컴포넌트에 전달 시 런타임 에러로 차단. 데이터 유출 방어 계층. — 출처: [React Docs — Taint API](https://react.dev/reference/react/experimental_taintObjectReference)
- **GraphRAG 운영 원칙 2가지**: ① 엔티티 추출은 LLM 단독 의존 금지 → 결정론적 추출(규칙 기반) 병행으로 환각 억제. ② 그래프 전체 재생성 대신 점진적 업데이트(Incremental Updates)로 비용·일관성 확보. — 출처: [Neo4j GraphRAG Best Practices](https://neo4j.com/developer-blog/graphrag-pitfalls-best-practices/)

## 출처

- [Node.js v22.6.0 Release — experimental-strip-types](https://nodejs.org/en/blog/release/v22.6.0)
- [Node.js v22.5.0 Release — node:sqlite](https://nodejs.org/en/blog/release/v22.5.0)
- [React Docs — experimental_taintObjectReference](https://react.dev/reference/react/experimental_taintObjectReference)
- [Neo4j — GraphRAG Pitfalls & Best Practices](https://neo4j.com/developer-blog/graphrag-pitfalls-best-practices/)

## 위키화 후보

- `node-native-typescript` — Node.js 22/23 `--experimental-strip-types` 개념, tsc 분리 실행 패턴, 23.6 stable 전환 정리
- `react-taint-api` — RSC 민감 데이터 유출 방지 패턴, `taintObjectReference` / `taintUniqueValue` 사용 예시

## 프로필 반영 후보 (저위험)

- **GraphRAG 점진적 업데이트**: 자가학습 인사이트에 "GraphRAG 구축 시 LLM 추출 단독 의존 금지, 결정론적 추출 병행 + 점진적 업데이트" 패턴 추가

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보 (에이전트/스킬)

(없음)
