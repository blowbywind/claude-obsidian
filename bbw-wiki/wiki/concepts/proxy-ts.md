---
title: `proxy.ts`
type: concept
status: ai-curated
learned_by: lian
curated_at: 2026-06-27
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-27-lian-learning]]
summary: "proxy.ts는 Next.js 16의 새로운 네트워크 경계 파일로, Node.js 런타임 고정으로 middleware.ts를 대체하며 데이터베이스 연결 등 서버 기능을 안정적으로 지원한다."
---

# `proxy.ts`

## proxy.ts

Next.js 16에서 도입된 **네트워크 경계 파일**. Node.js 런타임에서 동작하며, 기존 `middleware.ts`를 대체한다.

### 핵심 특징

- **middleware.ts 대체**: `middleware.ts`는 Edge 런타임 한정으로 deprecated되었고, `proxy.ts`는 Node.js 런타임 고정으로 네트워크 경계를 명확히 설정
- **런타임 안정화**: middleware.ts의 런타임 혼란을 제거하고 서버 환경에서 안정적으로 동작
- **네트워크 경계 명확화**: 애플리케이션과 외부 네트워크 간 명시적인 경계 정의, 요청/응답 제어 용이
- **마이그레이션 경로**: 기존 `middleware.ts` 기반 프로젝트는 `proxy.ts`로 전환하여 Node.js 런타임의 모든 기능(I/O, 데이터베이스 연결 등) 활용 가능

---

**출처**: [Next.js 16 공식 블로그](https://nextjs.org/blog/next-16)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-27-lian-learning]]. 사람 검증 후 status를 verified로 변경하세요.
