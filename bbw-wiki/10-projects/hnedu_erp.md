---
title: "hnedu_erp — Windows 업무 대시보드"
id: "P-03"
status: "기획중"
phase: "Phase 0"
stack: [WinForms, .NET 8, C#, ASP.NET Core]
created: 2026-06-13
updated: 2026-06-18
summary: "WinForms 기반 사내 ERP, Phase 0 설계 완료, Phase 1 착수 전 GitHub 레포·Docker Compose 구조 설정 필요"
---

## 현재 상태

- **Phase**: Phase 0 — 기획·설계 단계
- **진행 상황**: Windows 바탕화면 고정형 업무·근태 통합 대시보드 설계 중

## 서버 / 인프라

| 항목 | 값 |
|------|-----|
| 플랫폼 | Windows (WinForms 전용) |
| 배포 형태 | 단일 실행 파일 (.exe) |
| 인증 의존 | hnedu_auth (JWT RS256) |

## 스택

- UI: WinForms (.NET 8)
- 언어: C#
- API: ASP.NET Core Web API
- ORM: EF Core Code-First

## 에이전트 허용 범위

| 에이전트 | 허용 | 금지 |
|---------|------|------|
| Claude Code | 설계·검토·문서화 | credential 파일 읽기 |
| winforms-agent | WinForms UI 구현 | .env·credential 읽기 |
| dotnet-api-agent | API·마이그레이션 구현 | .env 읽기 |
| agy | 리서치만 | 코드 수정 불가 |

## Dev Gate

Phase 0: 환경 설정 불필요. 기획·설계·코드 작업만.

Phase 1 이후 적용:
```bash
dotnet build --configuration Release
dotnet test
dotnet format --verify-no-changes
```

## 위험 구역

- hnedu_auth JWT 공개키 의존
- `docs/PLAN.md` 기획서가 레이아웃·기능의 유일한 기준 (design/ 아님)
- 문서 동기화 규칙: UI 변경 시 PLAN.md + DESIGN.md 동시 업데이트 필수

## 자주 쓰는 명령

```bash
# 기획서 확인
cat /home/bbw/projects/hnedu_erp/docs/PLAN.md

# 빌드 (Phase 1 이후)
dotnet build
```

## 최근 작업

- **2026-06-10**: Claude Code × Obsidian 연동 고도화 — obsidian-mcp 설치, ADR frontmatter 표준화
- **2026-06-09**: prototype 모듈화 (모노리식 5383줄 → CSS+JS 8파일), Spotlight 전역 검색 구현
- **2026-06-09**: `docs/layout-mockup.html` → `prototype/index.html` 이동, `docs/기획서.md` → `docs/PLAN.md`

## 현재 상태 (Phase 0 완료 대기)

- WinForms + ASP.NET Core 스택 확정
- 프로토타입(HTML): 모듈화 완료, 가상 DB 29명 직원 데이터 반영
- Phase 1 착수 조건: GitHub 레포 구조 설정 + Docker Compose 초안

## 다음 작업

- [ ] GitHub 레포 `/client` `/server` `/db` 구조 설정
- [ ] Docker Compose 초안 (ERP API + PostgreSQL + hnedu-auth)
- [ ] Phase 1 착수 선언

## 사내 시스템 배포 계획 (2026-06-19 확정)

회사망(공인 218.235.63.196, 동적IP)에 사내 ERP/CRM/Auth 배포. 홈서버 snowball.me.kr(221.165.64.216)와 별개, 도메인은 snowball.me.kr 서브도메인 재사용.

**구성**
- 서버1(우분투26.04): hnedu_auth — `auth.snowball.me.kr` 외부 노출, JWT 발급. ✅ 완료
- 서버2(우분투26.04): ERP+CRM 백엔드+DB — **회사 LAN 전용**(외부 미노출)
- 핸드폰 검증: **TOTP 앱**(무료) / 보안장비: 보류(PC 테스트 후)

**4계층 보안(ERP 직원전용)**: 네트워크 LAN한정 → JWT/RBAC → TOTP MFA → ERP API가 `amr:otp` 없는 토큰 거부

**스택 결정(senior-strategist 검증)**: ERP 백엔드=.NET 유지 / 인프라 Docker·Caddy·PG 재사용 / **SeaweedFS 제외→호스트 디스크볼륨+off-host rsync** / DB·네트워크 분리 / 지문=Polling 확정 / 인증서=**step-ca 사내CA**(루트키 오프라인 백업) / Next.js 미적용

**Phase**: A 서버2 Docker(192.168.0.220) / B ERP·CRM 배포(step-ca+Caddy+분리DB) / **C★ hnedu_auth TOTP MFA(코드)** / D ERP API amr검증+WinForms / E 향후

> 상세·진행상태: 프로젝트 메모리 `project_deploy_plan.md`. 재개 시 그 파일 기준.
