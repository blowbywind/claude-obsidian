---
title: hnedu-crm (CRM)
type: entity
tags: [project, hnedu, crm, fastapi, nextjs]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-hnedu-auth-project]
summary: "hnedu-auth JWT 공개키 검증 기반 Next.js+FastAPI CRM 시스템으로 6개 역할 지원 및 연동 패턴 검증 완료."
---

## 개요

해냄에듀 CRM 시스템. hnedu-auth에서 발급한 JWT를 공개키로 검증해 인증한다.

| 항목 | 내용 |
|------|------|
| 클라이언트 | Next.js 15 |
| 서버 | FastAPI (Python) |
| 인증 방식 | JWT Bearer / Cookie (공개키 서명 검증만 수행) |

## 역할 구조 (system_code = 'CRM')

- `CRM.ADMIN` — CRM 관리자
- `CRM.MANAGER` — 매니저
- `CRM.SENIOR` — 시니어
- `CRM.JUNIOR` — 주니어
- `CRM.VIEWER` — 조회 전용
- `CRM.EXTERNAL` — 외부 파트너

## 현재 상태

연동 패턴 검증 완료 (`docs/integration-test/crm-verify.py`). 실제 엔드포인트 통합 테스트는 CRM 백엔드 구현 후 진행 예정 (Phase 8-4).

## 주요 연결

- [[wiki/entities/hnedu-auth|hnedu-auth]] — 인증 허브
- [[wiki/concepts/jwt-rs256|JWT RS256 패턴]]

## 출처

- [[wiki/sources/2026-06-05-hnedu-auth-project]]
