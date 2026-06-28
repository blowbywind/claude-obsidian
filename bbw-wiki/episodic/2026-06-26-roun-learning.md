---
date: 2026-06-26
bot: roun
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 로운 자가학습 — 2026-06-26

위키 중복 없음 확인. 기존 메모리 인사이트와 교차 대조 후 신규 항목만 추출한다.

**검증 결과 요약:**
- 항목 1·2 (Node.js 24 타입 소거 제약): 2026-06-21·06-24 메모리 기존 수록 — CI `tsc --noEmit` 명시 부분만 신규
- 항목 3·4 (Prisma 7): 06-20 메모리에 엔진 제거 수록. v7.3.0 원시 쿼리 최적화 세부사항은 신규
- 항목 5·6 (PG17): 06-24 메모리 기존 수록. `merge_action()` 함수 명시 세부는 신규
- 항목 7 (RFC 9700 토큰 패밀리): 06-18 메모리는 "비밀번호 리셋·MFA 변경 시 revoke"만 — 재사용 감지→패밀리 전체 만료는 신규
- 항목 8 (dev.to 계층 아키텍처): 출처 권위 부족(커뮤니티 블로그), 특정 기술 주장 아님 → 폐기

---

## 오늘 배운 것

- **Prisma v7.3.0+ 원시 쿼리 컴파일러 우회**: `$executeRaw` / `$queryRaw` 실행 시 쿼리 컴파일러 단계를 건너뛰고 드라이버 어댑터를 직접 통과 → 대량 원시 쿼리 워크로드에서 오버헤드 대폭 감소. v7.3.0 미만이면 혜택 없음, 버전 핀 확인 필요.
- **RFC 9700 Refresh Token 재사용 감지 → 패밀리 전체 revoke**: 이미 소비된 refresh token이 재사용되면 토큰 탈취 신호 → 해당 lineage(패밀리) 전체를 즉시 만료시켜야 함. 기존 인사이트(비밀번호 리셋·MFA 변경 시 전체 revoke)와 별개의 탈취 방어 메커니즘.
- **Node.js 24 타입 소거 → CI `tsc --noEmit` 필수**: 런타임은 타입을 소거만 하고 검사 안 함 → 정적 타입 안전성은 CI 단계에서 `tsc --noEmit`으로 별도 보장해야 함. (기존 06-21·06-24 인사이트 운영 보완)
- **PG17 `MERGE RETURNING` + `merge_action()`**: `MERGE ... RETURNING merge_action()` 으로 단일 원자적 작업에서 실제 수행된 동작 종류(`INSERT`/`UPDATE`/`DELETE`)를 즉시 식별 가능 — 멱등성 처리·감사 로그 기록에 활용 가능.

## 출처

- [Node.js 24 TypeScript Docs](https://nodejs.org/docs/latest/api/typescript.html)
- [Prisma 7 What's New](https://www.prisma.io/docs/orm/overview/whats-new-in-prisma-7)
- [RFC 9700 — OAuth 2.1 Security Best Current Practice](https://datatracker.ietf.org/doc/html/rfc9700)
- [PostgreSQL 17 Release Notes](https://www.postgresql.org/docs/17/release-17.html)

## 위키화 후보

- `Refresh Token Rotation & Family Revocation` — RFC 9700 기반 토큰 탈취 감지·패밀리 revoke 전략 노트 (기존 JWT/OAuth 노트와 연결)

## 프로필 반영 후보 (저위험)

- `Prisma v7.3.0+ $executeRaw 컴파일러 우회` — 원시 쿼리 성능 최적화 기법으로 DB 쿼리 최적화 역할에 직결
- `merge_action() in PG17 MERGE RETURNING` — 멱등성 API 설계·감사로그 구현 시 활용 가능한 DB 기법

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보 (에이전트/스킬)

(없음)
