---
title: "hnedu_auth 변경 영향 정책"
type: policy
tags: [hnedu_auth, dependency, policy]
created: 2026-06-13
updated: 2026-06-13
---

# hnedu_auth 변경 영향 분석 및 정책

> PM-3 산출물

## 의존 관계 구조

```
hnedu_auth (JWT RS256 발급)
    ├── hnedu_crm  — 공개키로 JWT 검증
    └── hnedu_erp  — 공개키로 JWT 검증
```

---

## 변경 유형별 영향 범위

### 1. JWT 키 로테이션 (private.pem 교체)

| 영향 범위 | 심각도 | 필수 조치 |
|---------|--------|---------|
| hnedu_crm JWT 검증 실패 | 높음 — 즉시 인증 불가 | 새 public.pem 배포 후 재시작 |
| hnedu_erp JWT 검증 실패 | 높음 — 즉시 인증 불가 | 새 public.pem 배포 후 재시작 |

**체크리스트**:
- [ ] 새 키 생성 완료
- [ ] hnedu_auth 재시작 → 헬스체크 통과
- [ ] hnedu_crm에 새 public.pem 배포 + 재시작
- [ ] hnedu_erp에 새 public.pem 배포 + 재시작
- [ ] `curl /auth/public-key` 로 새 키 노출 확인
- [ ] hnedu_crm 로그인 테스트
- [ ] hnedu_erp 로그인 테스트

### 2. JWT 스키마 변경 (payload 필드 추가/제거/이름 변경)

| 변경 유형 | 영향 범위 | 조치 |
|---------|---------|------|
| 필드 추가 (하위 호환) | 없음 | 소비자 측 선택적 적용 |
| 필드 이름 변경 | hnedu_crm, hnedu_erp 동시 | 3-way 배포 (auth → crm → erp 순) |
| 필드 제거 | hnedu_crm, hnedu_erp 동시 | 소비자 먼저 코드 제거 후 auth 제거 |

### 3. API 스펙 변경 (/auth/* 엔드포인트)

| 변경 | 영향 | 조치 |
|------|------|------|
| 엔드포인트 추가 | 없음 | 소비자 자유 채택 |
| 엔드포인트 URL 변경 | hnedu_crm, hnedu_erp 동시 | 소비자 먼저 업데이트 |
| 응답 구조 변경 | 소비자 파싱 오류 | 버전 접두사(`/v2/`) 사용 |
| 엔드포인트 제거 | hnedu_crm, hnedu_erp 동시 | Deprecation 기간 운영 후 제거 |

### 4. DB 스키마 변경 (Prisma 마이그레이션)

| 변경 | 영향 | 조치 |
|------|------|------|
| 테이블 추가 | 없음 | 직접 적용 가능 |
| 컬럼 추가 (nullable) | 없음 | 직접 적용 가능 |
| 컬럼 추가 (NOT NULL) | 기존 레코드 | 마이그레이션에 DEFAULT 포함 필수 |
| 컬럼 제거 | 코드 오류 | 코드 제거 후 마이그레이션 |
| 컬럼 이름 변경 | 코드 오류 | Prisma @map 또는 코드 동기 변경 |

---

## 변경 전 체크리스트 (공통)

```
□ 변경 유형 확인 (위 표 참조)
□ 영향받는 서비스 목록 확인
□ 배포 순서 결정 (영향 큰 변경은 소비자 먼저)
□ 롤백 계획 수립
□ 변경 후 헬스체크 URL 목록 준비
□ JWT 키 관련 변경 → 에이전트가 단독으로 실행 불가, 사용자 확인 필수
```

---

## 잔여 연동 항목 (실서비스 구현 후)

- [ ] `7-4` ERP 실제 엔드포인트 통합 테스트 (hnedu_erp Phase 1 구현 후)
- [ ] `8-4` CRM 실제 엔드포인트 통합 테스트 (hnedu_crm 백엔드 Phase 2 구현 후)
