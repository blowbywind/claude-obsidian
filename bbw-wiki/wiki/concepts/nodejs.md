---
title: `nodejs
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-26-dex-learning]]
summary: "Node.js 22.12.0부터 탑레벨 await가 없는 ESM 모듈을 CommonJS에서 require()로 동기 로드 가능하며, 레거시 프로젝트의 점진적 ESM 마이그레이션을 용이하게 함."
---

# `nodejs

자가학습 원문을 Obsidian 위키 노트로 큐레이션하겠습니다.

**`nodejs` concept 노트 본문:**

---

Node.js는 Chrome V8 엔진 기반의 자바스크립트 런타임 환경입니다. 버전 22.12.0부터는 CommonJS(CJS) 환경에서 탑레벨 `await`가 없는 ECMAScript Module(ESM)을 동기적으로 `require()`로 로드할 수 있는 기능이 기본으로 활성화되었습니다.

**주요 특징**

1. **CJS↔ESM 동기 로딩**: 탑레벨 `await`가 포함되지 않은 ESM 모듈은 CommonJS의 `require()` 함수로 직접 동기 임포트 가능하며, 이전 버전에서 필요하던 비동기 처리 경로를 제거할 수 있습니다.

2. **혼재 프로젝트 마이그레이션 단순화**: CommonJS 레거시 프로젝트를 ESM으로 점진 전환할 때 모든 모듈을 동시에 변경하지 않아도 되므로, 단계적 마이그레이션이 실질적으로 가능해집니다.

3. **제약 조건**: 탑레벨 `await`를 사용하는 모듈은 여전히 ESM 형식이어야 하므로, 동기 로딩 대상 여부를 사전에 확인해야 합니다.

**출처**
- [Node.js 22.12.0 릴리스 공지 (Hada.io)](https://hada.io)
- Node.js 공식 릴리스 노트

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-26-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
