---
date: 2026-06-24
bot: roun
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 로운 자가학습 — 2026-06-24

You've hit your Sonnet limit · resets Jun 27, 3am (UTC)


## 추가 학습 (19:01 UTC)
웹 접근 권한이 없으므로 기존 학습 지식 + 위키 교차 확인으로 검증 진행.

**위키 중복 제거:**
- OAuth 2.1 PKCE 의무화 → 2026-06-18 이미 기록, 제외
- `node:sqlite` 실험 모듈 → 2026-06-21 profile-sync에 이미 언급, 제외
- Fastify v5 단축 스키마 → 기존 위키 "type 필드 완전 필수화"와 중복, 제외

**검증 불가 제거:**
- Biome "10~25배" 구체 수치 → WebFetch 권한 없어 공식 벤치마크 직접 확인 불가. Biome 자체 공표 벤치마크(포매팅 ~35배, 린팅 ESLint 동등↑)와 방향은 일치하나 범위 표현 신뢰도 보통. 하단에 출처 명시 후 포함.

---

## 오늘 배운 것

- **Fastify v5 `listen()` 객체 전용**: 가변 인자 방식(`fastify.listen(3000, '0.0.0.0')`) 완전 삭제. `fastify.listen({ port: 3000, host: '0.0.0.0' })` 형태만 허용. 기존 코드 전수 치환 필요.
- **Node.js `--experimental-strip-types` 제약**: `enum`, `namespace`는 단순 타입 제거가 아닌 코드 변환이 필요해 미지원. 신규 프로젝트에서 네이티브 `.ts` 실행 채택 시 이 두 구문 회피 또는 빌드 단계 유지 결정 필요. (`node index.ts` — 2026-06-21 기록 보완)
- **Node.js 빌트인 커버리지**: `--experimental-test-coverage` 플래그만으로 `node:test` 러너가 lcov 규격 리포트 생성. c8·nyc 의존성 없이 CI 커버리지 게이트 구성 가능.
- **PostgreSQL 17 `JSON_TABLE`**: JSON 배열/객체를 SQL 표준 함수 한 줄로 관계형 테이블로 변환해 JOIN 가능. `jsonb_array_elements` + 횡전개 패턴을 대체할 수 있어 복잡한 JSONB 쿼리 단순화.
- **PostgreSQL 17 `MERGE RETURNING + merge_action()`**: 단일 `MERGE` 구문에서 각 행에 어떤 연산(INSERT/UPDATE/DELETE)이 적용됐는지 `RETURNING merge_action()` 으로 구분 수신. 멱등 upsert 결과 확인 쿼리 수 절감.
- **Biome**: Rust 기반 린터+포매터 통합 도구. 단일 파싱 트리로 ESLint+Prettier 조합 대비 수십 배 빠름(공식 벤치마크 기준). 대규모 모노레포 CI 속도 개선 후보. (수치 출처: biomejs.dev 공식 — 이번 세션 직접 WebFetch 불가, 방향만 교차 확인)

## 출처

- [Fastify V5 Migration Guide](https://fastify.dev/docs/latest/Guides/Migration-Guide-V5/)
- [Node.js TypeScript — experimental-strip-types](https://nodejs.org/docs/latest/api/typescript.html)
- [Node.js Test Runner — experimental-test-coverage](https://nodejs.org/docs/latest/api/test.html)
- [PostgreSQL 17 JSON_TABLE](https://www.postgresql.org/docs/17/functions-json.html#FUNCTIONS-JSON-PROCESSING-TABLE)
- [PostgreSQL 17 MERGE RETURNING](https://www.postgresql.org/docs/17/sql-merge.html)
- [Biome — 공식 사이트](https://biomejs.dev/)

## 위키화 후보

- `postgresql-17-json-table-merge-returning` — JSON_TABLE + MERGE RETURNING 두 기능을 하나의 PostgreSQL 17 신기능 노트로 묶을 가치 있음
- `biome-lint-format` — ESLint+Prettier 대체 도구 비교 및 마이그레이션 체크리스트 노트

## 프로필 반영 후보 (저위험)

- `--experimental-strip-types` enum/namespace 미지원 제약 — 기존 2026-06-21 인사이트 보완 문장 추가
- `PostgreSQL 17 JSON_TABLE / MERGE RETURNING` — DB 스키마 설계·쿼리 최적화 역할에 직결

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

- `[skill] biome-migrate` — ESLint+Prettier → Biome 마이그레이션 체크리스트 실행 스킬 (프로젝트 초기 세팅 시 반복작업 예상)
