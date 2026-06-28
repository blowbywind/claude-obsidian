---
title: "ADR-001: 운영 기준 경로 확정 (/projects + /ai-ops)"
id: "ADR-001"
status: "accepted"
created: 2026-06-13
updated: 2026-06-13
deciders: [bbw]
supersedes: ""
superseded_by: ""
summary: "에이전트 allowed_roots를 `/home/bbw/projects/`(앱 코드)와 `/home/bbw/ai-ops/`(AI 인프라) 두 경로로 확정해 파일시스템 공격 범위를 최소화한 운영 기준 경로 ADR."
---

## 맥락

서버 `/home/bbw/` 하위에 여러 경로가 혼재. 에이전트 작업 범위와 allowed_roots를 명확히 하기 위해 운영 기준 경로를 확정해야 함.

기존에 `/srv/ai/` 경로 사용이 검토됐으나 실제 운영은 `/home/bbw/`에서 진행되고 있었음.

## 결정

**운영 기준 경로 두 개로 확정:**
- `/home/bbw/projects/` — 애플리케이션 코드 (6개 프로젝트)
- `/home/bbw/ai-ops/` — AI 운영 인프라 (스크립트, 로그, 헬스레지스트리)

## 이유

- 두 경로 모두 현재 실제 사용 중이며 git 추적됨
- `/srv/ai/` 는 존재하지 않아 신규 구성이 필요해 오히려 복잡도 증가
- 에이전트 `allowed_roots`를 두 경로로 제한하면 파일시스템 공격 범위 최소화

### 고려한 대안

| 대안 | 장점 | 단점 | 기각 이유 |
|------|------|------|---------|
| `/srv/ai/` 신설 | 전용 공간 | 실제 코드 없음, 이전 작업 필요 | 오버헤드 대비 이득 없음 |
| `/home/bbw/` 전체 허용 | 단순 | .ssh/.aws 등 민감 경로 노출 | 보안 원칙 위반 |

## 결과

- agent-inventory.json `allowed_roots`에 두 경로 기반으로 정의됨 (P0-8 완료)
- Obsidian 위키 경로: `/home/bbw/obsidian-vault/bbw-wiki/` (에이전트 문서 작업 범위)

## 준수 기준

```bash
# 에이전트가 작업 시 경로 확인
grep "allowed_roots" ~/ai-ops/logs/health/agent-inventory.json
```
