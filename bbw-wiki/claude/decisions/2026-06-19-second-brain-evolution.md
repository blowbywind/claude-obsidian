---
date: 2026-06-19
project: claude-config
status: 적용 완료
tags: [claude-code, obsidian, second-brain, hooks, audit]
---

# 세컨드 브레인 진화 — 감사 결과 교정 및 피드백 루프 폐쇄

**날짜**: 2026-06-19
**프로젝트**: claude-config
**상태**: 적용 완료 (사용자 승인 후 config 3종 적용·검증 완료)

## 배경

`CLAUDE_CODE_OBSIDIAN_WIKI_USAGE_AUDIT_2026-06-19.md` 감사가 성숙도 42/100으로 평가했으나,
해당 감사는 **모든 라이브 검증이 실패한 상태**(Codex 실행 래퍼 깨짐, MCP 타임아웃)에서 작성됨.
Claude Code로 직접 검증한 실제 상태는 감사 가정과 다름.

## 감사 교정 (검증된 사실)

| 감사 주장 | 실제 검증 결과 |
|-----------|----------------|
| Obsidian MCP 타임아웃 → 연동 불건전 | MCP `obsidian-gateway`는 **autobots 전용 append-only 게이트웨이**(`90-agent-logs/`만 기록). 인간 세션은 파일시스템 직결 — MCP 무관하게 정상 |
| `AGENTS.md` 브릿지 필요 | 해당 없음. `~/.claude/CLAUDE.md` 정상 로드 중 |
| auto memory ↔ Obsidian 경쟁 원장 | 계층 분리 실재: 인간 볼트 / `claude/` 원장 / 봇 로그 / 로컬 메모리. 단 승격 규칙은 미명시 |
| 권한 경계 없음 | settings.json deny에 `.env`·`secrets`·`.ssh`·`.aws`·`gcloud`·파괴적 bash 이미 차단 |
| 감사 추적 없음 | session-log 설계는 존재하나 **훅 미등록으로 미작동** |

실제 성숙도 추정: **약 72/100** (설계·권한·계층분리 우수, 피드백 루프 일부 단절).

## 검증된 결함 3개

1. **세션 로그 루프 단절**: `hooks/session-stop/save-session.sh` 완성됐으나 `settings.json`에
   `SessionEnd` 훅으로 미등록 → 자동 기록 한 번도 실행 안 됨.
2. **"작업 전 볼트 검색" 무음**: `load-context.sh`는 프로젝트 노트가 존재할 때만 주입.
   부재 시 검색 권유 없음 → 과거 결정 모르고 작업 시작 위험.
3. **메모리 승격 정책 부재**: 로컬 `~/.claude/memory/` ↔ Obsidian `claude/` 승격 기준 미명시.

## 결정 (진화 방향)

피드백 루프를 닫는다. 새 시스템 추가가 아니라 **이미 설계된 경로를 활성화**하는 데 집중.

### 적용 완료 (문서)
- 이 ADR + INDEX 갱신
- `~/.claude/memory/` 에 진화 기록 + MEMORY.md 인덱스

### 적용 완료 (config — 사용자 승인 후, jq/bash -n/런타임 검증 완료)
- `settings.json`: `SessionEnd` 훅 등록 → `save-session.sh` 활성화 (결함 1)
- `load-context.sh`: 프로젝트 노트 부재 시 `grep` 검색 권유 1줄 주입 (결함 2, 런타임 검증: 노트 부재 시만 발동)
- `~/.claude/CLAUDE.md`: "메모리 승격 정책" + "작업 전 볼트 검색" 계약 추가 (결함 3)

## 승격 정책 (제안)

- **로컬 메모리 유지**: 반복 실행 명령, 빌드/디버깅 팁, 재발 방지 규칙 (active-rules·lessons)
- **`claude/decisions/` 승격**: 되돌리기 어려운 기술 결정
- **`claude/projects/` 승격**: 프로젝트 상태 변경
- **WIP 갱신**: 긴 작업·기기 전환·세션 종료 전
- **작업 전 검색**: 과거 결정·선호·히스토리가 영향 줄 수 있으면 `grep -ri` 로 볼트 먼저 검색

## 보류 (사용자 판단 필요)
- MCP `obsidian-gateway`를 인간 세션 settings.json에서 제거할지 (봇 전용이라 대화형엔 중복)
- root 소유 파일(session-log·episodic·90-agent-logs) 소유권 정리 (autobots가 root로 기록)
- 번호 폴더 vs `claude/` taxonomy 중복 명명(`90-agent-logs`) 정리

## 참조
- [[2026-06-08-obsidian-memory]] — 최초 연동 결정
- [[2026-06-10-context-exhaustion]] — 컨텍스트 관리
