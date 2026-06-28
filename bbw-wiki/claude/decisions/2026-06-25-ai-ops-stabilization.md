---
name: 2026-06-25-ai-ops-stabilization
description: ai-ops 안정화 — 봇 회의(로운·아서) 3차 교차검증 + 최종 코드 대조 후 작업 전 플랜 ADR
metadata:
  node_type: decision
  type: project
  status: in-progress
  date: 2026-06-25
---

# ADR: ai-ops 안정화 작업 (Phase 0 크래시·spawn 안전화 / Phase 1 데이터·시크릿 백업)

## 맥락
사용자 지시로 ai-ops 안정화 회의 진행. 회의 참석자는 **봇**(로운=backend codex, 아서=infra codex), 관리·오케스트레이션·검증은 눈꽃. 1차 회의 → 2차 봇 교차검증 → 3차 최종 코드 대조의 3단계로 회의록을 검증했고, 사용자가 눈꽃에게 진행 승인 권한을 위임함.

## 검증 결과 (코드 재대조로 확정)

### CONFIRMED (실재 확인)
| 항목 | 근거 |
|---|---|
| 전역 예외 핸들러 0건 | `unhandledRejection\|uncaughtException` grep 공집합 |
| 주기작업 `.catch` 누락 | `server.ts:220,223` `void ...then()` catch 없음 |
| chat/projects spawn 전역 캡 미적용 | `chat.ts:425/434/440`, `projects.ts:264/271/277` 직접 spawn, `acquireBotSlot()` 호출 0 |
| `acquireBotSlot` 인프라는 존재(미사용) | `watchers/concurrency.ts:10` (cron/learning만 사용) |
| stdin error/EPIPE 미처리 | `chat.ts:446-448`/`projects.ts:283-285` stdin.write/end에 error 리스너 0 |
| DB 백업 로컬 단일 디스크 | `scripts/governance/db-backup.mjs:11` dirname(DB)/backups |
| mTLS 평문 key 워킹트리 상존 | `live-console/certs/*.key`, `client.p12` |

### REFUTED / 정정 (회의록 오류)
| 항목 | 정정 |
|---|---|
| frontend 원격백업 없음 (P0) | REFUTED — `frontend/.git/config:6` origin 존재 → P2 강등(README 문구만 오래됨) |
| frontend CI 전무 (P0) | REFUTED — frontend 자체 CI 존재. 실구멍은 live-console CI 미연결 + 루트 통합게이트 부족 |
| learning 슬롯 영구점유 (P1) | REFUTED(주경로) — `learning-executor.ts:551` finally finalize. 슬롯획득 직후 초기 DB기록 예외경로만 Partial/Medium |
| 0바이트 유령DB 오연결 (P0) | REFUTED — `db/client.ts:4` 절대경로(HOME 고정), cwd 무관 → 잔재청소(P3)만 |
| systemd restart 정책 공백 | PARTIAL — `live-console.service:25 Restart=on-failure` 정의됨. 실이슈는 "미설치/현재 셸 미검증" |

### 봇이 추가 발굴 (회의록 누락)
- [High] `withTransaction` 재진입 가드 동시성 취약 (`db/client.ts:29`, 로운)
- [High] `setInterval` 콜백 `.catch` 누락 → 항목3과 결합 시 5분 주기 크래시 룰렛 (로운)
- [P0] `/etc/autobots/backend.env` 단일 평문+백업부재 (아서)
- [Low] `db/backups/` 0바이트 WAL/SHM 잔존 (아서)

## 결론
**진짜 최우선은 데이터 백업이 아니라 프로세스 크래시·spawn 폭주 연쇄.** 비동기 에러 1건이 컨테이너 전체를 내리는 구조가 실재.

## 결정 (작업 전 플랜)

### Phase 0 — 크래시·spawn 안전화 (P0, 단일 묶음) — 담당 로운
- 0-1. 공통 spawn 안전 헬퍼 신설 `watchers/spawn-guard.ts`: `acquireBotSlot` 래핑 + 단일 release(close/error 1회) + `proc.stdin` error 리스너(EPIPE 흡수) + 타임아웃 통합. chat/projects attemptRuntime 적용. 슬롯 미가용 시 503/재시도.
- 0-2. 전역 예외 핸들러 `server.ts`: `unhandledRejection`/`uncaughtException` 로깅+SSE broadcast, uncaught는 즉시 exit 금지(Docker restart 위임, 워처 보존).
- 0-3. 주기작업 `.catch` `server.ts:220,223` setInterval 콜백 catch 부착.
- 검증: `tsc --noEmit` + 기존 테스트 + spawn 캡 단위테스트 1건. 게이트: 눈꽃 검토 → (코드변경) code-reviewer → evaluator-strict.

### Phase 1 — 데이터/시크릿 오프사이트 백업 (P0) — 담당 아서
**인프라·보안·되돌리기 어려운 작업 → 실행 직전 사용자 재확인 필수**
- 1-1. db-backup 오프호스트 타깃(`DB_BACKUP_REMOTE`) 추가, 로컬+원격 이중화.
- 1-2. mTLS 키·운영 env 백업 대상 포함, 키 워킹트리 밖(`/etc/live-console/certs`) 이전 검토.
- 1-3. live-console 현재 셸 미설치 ↔ 위키 "배포완료" 불일치 → 호스트 실측 후 systemd 설치/검증.

### Phase 2 — 위생/회귀 (P1~P2, 저위험)
루트 CI에 live-console typecheck/build 추가 / tmp 233MB TTL 정리 / logrotate 대상 확장 / README 정정 / 0바이트 DB 잔재 청소 / learning 초기DB기록 예외경로 try/finally 보강.

## 진행 게이트
- Phase 0: 승인 위임 받음 → 로운 착수, 눈꽃 검증.
- Phase 1: 호스트 실측 + 키 이동·systemd 등 파괴적 작업은 실행 직전 재확인.
- 관련: [[effective-improvement-workflow]], [[orchestration-directives]], [[live-console-caddy-mtls-deploy]], [[autobots-hardening-backlog]]
</content>
</invoke>
