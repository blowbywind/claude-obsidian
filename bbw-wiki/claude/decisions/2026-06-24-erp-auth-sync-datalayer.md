---
date: 2026-06-24
project: hnedu_erp (+ hnedu_auth)
status: 구현·배포 완료 (.220/.221)
tags: [hnedu_erp, hnedu_auth, sync, service-token, ef-core, npgsql, security, adr]
---

# ERP↔auth 동기화 — 서비스 인증 + 데이터레이어 정책

날짜: 2026-06-24 / 프로젝트: hnedu_erp(+auth) / 상태: 구현·.220/.221 배포 완료
커밋: ERP `1a0b6da 0f4c14d a4210eb 84e6989 228111a` / auth `3a85665`(feat/mfa-totp)

## 배경
auth↔ERP 직원/부서 동기화를 운영 배선하던 중, 무인 동기화의 인증 수단이 없고
(15분 사용자 토큰만·MFA 게이트) ERP 쓰기경로 전반에 잠복 결함이 다수 드러났다.
DB가 비어 있어 단위테스트로는 안 잡히던 것들.

## 결정 1: ERP→auth 서비스 인증 = 불투명 서비스 토큰
채택: auth에 `service_tokens` 테이블(sha256 해시 저장) + `svc_` 불투명 토큰.
가드 `requireServiceOrAdmin` = svc_면 (선택 IP화이트리스트)+GET만 허용, 아니면 기존 requireAdmin.
- 대안 거부: 장기 JWT(취소 어려움), 사용자 토큰 재사용(15m·MFA로 무인 불가).
- 스코프: read 전용(employees/departments GET)만 → 유출 시 피해 최소화. 쓰기는 ALL.ADMIN 유지.
- 첫 발급은 부트스트랩 CLI(`scripts/issue-service-token.mjs`, MFA 우회). 원문은 1회만 노출.
- ERP 배선: `infra/.env` `AuthIntegration__BaseUrl`(도메인 변경예정·env로만)·`__ServiceToken`.

## 결정 2: PG enum 컬럼 전부 → text (Npgsql enum 미등록)
채택: 모든 사용자정의 enum 컬럼을 text로 전환(`023_all_enums_to_text.sql`, 제네릭 멱등),
AppDbContext는 `HasColumnType("*_enum")` 제거 + `ConfigureConventions Properties<Enum>().HaveConversion<string>()`(enum 이름 저장).
- 이유: Npgsql에 enum 미등록 → EF가 string/enum을 PG enum에 바인딩 못 해 INSERT마다 42804.
  거의 모든 쓰기기능 영향(잠복). ip_address inet→text 선례와 동종.
- 대안 거부: MapEnum+CLR enum 정식 등록(27종 신설 대공사).
- ⚠ 함정: HasColumnType만 떼고 HasConversion<string>까지 지우면 enum이 정수 ordinal로 저장됨
  (code-review가 배포 직전 적발). 전역 컨벤션이 누락 없는 정답.

## 결정 3: 시스템 액터 audit 처리 + jsonb 정규화
- 예약 동기화 잡(SystemActorId=Guid.Empty)은 audit_logs.actor_id FK가 없어 생략(AuditLogService).
- old_value/new_value(jsonb)에 평문 들어가면 22P02 → AuditLogService.AsJson로 정규화.

## 부수 발견·수정 (운영 쓰기경로 prod 버그, 통합테스트로 노출)
- DTO 검증 `[property: ...]`(record 위치파라미터) → .NET 8 InvalidOperationException→409. 파라미터 타깃으로 전환(11개 DTO).
- 근태 KST 일자 쿼리경계 +09:00 DateTimeOffset → timestamptz 바인딩 ArgumentException. `.ToUniversalTime()`.
- PII_ENCRYPTION_KEY 미설정 → 직원 동기화 실패. 생성·.220 .env 설정(유실 시 PII 복호화불가, 백업 필수).

## 결과
- 부서 12·직원 31 동기화 실증. 통합테스트 1→12 green(단위 287 포함 299/299). code-review 통과.
- 트레이드오프: enum→text로 DB레벨 값검증 사라짐 → 애플리케이션 레이어 검증 의존.

## 교훈 (→ lessons 2026-06-24 / active-rules Rule 11)
DB 스키마·데이터매핑 변경은 배포 전 ① 일괄편집 항목별 의미확인 ② code-reviewer 게이트
③ 실DB round-trip 값검증(단위·일부통합 통과는 거짓양성 가능).
