---
title: hnedu-erp (ERP)
type: entity
tags: [project, hnedu, erp, dotnet, winforms]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-hnedu-auth-project]
---

## 개요

해냄에듀 ERP 시스템. hnedu-auth에서 발급한 JWT를 공개키로 검증해 인증한다.

| 항목 | 내용 |
|------|------|
| 클라이언트 | WinForms (C#) |
| 서버 | Web API (.NET) |
| 인증 방식 | JWT Bearer (공개키 서명 검증만 수행) |

## 역할 구조

- `ERP.ADMIN` — ERP 관리자
- `ERP.DEPT_LEADER` — 부서장 (직위 역할 도출에 사용)
- `ERP.USER` — 일반 사용자

## hnedu-auth와의 관계

- 직원의 `hire_date`, `prev_career_months` 값을 hnedu-auth에서 가져와 연차·승진 연한 계산 수행
- `job_title`·`department_path`는 표시 전용 — 비즈니스 로직은 ERP Ch.4에서 전담

## 현재 상태

연동 패턴 검증 완료 (`docs/integration-test/erp-verify.js`). 실제 엔드포인트 통합 테스트는 ERP 구현 후 진행 예정 (Phase 7-4).

## 주요 연결

- [[wiki/entities/hnedu-auth|hnedu-auth]] — 인증 허브
- [[wiki/concepts/jwt-rs256|JWT RS256 패턴]]

## 출처

- [[wiki/sources/2026-06-05-hnedu-auth-project]]
