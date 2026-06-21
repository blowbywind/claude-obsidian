# Claude 위키 인덱스

> 세션 시작 시 이 파일만 주입 → 필요한 노트를 온디맨드로 로드한다.
> 노트 추가·상태 변경 시 이 파일도 함께 업데이트할 것.

---

## 프로젝트 노트 (`projects/`)

| 프로젝트 | 한 줄 요약 | 현재 단계 | 노트 |
|----------|-----------|----------|------|
| autobots | AI 에이전트 운영 대시보드 (Fastify+Next.js, SQLite, port 9200) | v2.1 — backend UP (healthy) / hermes-dashboard UP / ai-ops-ui UP / 봇 9/9 active (갱신: 04:01Z) | [→](projects/autobots.md) |
| ai-agent-ops-plan | AI Ops 구현 계획 — Phase 0~4 로드맵 | Phase 0~3 완료, Phase 4 대기 | [→](projects/ai-agent-ops-plan.md) |
| hnedu_erp | 해냄에듀 Windows 풀스크린 업무·근태 대시보드 (win-screen) | Phase 0 완료, Phase 1 준비 중 | [→](projects/hnedu_erp.md) |
| hnedu_auth | 전사 통합 인증 서버. JWT RS256 발급, ERP·CRM 공통 허브 | Phase C 완료 - TOTP MFA 구현 (feat/mfa-totp, 배포 대기) | [→](projects/hnedu_auth.md) |
| hnedu_crm | 교사 CRM. 전국 41,264명 관계 정보 통합 관리 | Phase 1 운영 중 (Vanilla SPA) | [→](projects/hnedu_crm.md) |
| web-infra | 홈서버 Docker 인프라. snowball.me.kr / 221.165.64.216 | 운영 중 | [→](projects/web-infra.md) |
| pdf_to_html | PDF → HTML 변환기. Windows .exe 단일 배포 | 완성·유지보수 | [→](projects/pdf_to_html.md) |
| bbw_ebook | 전자책 관련 프로젝트 | 기획 중 | [→](projects/bbw_ebook.md) |
| obsidian-vault | 개인 지식 관리 볼트. AI 리서치·git 자동커밋·YouTube ingest | 운영 중 | [→](projects/obsidian-vault.md) |
| claude-config | Claude Code 글로벌 설정 (~/.claude/) | 유지보수 | [→](projects/claude-config.md) |
| firecrawl | 웹 크롤링 도구. ~/projects/firecrawl | 스텁 (마지막 활동 2026-06-11) | [→](projects/firecrawl.md) |

---

## 아키텍처 결정 (`decisions/`)

| 날짜 | 프로젝트 | 결정 내용 | 노트 |
|------|----------|----------|------|
| 2026-06-21 | autobots | 봇 자율 sudo/승인 UI 디버깅 -- SSE hijack, Caddy+Safari 인증, FastifyPlugin 재등록 | [->](decisions/2026-06-21-autobots-sudo-auth-debugging.md) |
| 2026-06-19 | hnedu_auth | TOTP MFA 핵심 결정 3건 — 2단계 플로우, ERP setup 강제, 복구코드 10개 | [→](decisions/2026-06-19-mfa-totp-decisions.md) |
| 2026-06-19 | claude-config | 세컨드 브레인 진화 — 감사 교정, 피드백 루프 폐쇄(SessionEnd 훅·검색 권유·승격 정책) | [→](decisions/2026-06-19-second-brain-evolution.md) |
| 2026-06-10 | claude-config | 컨텍스트 소진 원인 분석 — @멘션+누적이 방아쇠, 재발 방지 규칙 | [→](decisions/2026-06-10-context-exhaustion.md) |
| 2026-06-09 | web-infra | VS Code 원격 환경 포트 충돌 해결 방법 | [→](decisions/2026-06-09-vscode-port-conflict.md) |
| 2026-06-08 | hnedu_erp | 모노리식 HTML → CSS+JS 8파일 모듈화 | [→](decisions/2026-06-08-erp-prototype-modularize.md) |
| 2026-06-08 | claude-config | Obsidian을 Claude 메모리로 연동하는 아키텍처 | [→](decisions/2026-06-08-obsidian-memory.md) |
| 2026-06-08 | web-infra | ufw-docker 도입 (방화벽 + Docker 포트 정책) | [→](decisions/2026-06-08-ufw-docker.md) |
| 2026-06-08 | web-infra | 서비스 위치 /opt로 이전 | [→](decisions/2026-06-08-webinfra-opt.md) |

---

## 메모리 파일 통계

> 마지막 갱신: 2026-06-21T04:01Z (autobots-scheduler) -- session-log 15959라인, vault 678 md

| 범위 | 파일 수 | 변동 |
|------|------|-----|
| bbw-wiki/ (전체) | 678 md | +2 |
| claude/ | 35 md (projects:**11**, decisions:**10**, 루트:4, 90-agent-logs:10) | = |
| 50-prompts/ | 6 md (claude:3, codex:2, hermes:1, gemini:0) | = |
| wiki/ | 250 md (sources:32, concepts:**179**, entities:37, queries:1) | = |
| 90-agent-logs/ (bbw-wiki 루트) | 194 md (daily:188) | +2 |
| session-log.md | 15959라인 | +135 |
| work-in-progress.md | 47라인 | = |

### ai-ops 프로젝트 메모리 (`~/.claude/projects/-home-bbw-ai-ops/memory/`)

| 파일 | 라인 | 크기 | 최종 수정 |
|------|------|------|----------|
| MEMORY.md | 16 | 2.1K | 2026-06-21 |
| autobots-erp-ssh.md | 23 | 2.0K | 2026-06-20 |
| autobots-hardening-backlog.md | 29 | 3.8K | 2026-06-20 |
| autobots-identity.md | 20 | 1.5K | 2026-06-19 |
| bot-autonomous-sudo.md | 28 | 3.8K | 2026-06-21 |
| codex-bwrap-apparmor-fix.md | 38 | 2.8K | 2026-06-20 |
| effective-improvement-workflow.md | 28 | 2.5K | 2026-06-19 |
| feedback-rina-ux-rules.md | 20 | 1.1K | 2026-06-18 |
| lessons.md | 213 | 25K | 2026-06-21 |
| responsive-design-guide.md | 296 | 9.0K | 2026-06-19 |
| server-infra.md | 30 | 1.8K | 2026-06-20 |
| ui-ux-design-learning.md | 302 | 12K | 2026-06-19 |
| **합계** | **1043** | ~65K | 12파일 |

일별 통계 로그: [90-agent-logs/daily/](../90-agent-logs/daily/)

---

## 세션 로그

최근 작업 기록: [session-log.md](session-log.md)
