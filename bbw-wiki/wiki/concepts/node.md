---
title: `node
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-27
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-27-dex-learning]]
---

# `node

원문의 자가학습 항목 중 **Node.js 관련 내용**으로 concept 노트를 작성하겠습니다.

---

**Node.js** — JavaScript를 서버·CLI·도구 환경에서 실행하는 런타임. V8 엔진과 libuv 라이브러리로 비동기 I/O와 이벤트 루프 기반 고성능·고동시성 처리를 제공하며, npm 에코시스템으로 생태계가 확장됨.

## 최근 변화

**1. 네이티브 타입스크립트 지원**  
Node.js 22부터 `--experimental-strip-types` 플래그로 TypeScript를 트랜스파일 단계 없이 `.ts` 파일 직접 실행 가능. 단, 타입 오류는 런타임 감지 불가하므로 `tsc --noEmit`으로 타입 검증은 별도 실행 필수. Node.js 23.6에서 안정화(stable) 진입 예정.

**2. 내장 SQLite 모듈 + WAL 모드**  
Node.js 22.5.0부터 `node:sqlite` 모듈을 실험적으로 제공. 데이터베이스 다중 읽기 동시성 확보를 위해 WAL(Write-Ahead Logging) 모드 활성화 권장. 외부 라이브러리 의존도를 낮춤.

## 출처
- [Node.js v22.6.0 Release — experimental-strip-types](https://nodejs.org/en/blog/release/v22.6.0)
- [Node.js v22.5.0 Release — node:sqlite](https://nodejs.org/en/blog/release/v22.5.0)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-27-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
