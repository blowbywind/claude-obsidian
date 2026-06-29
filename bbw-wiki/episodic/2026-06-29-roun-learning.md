---
date: 2026-06-29
bot: roun
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 로운 자가학습 — 2026-06-29

위키 대조 결과를 반영하여 교차검증합니다.

---

**검증 요약**
| 항목 | 판정 | 사유 |
|------|------|------|
| MERGE RETURNING + merge_action() | **중복 제외** | 위키 `postgresql.md` + 프로필 [2026-06-24] 이미 존재 |
| MERGE 카디널리티 위반 | **신규 ✓** | 공식 PG 문서(https://postgresql.org/docs/17/sql-merge.html) 직접 확인 |
| PostgreSQL 17 병렬 COPY | **삭제** | 출처가 Vertex AI redirect URL만 — 직접 확인 불가 |
| PG17 SQL/JSON 표준함수 | **신규 ✓** | PG17 실제 피처(ISO SQL:2023), 위키에 JSON_TABLE만 있고 JSON_VALUE/EXISTS/QUERY 미기재 |
| Soft delete → archive table | **보류** | Vertex AI redirect만 — 출처 없음. 개념은 알려져 있으나 이번 리서치 근거 없음 |
| OAuth PKCE + Implicit Grant 제거 | **중복 제외** | 위키 `oauth-2-1-리프레시-토큰-보안-rfc-9700.md` + 프로필 [2026-06-18] 이미 존재 |
| BOLA/IDOR 소유권 검증 | **중복 제외** | 프로필 [2026-06-20] 이미 존재 |
| AI-First 파이프라인 관리 | **삭제** | Vertex AI redirect만, 구체 출처 없는 범용 주장 |
| Infrastructure-from-Code Encore | **삭제** | 마케팅성 주장, 기술 출처 없음 |

---

## 오늘 배운 것
- **PG17 `MERGE` 카디널리티 위반 방지**: `ON` 조인 소스 측에 중복 행이 있으면 `ERROR: MERGE command cannot affect row a second time` 발생 → 병합 전 CTE 또는 `DISTINCT ON`으로 소스 고유화 필수. Upsert 설계 체크리스트에 추가.
- **PG17 ISO SQL:2023 JSON 함수 (`JSON_VALUE` / `JSON_EXISTS` / `JSON_QUERY`)**: 기존 `jsonb_to_text`, `jsonb_path_exists` 대신 표준 SQL 함수로 교체 가능. `JSON_TABLE`(위키 기재)과 별개로 스칼라·술어·경로 추출 각각 분리 제공 → JSONB 컬럼 쿼리 가독성·이식성 향상.

## 출처
- [PostgreSQL 17 MERGE 공식 문서](https://www.postgresql.org/docs/17/sql-merge.html)
- [PostgreSQL 17 JSON 함수 문서](https://www.postgresql.org/docs/17/functions-json.html)

## 위키화 후보
- `postgresql-merge-safe-patterns` — 카디널리티 위반 방지 CTE 패턴 단독 노트 (기존 `postgresql.md` 분리)

## 프로필 반영 후보 (저위험)
- `PG17 MERGE` 기존 [2026-06-24] 항목에 보완 문장 추가: "소스 중복 시 카디널리티 위반 → CTE/DISTINCT ON 전처리 필수"
- `PG17 JSON_VALUE / JSON_EXISTS / JSON_QUERY` — ISO SQL:2023 표준 함수, JSONB 쿼리 표준화 시 활용

## 승인 필요 (고위험)
- (없음)

## 신규 도구 후보 (에이전트/스킬)
- (없음)
