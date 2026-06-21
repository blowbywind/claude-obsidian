---
title: `fastify
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-roun-learning]]
---

# `fastify

Fastify 노트 본문을 작성하겠습니다.

---

**핵심 정의:**
Fastify는 Node.js용 경량 웹 프레임워크로, v5에서 응답 직렬화와 스키마 검증을 강화했습니다.

**요점 3개:**

1. **응답 스키마 필수화**: v5부터 response schema 미지정 시 `fast-json-stringify` 대신 `JSON.stringify()` 폴백으로, 직렬화 속도가 느리고 민감 필드 누출 위험이 증가합니다. 모든 라우트에 `response: { 200: { type: 'object', ... } }` 필수 지정이 권장됩니다.

2. **브레이킹 변경 4종**: ① `logger` → `loggerInstance` (커스텀 로거 주입), ② `reply.sent = true` → `reply.hijack()` (응답 가로채기), ③ `version`/`versioning` → `constraints` (라우트 버전 제약), ④ `request.connection` → `request.socket`

3. **스키마 필드 강화**: querystring, params, body 스키마에서 `type` 필드가 완전 필수화되어 불완전한 스키마 정의 방지.

## 참고
- [V5 Migration Guide | Fastify](https://fastify.dev/docs/latest/Guides/Migration-Guide-V5/)
- [Fastify v5 breaking changes: worth the upgrade? – Encore Blog](https://encore.dev/blog/fastify-v5)

---

**특징**: 원문의 자가학습 내용만 사용 / 정의는 제목과 v5 변경사항에서 추론 / 300~500자 범위 / 구체적 코드 예시는 출처 링크에 위임

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
