---
title: hnedu-auth 프로젝트 지침 (CLAUDE.md)
type: source
tags: [hnedu, auth, fastify, nextjs, project]
created: 2026-06-05
updated: 2026-06-05
origin: /home/bbw/projects/hnedu_auth/CLAUDE.md
author: blowbywind@hnedu.co.kr
date_published: 2026-06-05
summary: "해냄에듀 사내 통합 인증 서비스(hnedu-auth) 프로젝트 지침 — Fastify(3100)+Next.js 15(3200) 구성, Phase 1~11 완료·실서비스 연동 대기 중, ERP·CRM에 JWT RS25"
---

## 요약

해냄에듀 사내 통합 인증 서비스(hnedu-auth)의 프로젝트 지침 문서. Fastify 백엔드(포트 3100) + Next.js 15 관리자 UI(포트 3200)로 구성되며, Phase 1~11 전체 완료 후 실서비스 연동 대기 중. ERP·CRM 등 사내 시스템에 JWT(RS256)를 발급하는 중앙 인증 허브.

## 핵심 주장

- admin-ui/ 소스를 수정하고 `pnpm build`하면 `public/admin/`에 빌드 결과가 출력됨 — **`public/admin/` 직접 편집 절대 금지**
- 배포는 항상 `build → scp → docker logs` 3단계 수동 수행
- SSH 비대화형 세션에서는 매번 `PATH=~/.local/bin:~/.npm-global/bin:$PATH` 명시 필요
- Prisma 시드의 `upsert`에 `update: {}` 사용 시 기존 데이터 미갱신 — `update` 필드에 description 반드시 포함
- Docker ↔ UFW iptables 충돌로 컨테이너 재시작 시 LAN 인터넷 일시 끊김 이력 있음

## 반복 수행 작업 (자동화 후보)

| 작업 | 현재 방식 | 빈도 |
|------|----------|------|
| 관리자 UI 배포 | build → scp → docker 확인 (3단계) | UI 변경 시마다 |
| 서버 SSH 작업 | PATH 명시 후 pnpm 명령 | 서버 작업 시마다 |
| Prisma 스키마 변경 | migrate → generate (2단계) | 스키마 변경 시마다 |
| 배포 후 상태 확인 | docker logs --tail 10 | 배포 시마다 |
| DB 시드 재실행 | pnpm db:seed (또는 수동 SQL) | 역할 데이터 변경 시 |

## 연결된 개념

- [[wiki/concepts/hnedu-auth-deploy|hnedu-auth 배포 워크플로우]]
- [[wiki/concepts/jwt-rs256|JWT RS256 인증 패턴]]

## 연결된 엔티티

- [[wiki/entities/hnedu-auth|hnedu-auth]]
- [[wiki/entities/hnedu-erp|hnedu-erp (ERP)]]
- [[wiki/entities/hnedu-crm|hnedu-crm (CRM)]]

## 메모

- Phase 11은 Vanilla JS SPA로 완료됐고, 현재 Next.js 15로 admin-ui 리빌드 진행 중
- 잔여: ERP·CRM 실제 엔드포인트 통합 테스트 (각 서비스 구현 후 진행)
- `docs/DESIGN.md` = Warp 다크 테마 디자인 토큰 레퍼런스 — admin-ui 작업 시 반드시 참조
