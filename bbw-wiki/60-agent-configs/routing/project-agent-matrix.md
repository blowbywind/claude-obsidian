---
title: "프로젝트별 에이전트 할당 매트릭스"
type: concept
tags: [routing, risk-map, agent-assignment]
created: 2026-06-13
updated: 2026-06-13
---

# 프로젝트별 에이전트 할당 매트릭스

> PM-4 산출물 | 에이전트가 작업 전 참조하는 라우팅 기준 문서

## 위험도 정의

| 위험도 | 기준 | 에이전트 자동 실행 |
|--------|------|----------------|
| Low | 텍스트·주석·문서 변경 | 가능 |
| Medium | 기능 추가·리팩터링 | 가능 (리뷰 권장) |
| High | DB 스키마·인증·API 스펙 변경 | **사용자 확인 필수** |
| Critical | 키 로테이션·배포·롤백·보안 패치 | **사용자 확인 필수** |

---

## 프로젝트별 매트릭스

### P-01 hnedu_auth (통합 인증 서비스)

| 에이전트 | 허용 경로 | 기본 위험도 | 제한 사항 |
|---------|---------|-----------|---------|
| Claude Code | `/home/bbw/projects/hnedu_auth/` (read) | Medium | credential 읽기 금지 |
| Codex | `/home/bbw/projects/hnedu_auth/src/` | Medium | keys/ · .env 접근 금지 |
| backend-agent | `/home/bbw/projects/hnedu_auth/` | High | DB 스키마 변경 시 사용자 확인 |
| agy | 없음 (리서치만) | Low | 코드 수정 불가 |

**승인 필요 작업**: JWT 키 로테이션, DB 마이그레이션, API 스펙 변경, 배포

---

### P-02 hnedu_crm (교사 CRM)

| 에이전트 | 허용 경로 | 기본 위험도 | 제한 사항 |
|---------|---------|-----------|---------|
| Claude Code | `/home/bbw/projects/hnedu_crm/` (read) | Medium | .env 읽기 금지 |
| Codex | `/home/bbw/projects/hnedu_crm/` | Medium | .env 접근 금지 |
| frontend-agent | `/home/bbw/projects/hnedu_crm/frontend/` | Medium | |
| backend-agent | `/home/bbw/projects/hnedu_crm/backend/` | High | DB 변경 시 사용자 확인 |
| agy | 없음 (리서치만) | Low | 코드 수정 불가 |

**승인 필요 작업**: DB 스키마 변경, hnedu_auth 의존 API 스펙 변경

---

### P-03 hnedu_erp (Windows 업무 대시보드)

| 에이전트 | 허용 경로 | 기본 위험도 | 제한 사항 |
|---------|---------|-----------|---------|
| Claude Code | `/home/bbw/projects/hnedu_erp/` (read) | Medium | |
| winforms-agent | `/home/bbw/projects/hnedu_erp/` | Medium | .env 접근 금지 |
| dotnet-api-agent | `/home/bbw/projects/hnedu_erp/` | High | DB 마이그레이션 시 사용자 확인 |
| agy | 없음 (리서치만) | Low | 코드 수정 불가 |

**승인 필요 작업**: DB 스키마 변경, hnedu_auth 공개키 업데이트

---

### P-04 pdf_to_html (PDF 변환기)

| 에이전트 | 허용 경로 | 기본 위험도 | 제한 사항 |
|---------|---------|-----------|---------|
| Claude Code | `/home/bbw/projects/pdf_to_html/` (read) | Low | references/ 수정 금지 |
| Codex | `/home/bbw/projects/pdf_to_html/` | Medium | .venv 직접 수정 금지 |
| agy | 없음 (리서치만) | Low | 코드 수정 불가 |

**주의**: stdout JSON 포맷 변경 시 호출 측 영향 분석 필수

---

### P-05 firecrawl (웹 스크레이퍼 — 외부 프로젝트)

| 에이전트 | 허용 경로 | 기본 위험도 | 제한 사항 |
|---------|---------|-----------|---------|
| Claude Code | `/home/bbw/projects/firecrawl/` (read) | Medium | |
| Codex | `/home/bbw/projects/firecrawl/apps/api/` | Medium | |
| agy | 없음 (리서치만) | Low | 코드 수정 불가 |

**필수**: PR + CI 통과 없이 변경 금지. `pnpm harness` 사용 (직접 start 금지)

---

### P-06 bbw_ebook (eBook Viewer)

| 에이전트 | 허용 경로 | 기본 위험도 | 제한 사항 |
|---------|---------|-----------|---------|
| Claude Code | `/home/bbw/projects/bbw_ebook/` (read) | Low | **Dev Gate 전 코드 수정 일체 금지** |
| Codex | **Dev Gate 전 금지** | — | "개발해줘" 명시 후에만 허용 |
| agy | 없음 (리서치만) | Low | 코드 수정 불가 |

**Dev Gate**: 사용자가 "개발해줘" 명시 전까지 코드 작성·수정 금지

---

## 공통 금지 사항 (전 프로젝트)

- `.env`, `*.pem`, `*key*`, `*secret*`, `*credential*` 파일 읽기 금지
- `~/.ssh/`, `~/.aws/`, `~/.config/gcloud/` 접근 금지
- git push 에이전트 단독 실행 금지 (사용자 확인 필수)
- `eval` 사용 금지 (RCE 위험)
- 환경변수 `export SECRET=xxx` 형식으로 secret 전달 금지
