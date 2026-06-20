# MCP/Hook Adversarial Smoke Test

> 실행일: 2026-06-13 | P0-9 산출물

## 결과 요약

| 케이스 | 방법 | 결과 | 비고 |
|--------|------|------|------|
| secret read block | settings.json deny 정책 확인 | ✅ **차단 확인** | P0-2 완료 — deny에 ssh·aws·gcloud 경로 포함 |
| destructive command block | settings.json + hook deny 확인 | ✅ **차단 확인** | rm -rf·systemctl·crontab·git push deny 등록 |
| MCP delete block | obsidian-mcp 도구 목록 확인 | ✅ **해소 완료** | P3-1 gateway + disabled_tools 12종 (2026-06-13) |
| hook safety | bash -n 구문 검사 5개 파일 | ✅ **통과** | 5개 hook 전부 pass |
| hermes 중복 프로세스 | P0-3 정리 완료 확인 | ✅ **해소됨** | hermes-dashboard 단독 운영, port 9120 소멸 |
| prompt injection boundary | 수동 점검 | ⚠️ **미완료** | Phase 3 이후 gateway 구현 시 재실행 |
| wrapper timeout | run-gemini bash -n 검사 | ✅ **통과** | bash -n pass, timeout 동작은 실행 시 확인 |
| symlink bypass | Phase 3 gateway 구현 후 실시 | ⏳ **연기** | Phase 3 P3-1 완료 후 재실행 |

## 실패/경고 항목 → Risk Register

| 항목 | 위험도 | 상태 | 대응 |
|------|--------|------|------|
| ~~settings.json JSON 파싱 실패~~ | ~~높음~~ | ✅ **P0-2 완료** | 주석 제거·deny 보강 완료 (2026-06-13) |
| obsidian-mcp delete-note 노출 | 높음 | **✅ R5 해소** | P3-1 gateway + settings.json disabled_tools 12종 추가 (2026-06-13) |
| ~~hermes 프로세스 중복 실행~~ | ~~높음~~ | ✅ **P0-3 완료** | hermes-dashboard 단독 운영 확인 (2026-06-13) |

## Hook 검사 결과

```
OK: ~/.claude/hooks/pre-tool-use/block-dangerous.sh
OK: ~/.claude/hooks/pre-tool-use/block-env-read.sh
OK: ~/.claude/hooks/post-tool-use/auto-format.sh
OK: ~/.claude/hooks/session-start/load-context.sh
OK: ~/.claude/hooks/session-stop/save-session.sh
```

## 재실행 필요 조건

- P0-2 완료 후: secret read block, destructive command block 재검증
- Phase 3 P3-1 완료 후: symlink bypass, MCP delete block 재검증
