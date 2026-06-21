---
title: ai-ops 플랫폼 방향·유지보수 전략 (논의 진행중)
type: decision
status: discussing
created: 2026-06-21
updated: 2026-06-21
tags: [ai-ops, autobots, platform, maintainability, strategy, adr-draft]
---

# ai-ops 플랫폼 방향·유지보수 전략 (논의 로그)

> **상태: DISCUSSING — 결론 미확정. 사용자 승인 전까지 구현 금지.**
> 이 노트는 결론 도달 시 ADR로 승격한다. 대화가 진행될 때마다 §로그에 계속 추가한다.

## 0. 게이트 규칙 (사용자 지시 2026-06-21)
- 이 논의는 Obsidian(이 노트) + 로컬 메모리에 **계속 기록**한다.
- **최종 결론이 난 뒤에만**, 사용자 **승인 후** 실제 작업(구현)을 시작한다.
- 그 전까지는 진단·논의·기록만. 코드 변경 금지.

## 1. 발단
사용자 질문: "ai-ops를 쓰는 것 vs Claude Code / Codex / Antigravity를 각각 개별로 쓰는 것"의 장단점과,
ai-ops가 가야 할 방향이 맞는지·계속 쓰는 게 옳은지 깊은 판단 요청.

## 2. ai-ops 현황 (실측, 2026-06-21)
- 자작 플랫폼 ~22k LOC (backend 10.4k + frontend 11.6k).
- Docker + Caddy 24/7 배포. 봇 9개를 3개 런타임에 매핑(Codex gpt-5.5 / Claude Code claude-sonnet-4-6 / Antigravity gemini-3.5-flash).
- 7개 실제 프로젝트 관리, Obsidian vault 737노트·session-log 21k줄.
- cron·학습루프·파이프라인·승인 게이트·sudo executor 보유.
- 알려진 약점: hermes WebSocket 장기 DEGRADED, run-gemini ~69h unavailable.

## 3. 1차 판단 (claude 의견)
- ai-ops를 "개발 작업 시키는 엔진"으로 쓰는 건 ROI 약함. 핸즈온 코딩은 도구 직접 사용이 더 강함.
- **가장 큰 전략 위험**: 프런티어 도구(특히 Claude Code)가 subagent·hooks·skills·background task·scheduling·MCP·plan mode 등 오케스트레이션을 빠르게 내재화 → 자작 레이어의 차별점이 릴리스마다 침식.
- ai-ops가 진짜 못 뺏기는 가치 2가지: (1) 3개 공급자가 공유하는 단일 제2의 두뇌, (2) 무인 자율 루틴 + 거버넌스(승인/sudo/failover).
- A(생산성 도구) vs B(플랫폼 구축 자체가 목표)로 분기. 중간지대(플랫폼을 생산성 도구인 척 운영하며 인프라 소방에 노력 소모)가 가장 위험.

## 4. 사용자 결정
**B 경로 채택**: 플랫폼 구축 자체를 목표로, "더 완벽하고 잘 만들고 유지보수를 잘" 하는 방향으로 진행.

## 5. 유지보수 건강도 진단 (실측, 2026-06-21)
- **테스트 사실상 없음**: backend 10.4k LOC에 테스트 3개(전부 sudo 관련). `package.json`에 `test` 스크립트 없음.
- **CI 게이트 없음**: `.github/workflows`에 webhook 트리거 1개뿐(typecheck/lint/test 관문 없음).
- **`tsconfig strict: false`**: null 안전성·implicit any 무방비. (단 현재 `tsc --noEmit` 통과.)
- **관측성 빈약**: 구조화 로그(`fastify.log`) 1회 · `console.*` 2회 · try/catch 193개 제각각.
- **god 파일**: projects.ts 685 / chat.ts 672 / learning-executor.ts 621 / stream-engine.ts 604줄.
- **frontend 소멸 리스크**: `autobots/frontend/` 전체가 부모 .gitignore에 의해 무시 + 별도 레포 + 원격 백업 없음 → `rm` 한 번에 11.6k LOC 소멸 가능. (관련: 로컬 메모리 rollback-prevention)
- 연결고리: 최근 커밋이 회귀 소방(레이스·SSE·sudo·SPA404·pnpm)으로 가득한 건 **안전망 부재**의 자연스러운 결과.

## 6. claude의 우선순위 의견 (논의용, 미확정)
방향: 기능 확장이 아니라 **표면 축소 + 코어 심화**. 순서 중요.
1. (즉시/저비용·고가치) frontend 백업·원격 확보 — 소멸 리스크 제거.
2. (안전망 1단계) 회귀 다발 경로부터 통합테스트 + CI 게이트(typecheck/lint/test).
3. (관측성) 구조화 로깅 + 헬스 일원화 → 장기 DEGRADED 즉시 알림.
4. (strict 점진 도입) 디렉터리별 단계 적용.
5. (god 파일 분해) **반드시 2번 이후**. 테스트 없이 분해 = 회귀 위험.

## 7. 미해결 쟁점 (사용자 답변 대기)
- Q1. "완벽"의 정의: 신뢰성(안 깨짐) / 기능 완성도 / 코드 품질 중 무엇 우선?
- Q2. 실제로 가장 자주 괴롭히는 곳: SSE? 봇 라우팅? 두뇌 read/write 신뢰성? hermes?
- Q3. ai-ops를 봇이 자기수정(self-modify)하나? → 그렇다면 안전망은 필수 전제.

## 8. 대화 로그 (시간순, 계속 추가)
- 2026-06-21: 발단 질문 → 1차 판단(§3) 제시 → 사용자 B 경로 결정(§4) → 유지보수 진단(§5) → claude 우선순위 의견(§6) + 쟁점 3개(§7) 제시.
- 2026-06-21: 사용자 "구현 말고 의견만 / 기록 계속 / 결론 후 승인 시 작업" 지시 → 이 노트 + 로컬 메모리 포인터 생성, 게이트 규칙(§0) 확립.
