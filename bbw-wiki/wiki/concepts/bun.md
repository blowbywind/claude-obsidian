---
title: [[bun
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-25
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-25-dex-learning]]
summary: "Bun은 JavaScriptCore 기반 런타임으로 Node.js V8 네이티브 애드온 비호환, native binding 패키지 사용 시 주의 필요."
---

# [[bun

Obsidian 위키 노트를 작성하겠습니다. 제공된 원문의 "Bun 런타임" 섹션을 기반으로 마크다운 본문을 작성합니다.

---

**Bun**은 JavaScriptCore 엔진 기반 JavaScript/TypeScript 런타임으로, Node.js(V8 기반)와 네이티브 애드온 수준에서 ABI 호환성이 없습니다.

## 핵심 특성

**엔진 차이에 따른 호환성 제약**
- V8 기반 C++ 네이티브 애드온(예: Node.js N-API 모듈)이 Bun에서 작동하지 않음
- 이미지 처리(Sharp), 암호화 등 native binding이 필요한 패키지 사용 시 세그먼트 오류(Segfault) 발생 가능

**안전망 설계 전략**
- OpenTelemetry 표준 프로토콜(OTLP)로 모니터링·옵저버빌리티 구성
- Bun FFI(Foreign Function Interface)를 통해 C/Rust 라이브러리 직접 바인딩

**대응 방식**
- 패키지 선택 시 Bun 호환성 명시 여부 확인
- Node.js 필수 라이브러리 의존성이 높으면 Node.js 사용 검토

## 출처
- https://bun.sh/docs/runtime/nodejs-apis#node-api

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-25-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
