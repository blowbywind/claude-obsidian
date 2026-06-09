# Claude 위키 인덱스

> 세션 시작 시 이 파일만 주입 → 필요한 노트를 온디맨드로 로드한다.
> 노트 추가·상태 변경 시 이 파일도 함께 업데이트할 것.

---

## 프로젝트 노트 (`projects/`)

| 프로젝트 | 한 줄 요약 | 현재 단계 | 노트 |
|----------|-----------|----------|------|
| hnedu_erp | 해냄에듀 Windows 풀스크린 업무·근태 대시보드 (win-screen) | Phase 0 완료, Phase 1 준비 중 | [→](projects/hnedu_erp.md) |
| hnedu_auth | 전사 통합 인증 서버. JWT RS256 발급, ERP·CRM 공통 허브 | Phase 1 개발 중 | [→](projects/hnedu_auth.md) |
| hnedu_crm | 교사 CRM. 전국 41,264명 관계 정보 통합 관리 | Phase 1 운영 중 (Vanilla SPA) | [→](projects/hnedu_crm.md) |
| web-infra | 홈서버 Docker 인프라. snowball.me.kr / 221.165.64.216 | 운영 중 | [→](projects/web-infra.md) |
| pdf_to_html | PDF → HTML 변환기. Windows .exe 단일 배포 | 완성·유지보수 | [→](projects/pdf_to_html.md) |
| bbw_ebook | 전자책 관련 프로젝트 | 기획 중 | [→](projects/bbw_ebook.md) |
| obsidian-vault | 개인 지식 관리 볼트. AI 리서치·git 자동커밋·YouTube ingest | 운영 중 | [→](projects/obsidian-vault.md) |
| claude-config | Claude Code 글로벌 설정 (~/.claude/) | 유지보수 | [→](projects/claude-config.md) |

---

## 아키텍처 결정 (`decisions/`)

| 날짜 | 프로젝트 | 결정 내용 | 노트 |
|------|----------|----------|------|
| 2026-06-10 | claude-config | 컨텍스트 소진 원인 분석 — @멘션+누적이 방아쇠, 재발 방지 규칙 | [→](decisions/2026-06-10-context-exhaustion.md) |
| 2026-06-09 | web-infra | VS Code 원격 환경 포트 충돌 해결 방법 | [→](decisions/2026-06-09-vscode-port-conflict.md) |
| 2026-06-08 | hnedu_erp | 모노리식 HTML → CSS+JS 8파일 모듈화 | [→](decisions/2026-06-08-erp-prototype-modularize.md) |
| 2026-06-08 | claude-config | Obsidian을 Claude 메모리로 연동하는 아키텍처 | [→](decisions/2026-06-08-obsidian-memory.md) |
| 2026-06-08 | web-infra | ufw-docker 도입 (방화벽 + Docker 포트 정책) | [→](decisions/2026-06-08-ufw-docker.md) |
| 2026-06-08 | web-infra | 서비스 위치 /opt로 이전 | [→](decisions/2026-06-08-webinfra-opt.md) |

---

## 세션 로그

최근 작업 기록: [session-log.md](session-log.md)
