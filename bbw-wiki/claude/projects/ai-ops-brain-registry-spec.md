---
title: ai-ops 두뇌 레지스트리 규약 (Phase 3)
type: spec
status: draft
owner: bbw
created: 2026-06-23
last_verified: 2026-06-23
review_by: 2026-09-23
project: ai-ops
adr: claude/decisions/2026-06-21-ai-ops-platform-direction.md
parent: claude/projects/ai-ops-build-plan.md
tags: [ai-ops, brain, registry, phase-3, spec, governance]
summary: "결정/명세/런북 등 타입별 권위와 frontmatter 메타데이터(소유자·검증일·신선도) + 신선도 정책으로 공유 두뇌를 검증된 아티팩트 레지스트리로 운영하는 규약."
---

# ai-ops 두뇌 레지스트리 규약

> **목적**: 공유 두뇌를 "기본 진실원"이 아니라 **검증된 아티팩트 레지스트리**로 전환. codex 교차검증 최대 결함("취약 브레인 중앙화 = 오염 중앙집중화") 대응.
> **원칙**: 권위는 *타입 고정 + 신선도 + 소유자*가 있는 노트에만. 자유 메모는 비권위 참고용. grep+wikilink 효율 유지(전체 마이그레이션 금지).

## 1. 권위 타입 (registry — RAG가 신뢰)
| 타입 | 디렉터리 | 권위 근거 | 신선도 모델 |
|------|----------|-----------|-------------|
| `decision`(ADR) | `claude/decisions/`, `40-decisions/` | `status: accepted` | 시간만료 아님 — `superseded`로 폐기 |
| `spec` | `claude/projects/`(type:spec), `80-templates` 제외 | `status: draft\|approved` + owner | `review_by` 경과 시 stale |
| `runbook` | `30-runbooks/` | owner + last_verified | `review_by`(운영정확도 부패) |
| `project`(상태) | `claude/projects/`, `10-projects/` | owner + last_verified | `review_by` 또는 last_activity |
| `test-evidence` | (신규) `claude/projects/` 또는 commit 첨부 | 커밋 해시 + 날짜 | 커밋 변경 시 무효 |
| `postmortem` | `40-decisions/` 또는 신규 | 사건 날짜 | 불변(역사 기록) |

## 2. 필수 frontmatter (권위 노트)
```yaml
type: decision|spec|runbook|project|test-evidence|postmortem
owner: <사람>            # 유지 책임자 (기본 bbw)
last_verified: YYYY-MM-DD # 사람이 정확성 마지막 확인
review_by: YYYY-MM-DD     # 신선도 마감 (decision/postmortem 제외)
status: <타입별>          # accepted/superseded · draft/approved · ...
```
- `decision`·`postmortem`은 `review_by` 면제(불변/supersede 모델). 나머지는 필수.
- 누락 = 감사에서 비권위로 강등(경고).

## 3. 비권위 (free memo — RAG 저신뢰/제외)
- `00-inbox/`, `20-research/`, `90-agent-logs/`, `episodic/`, `raw/`, `session-log.md`, daily 로그.
- `wiki/concepts/_drafts/`(`status: ai-curated`) — **이미 RAG 제외**(stream-engine `isUnverifiedCuration`). 현재 114개.
- 자유 메모는 참고용으로만 쓰이고 "진실원"으로 승급되지 않는다(사람이 권위 타입으로 옮겨야 승급).

## 4. 신선도 정책
- `review_by < today` → **stale**. 감사가 플래그. RAG는 stale 노트를 `⚠stale` 마킹(하드 제외 아님 — 유용정보 은폐 방지). ※ RAG 마킹 적용은 §6 결정 대기.
- `decision status: superseded` → RAG 제외.
- 권장 review_by 주기: spec/runbook 90일, project 90일(또는 last_activity 60일 무활동 시 재확인).

## 5. 큐레이션·갱신 루프 (구현)
- **감사 스크립트**: `autobots/scripts/governance/brain-registry-audit.mjs` (결정론·read-only, cron job_type=script). 권위 dir 스캔 → ① 필수 metadata 누락 ② stale(review_by 경과) ③ superseded 미반영. 리포트만, 파일 무변경. 기존 `wiki_integrity_scan.py`와 상보(그건 링크/고아/wiki 스키마, 이건 권위/신선도).
- 갱신: stale 발견 → 사람이 last_verified/review_by 갱신 또는 supersede.

## 6. 미결 (사용자 결정 — RAG 동작 변경)
- [ ] RAG(`resolveMemoryContext`)가 권위 타입·신선도를 반영하도록 확장할지:
  - (보수) stale도 포함하되 `⚠stale` 마킹만 — 권장(은폐 없음).
  - (엄격) stale·비권위 dir 제외 — 강한 게이트지만 유용정보 손실 위험.
  - 현재는 **미변경**(ai-curated 제외만 유지). 결정 후 적용.
- [ ] `test-evidence`·`postmortem` 전용 dir 신설 여부(현재 claude/projects 겸용).

## 관련
[[ai-ops-build-plan]] · [[ai-ops-platform-direction]] · [[ai-ops-slo-spec]] · [[autobots-identity]]
