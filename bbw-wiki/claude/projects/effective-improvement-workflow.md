---
name: effective-improvement-workflow
description: ai-ops 분석과 개선 작업에서 검증된 단계적 개선 워크플로.
metadata:
  type: feedback
summary: "병렬분석·교차검증·Phase별 구현·검증 게이트·별도검토로 대규모 개선의 회귀 위험을 낮춘다."
---

# effective-improvement-workflow

대규모 개선은 병렬 분석, 직접 교차검증, 단계별 구현, 검증 게이트 순서로 진행할 때 회귀 위험이 낮아집니다.

## 절차
- 구조, DB, 보안, 레포 위생을 분리해 분석한다.
- 심각도 높은 발견은 직접 파일과 실행 결과로 확인한다.
- Phase별로 작게 구현하고 타입체크와 테스트를 실행한다.
- 보안·DB·인프라 변경은 별도 검토 기준을 둔다.

## 관련
- [[rollback-prevention]]
- [[autobots-hardening-backlog]]
