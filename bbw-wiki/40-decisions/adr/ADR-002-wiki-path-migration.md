---
title: "ADR-002: bbw-wiki 구 경로 이관 계획 (claude/ → 40-decisions/, wiki/ → 이관 대상)"
id: "ADR-002"
status: "proposed"
created: 2026-06-13
updated: 2026-06-13
deciders: [bbw]
supersedes: ""
superseded_by: ""
---

## 맥락

P1-4 경로 감사 결과. bbw-wiki 내 구 경로가 신규 번호 구조와 공존 중:

| 구 경로 | 내용 | 신규 대상 경로 |
|---------|------|--------------|
| `claude/` | INDEX.md, decisions/, projects/, session-log.md, work-in-progress.md | `40-decisions/`, `10-projects/`, `90-agent-logs/` |
| `wiki/` | concepts/, entities/, sources/, queries/, overview.md | 현행 유지 또는 `20-research/` 하위로 이관 검토 |
| `raw/` | 원본 소스 자료 | 현행 유지 (CLAUDE.md: 에이전트 수정 금지) |

**신규 파일(10-projects/, 40-decisions/ 등)이 구 경로를 참조하는 경우는 현재 없음** — 이관 영향 없음.

## 결정

**단계적 이관. 즉시 대량 이동 금지.**

1. `claude/decisions/` → `40-decisions/adr/`에 개별 복사 (내용 검토 후)
2. `claude/projects/` → `10-projects/`에 합산 검토 (이미 stub 생성됨)
3. `claude/session-log.md`, `claude/work-in-progress.md` → `90-agent-logs/daily/` 이관
4. `wiki/` → 현행 유지 (Obsidian CLAUDE.md 기존 스키마 기준)
5. `raw/` → 현행 유지 (에이전트 수정 금지 원칙)

## 이유

- 즉시 대량 이동 시 내부 링크 깨짐 위험
- `wiki/`는 기존 Obsidian CLAUDE.md에 정의된 스키마 구조로 별도 관리
- `raw/`는 수정 금지 대상이므로 위치 변경 최소화

### 이관 순서

| 단계 | 작업 | 시점 |
|------|------|------|
| 1 | claude/decisions/ 내용 검토 | Phase 1 P1-4 |
| 2 | claude/projects/ → 10-projects/ stub과 통합 | PM-1 이후 |
| 3 | session-log.md 이관 | Phase 1 말 |
| 4 | wiki/ 구조 재검토 | Phase 2 이후 |

## 준수 기준

- 이관 전 `cp -r`로 원본 보존 후 검증
- 이관 후 Obsidian에서 링크 깨짐 없는지 확인
