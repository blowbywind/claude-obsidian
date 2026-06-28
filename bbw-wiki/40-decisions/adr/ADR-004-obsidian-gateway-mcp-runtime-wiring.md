---
id: ADR-004
title: "obsidian-gateway MCP runtime wiring"
status: accepted
date: 2026-06-28
---

## 컨텍스트

ai-ops에는 append-only allowlist 기반 `obsidian-gateway` MCP 서버와 `mcp_tool_fingerprints` 저장 테이블이 이미 존재했다. 그러나 자동 봇 spawn 경로가 MCP 서버를 명시적으로 주입하지 않아, 봇은 전역 Claude 설정이나 직접 파일 쓰기에 의존할 수 있었다.

기존 합의는 다음과 같다.

- Obsidian 발견과 검색은 기존 `--add-dir` + grep/RAG 경로를 유지한다.
- 정형 작업 카드, ADR, 일일 로그, 작업 로그 같은 쓰기 경로는 MCP gateway로 코드화된 allowlist를 적용한다.
- 외부 MCP 연동은 별도 고위험 결정으로 분리한다.

## 결정

Claude Code 기반 자동 봇 spawn에는 사내 `obsidian-gateway`만 `--mcp-config`로 명시 주입하고 `--strict-mcp-config`를 함께 사용한다. 적용 대상은 대화형 chat, project workspace, agent cron, pipeline 실행 경로다.

허용 도구는 현재 gateway가 노출하는 6개 도구를 명시 목록으로만 둔다.

- `create_task`
- `append_task_log`
- `update_task_status`
- `create_adr`
- `append_daily_log`
- `read_project_note`

와일드카드 허용은 금지한다. 이후 gateway에 삭제, 이동, 외부 연동 도구가 추가되더라도 자동으로 권한이 열리지 않게 하기 위함이다.

백엔드는 부팅 시 실제 `tools/list` 응답을 probe해 fingerprint를 DB에 등록 또는 재검증한다. drift나 probe 실패는 `security_events`와 SSE로 노출한다.

## 결과

정형 Obsidian 쓰기 경로는 프롬프트 지침이 아니라 MCP 서버의 realpath, allowlist, idempotency, 감사로그 구현을 통과한다.

전역 Claude 사용자 설정에 어떤 MCP가 있든 자동 봇 세션은 사내 gateway만 로드한다. 외부 MCP 도입은 이 ADR의 범위 밖이며, 별도 핀 고정, 토큰 바운딩, SSRF 방어, 승인 게이트 결정을 필요로 한다.

읽기 발견 경로는 기존 파일 접근과 위키 검색 흐름을 유지한다. `read_project_note`는 gateway의 좁은 허용 경로 단건 조회 도구로만 남긴다.
