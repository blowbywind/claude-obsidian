---
title: "firecrawl — 웹 스크레이퍼 API (외부 프로젝트)"
id: "P-05"
status: "유지보수"
phase: "Phase 유지보수"
stack: [Node.js, pnpm, TypeScript, Jest]
created: 2026-06-13
updated: 2026-06-11
summary: "firecrawl 오픈소스 프로젝트 유지보수 중—TypeScript/pnpm 모노레포, Codex 기여·PR·CI 필수, pnpm harness jest로만 테스트"
---

## 현재 상태

- **Phase**: 유지보수
- **진행 상황**: 외부 오픈소스 프로젝트 유지보수. 로컬 기여·패치 관리.

## 서버 / 인프라

| 항목 | 값 |
|------|-----|
| 구조 | 모노레포 |
| API | `apps/api` |
| SDK | `apps/*-sdk` |

## 스택

- 언어: TypeScript / Node.js
- 패키지 관리: pnpm
- 테스트: pnpm harness jest (snips — E2E 우선)

## 에이전트 허용 범위

| 에이전트 | 허용 | 금지 |
|---------|------|------|
| Claude Code | 설계·검토·문서화 | |
| Codex | `/home/bbw/projects/firecrawl/` 수정 | 임의 push |
| agy | 리서치만 | 코드 수정 불가 |

## Dev Gate

```bash
cd /home/bbw/projects/firecrawl
pnpm install

# 테스트 실행 (harness 필수 — 직접 pnpm start 금지)
pnpm harness jest <test-file>
```

## 위험 구역

- **PR/CI 필수**: 변경 후 반드시 PR 열고 CI 통과 확인 (§4.3 원칙8)
- `pnpm start` 직접 실행 금지 → `pnpm harness` 사용
- fire-engine 의존 테스트: `TEST_SUITE_SELF_HOSTED` 환경변수 확인

## 자주 쓰는 명령

```bash
# E2E 테스트
pnpm harness jest apps/api/src/__tests__/snips/<test>.test.ts

# PR 오픈 전 확인
pnpm harness jest --testPathPattern=<pattern>
```

## 최근 작업

- 유지보수 모드

## 다음 작업

- [ ] CI 상태 확인

<!-- night-learn-status -->
> 자동 상태 요약 (2026-06-15): 
