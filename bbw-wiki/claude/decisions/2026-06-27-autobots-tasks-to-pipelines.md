---
title: Autobots Tasks 기능을 Pipelines로 흡수
type: decision
status: accepted
owner: bbw
created: 2026-06-27
updated: 2026-06-27
accepted: 2026-06-27
tags: [ai-ops, autobots, pipelines, tasks, simplification]
summary: "Tasks 제품을 Pipelines로 흡수하고 /tasks 라우트 제거, [[TASK]] 디렉티브를 pipeline_runs으로 처리."
---

# Autobots Tasks 기능을 Pipelines로 흡수

## 결정

Autobots의 독립 `Tasks` 제품 표면을 제거하고, 작업 생성·승인·실행 상태 추적을 `Pipelines`로 통합한다.

## 배경

- 프론트에는 `/tasks` 페이지가 없고, 실제 사용자 표면은 `/pipelines`가 담당한다.
- `Pipelines`는 `pipeline_runs`, `pipeline_run_stages`, `approval_history`를 기반으로 작업 생성, 승인 대기, 승인·거부, 실행 상태, SSE 갱신을 이미 처리한다.
- legacy `Tasks` 경로는 인박스 마크다운 카드와 `task-update` 감시자로 남아 있었고, 제품 표면과 실행 표면이 중복됐다.

## 적용

- `/tasks` 백엔드 라우트와 `task-queue` 감시자를 제거한다.
- `[[TASK: 제목 | risk | project | botId]]` 디렉티브는 인박스 카드 대신 `pipeline_runs`를 생성한다.
- `[[APPROVE: runId]]`, `[[REJECT: runId | reason]]`는 파이프라인 승인·반려로 처리한다.
- 프론트의 미사용 `TaskApprovalCard`, `taskStore`를 제거한다.
- 계획 문서의 독립 Tasks 항목을 Pipelines 항목으로 합친다.

## 보존

기존 `~/obsidian-vault/bbw-wiki/00-inbox/requests/` 마크다운 카드 15개는 삭제하지 않는다. 이번 결정은 새 기능 표면과 백엔드 실행 경로를 Pipelines로 통합하는 것이며, 과거 인박스 기록 삭제나 자동 재실행 마이그레이션은 포함하지 않는다.

## 검증

- `npm --prefix autobots/backend run typecheck`
- `npm --prefix autobots/backend test`
- `npm --prefix autobots/frontend run lint`
- `npm --prefix autobots/frontend run build`

검증 결과 백엔드 타입체크와 141개 테스트, 프론트 린트, 프론트 정적 빌드가 통과했다. 새 정적 빌드 라우트 목록에 `/tasks`는 없다.
