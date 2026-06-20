# Obsidian MCP 도구 정책 (obsidian-mcp-policy)

> 작성: 2026-06-13 | P0-6 산출물

## 현황 (2026-06-13 실측)

- **패키지**: obsidian-mcp v1.0.6
- **경로**: `/home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js`
- **vault**: `/home/bbw/obsidian-vault/bbw-wiki`

## 도구 노출 현황

### Claude Code (현재 설정)

obsidian-mcp가 settings.json의 `mcpServers.obsidian`으로 등록됨.
`disabled_tools` 설정 없음 → **delete 계열 도구 전부 노출 상태**.

| 도구명 | 유형 | 노출 여부 | 위험도 |
|--------|------|-----------|--------|
| `delete-note` | 삭제 | **노출** | 높음 |
| `move-note` | 이동 | **노출** | 중간 |
| `remove-tags` | 태그 제거 | **노출** | 낮음 |

### Codex

`disabled_tools` 6종 설정 완료 (§5.1 기준) — delete 계열 차단됨.

## 위험 등록

- **R5**: Claude Code에서 `delete-note` 도구 노출 확인 → Phase 3 Obsidian Gateway 구현(P3-1)으로 대체 전까지 임시 주의

## 금지 사항

- `delete-note` 명시적 호출 금지
- `move-note`로 vault 루트 밖으로 이동 금지
- `.obsidian/` 디렉터리 직접 조작 금지

## 대응 계획

| 단계 | 시점 | 조치 |
|------|------|------|
| 단기 | 현재 | Claude Code 세션에서 delete-note 미호출 자율 준수 |
| 중기 | Phase 3 P3-1 | Obsidian Gateway MCP로 대체 (delete 계열 미노출) |
| 완료 기준 | P3-1 완료 후 | raw obsidian-mcp settings.json 에서 제거 |
