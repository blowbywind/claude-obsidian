---
date: 2026-06-28
bot: roun
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 로운 자가학습 — 2026-06-28

## 오늘 배운 것

- **RFC 9700 Implicit·ROPC 공식 폐기** — 퍼블릭 클라이언트에 Implicit Grant·ROPC는 사용 금지; DPoP(Sender-Constrained Token) 또는 Refresh Token Rotation 필수 적용. 기존 `[2026-06-18]` revoke 규칙에 플로우 레벨 제약 추가.
- **RFC 9700 Redirect URI 완전 일치 강제** — 인가 서버는 와일드카드 패턴을 허용하면 오픈 리다이렉터 취약점 발생; 사전 등록값과 **정확히 일치** 검증만 허용. 인가 서버 구현 체크리스트 필수 항목.
- **PostgreSQL 17 `MERGE RETURNING` + `merge_action()`** — `MERGE` 단일 트랜잭션 내에서 `merge_action()` 반환값으로 INSERT/UPDATE/DELETE 구분 → 변경 감사 파이프라인을 추가 쿼리 없이 구축 가능. (기존 `[2026-06-24]` 메모의 세부 구현 보완)
- **PostgreSQL 17 `JSON_TABLE COLUMNS` 타입 명시** — `jsonb_array_elements` + 중첩 JOIN 체인 대신 `COLUMNS` 절에서 타입 직접 지정 → 타입 캐스팅 오류 방지 + 쿼리 단순화. (기존 `[2026-06-24]` 메모 보완)
- **BullMQ v5 DAG 원자 생성** — `flowProducer.add()` **단일 호출**로 전체 의존성 트리 등록 필수(분할 호출 시 고아 잡 발생); 자식 실패가 부모로 즉시 전파되지 않으려면 `failParentOnFailure: false` 명시.
- **BullMQ v5 잡 간 데이터 최소화** — 잡 payload에는 DB ID·파일 경로 등 직렬화 가능 메타데이터만 전달; 자식 결과 전체는 부모 잡에서 `job.getChildrenValues()` 로 읽어야 Redis 과부하 방지. (기존 `[2026-06-21]` 메모 보완)

> **제외 항목**: Prisma 7 `compilerBuild = "fast"` — 공식 문서에 없는 옵션, 출처 불확실로 폐기.  
> **중복 항목**: Node.js 24 `--experimental-strip-types` enum/namespace 제약 → `[2026-06-24]` 기록 있음, 생략.

---

## 출처

- [RFC 9700 — OAuth 2.0 Security Best Current Practice](https://datatracker.ietf.org/doc/html/rfc9700)
- [PostgreSQL 17 Release Notes](https://www.postgresql.org/docs/17/release-17.html)
- [BullMQ v5 — FlowProducer](https://bullmq.io/guide/flows)
- [Prisma 7 — Driver Adapters & Query Compiler](https://www.prisma.io/docs/orm/prisma-client/setup-and-configuration/driver-adapters)

---

## 위키화 후보

- **RFC 9700 OAuth 보안 체크리스트** — Implicit·ROPC 금지, DPoP/Rotation, Redirect URI 완전일치 등 인가 서버·클라이언트 구현 체크리스트 노트

---

## 프로필 반영 후보 (저위험)

- `MERGE RETURNING + merge_action()` 감사 패턴 — DB 스키마 설계·변경 이력 구축 역할에 직결
- BullMQ `failParentOnFailure` + `getChildrenValues()` — 비동기 파이프라인 설계 세부 기법

---

## 승인 필요 (고위험)

(없음)

---

## 신규 도구 후보 (에이전트/스킬)

(없음)
