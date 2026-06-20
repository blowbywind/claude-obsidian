---
title: Delete 도구 차단 확인 보고서
generated: 2026-06-13
phase: P3-3
status: verified
---

# Delete 도구 차단 확인 보고서

> P3-3 완료 기준: 3개 클라이언트 모두 delete 도구 미노출 확인

## 1. Codex

**상태: ✅ 차단 완료**

- 설정 위치: `~/.codex/config.toml`
- `disabled_tools` (6종):
  - `delete-note`, `delete_note`, `delete_notes`, `deleteNote`
  - `remove-note`, `remove_note`
- 완료 시점: §5.1 Codex 기준선 (P0 단계)

## 2. Claude Code

**상태: ✅ 차단 완료 (P3-3에서 확정)**

### 2a. raw `obsidian` MCP 항목
- 설정 위치: `~/.claude/settings.json` → `mcpServers.obsidian.disabled_tools`
- 차단 도구 (12종):
  - `delete-note`, `delete_note`, `delete_notes`, `deleteNote`
  - `remove-note`, `remove_note`
  - `move-note`, `move_note`
  - `permanent-delete`, `permanent_delete`
  - `remove-tags`, `remove_tags`
- 비고: R5 리스크 해소. gateway 완전 검증 후 raw 항목 제거 예정.

### 2b. `obsidian-gateway` MCP 항목 (P3-1 신규)
- 설정 위치: `~/.claude/settings.json` → `mcpServers.obsidian-gateway`
- 구현 위치: `/home/bbw/ai-ops/mcp-servers/obsidian-gateway/index.js`
- delete·permanent_delete·move-note 도구 **미등록** — 도구 목록 자체에 없음
- 보안: `realpath()` + ALLOWED prefix 재검사 (CVE-2025-53109/110 대응)
- 제공 도구: `create_task`, `append_task_log`, `update_task_status`, `create_adr`, `append_daily_log`, `read_project_note`

## 3. Hermes

**상태: ✅ 차단 완료**

- Hermes (Docker `hermes-dashboard`)는 MCP 직접 연동 없음
- 작업 위임 경로: `require-approval` → work card → 00-inbox/requests/ → 사람 승인
- `run-codex` / `run-claude` wrapper 경유 — 직접 Obsidian MCP 호출 없음
- 향후 MCP 연동 시 `obsidian-gateway`만 허용 (raw obsidian-mcp 비활성화)

## 요약

| 클라이언트 | delete 도구 차단 | 방법 |
|-----------|----------------|------|
| Codex | ✅ | `disabled_tools` 6종 (config.toml) |
| Claude Code (raw obsidian) | ✅ | `disabled_tools` 12종 (settings.json) |
| Claude Code (gateway) | ✅ | 도구 미등록 (구현 수준) |
| Hermes | ✅ | MCP 직접 연동 없음 |

**R5 리스크 상태: 해소 완료**
