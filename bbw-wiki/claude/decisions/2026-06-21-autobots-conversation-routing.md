---
title: Autobots 대화 라우팅 — 의도 기반 자동 라우팅 + Sticky (눈꽃 단일 오케스트레이터)
date: 2026-06-21
tags: [autobots, routing, orchestration, chat, projects, sticky, decision]
---

# Autobots 대화 라우팅: 의도 기반 자동 라우팅 + Sticky 컨텍스트

상위 기획: [[ai-agent-ops-plan]] §10 · 정체성: [[autobots]]

## 배경
Chat/Projects 화면에서 사용자가 (1) 대화마다 봇 로스터를 수동으로 추가하고, (2) 매 메시지 `@봇이름`으로 호출해야 하며, (3) 같은 봇에게 이어서 작업시킬 때도 재호출해야 정상 진행됐다. 무멘션 시 백엔드는 `roster[0]`만, 프론트는 "로스터 전체 봇이 각각 응답"하는 구조라 부담이 컸다.

codex에 자문한 결과 "눈꽃(전역 오케스트레이터) + 프로젝트/장기 대화용 PM 봇 신설" 2단계 안을 받았으나, 코드 확인 결과 눈꽃은 이미 `role: 관리자/오케스트레이션`으로 정의돼 있어 **별도 PM 봇은 과설계**로 판단.

## 결정
1. **별도 PM 봇 신설하지 않음.** 눈꽃(snow)을 항상 작동하는 라우터/오케스트레이터로 두고, **PM은 봇이 아니라 모드**(Chat=라우팅 모드 / Projects=프로젝트 모드). 프로젝트 상태는 봇 페르소나가 아니라 DB(태스크 카드/스레드)에 둔다.
2. **로스터는 필수 설정 → 선택적 핀(후보 풀 제한)으로 강등.** 비우면 전체 활성 봇이 후보. 하드 삭제하지 않고 검증 인프라는 보존(escape hatch).
3. **의도 기반 자동 라우팅 + Sticky 컨텍스트.** 무멘션 메시지는 라우터가 후보 풀에서 1봇을 자동 선택. `@멘션`은 명시 오버라이드(다중 멘션=멀티봇)로 유지.

## 구조 (3계층)
- **L0 라우터**: 매 메시지 "이번 턴 누가?" 결정. sticky 빠른경로 + 저비용(haiku) 분류.
- **L1 눈꽃**: 단일 위임 / 다단계 계획·취합·승인 게이트.
- **L2 전문봇**: 키엘(기획)·로운(백엔드)·아서(프론트)·해리(검증)·덱스(위키)·리안(검색)·리나(UI/UX).

### 라우팅 우선순위
`forceBotId` → `@멘션(후보 풀 내)` → **자동 라우터** → 폴백(sticky → snow → 풀 첫봇).

- **후보 풀(candidatePool/projectPool)**: 로스터(chat) / project_bot_links(project)가 있으면 제한, 없으면 전체 활성 봇.
- **Sticky**: 직전 턴 담당 봇 = 마지막 assistant 메시지 `bot_id`(신규 컬럼 불필요). 짧은 후속(≤24자)은 LLM 생략하고 유지. 도메인 명확 전환 시만 교체.
- **자동 라우터**: haiku에 봇 목록·역할·sticky·최근 대화를 주고 봇 id 1개만 출력하도록 분류. 협업·계획·애매 시 snow.

## 구현 (기존 인프라 재사용 — DB 스키마 변경 0)
- 신규 `autobots/backend/routes/bot-router.ts`
  - `candidatePool(convId)` / `projectPool(projectId)`, `routeMessage` / `routeProjectMessage`
  - sticky 빠른경로 + `quickClassify`(claude haiku, `-p --no-session-persistence`, stdout 텍스트 회수)
  - 결정은 `event_logs(type='bot_routed')`에 기록(정확도 계측 소스)
- `routes/chat.ts` `resolveBotInfo` async화 + `@멘션`을 후보 풀 전체로 매칭(로스터 비어도 동작). `routes/projects.ts` `resolveProjectBot` 동일 패턴.
- 프론트(`app/chat/page.tsx`, `app/projects/page.tsx`): 무멘션 디스패치를 백엔드 라우팅에 위임(`force_bot_id` 없이 단일 run), 로스터 UI → **"봇 핀(선택)"** 재라벨, 안내문구 상시 표시.
- env 튜닝: `BOT_ROUTER_MODEL`(haiku), `BOT_ROUTER_FOLLOWUP_CHARS`(24), `BOT_ROUTER_TIMEOUT_MS`(25000), `BOT_ROUTER_DEFAULT`(snow).

## 근거 (codex 2-봇 안 대비)
- 봇 1개 추가는 페르소나·런타임 바인딩·profile_memory·학습 경로 부담을 늘린다. 눈꽃이 이미 그 역할.
- "언제 PM을 켜는가"의 모호한 상태전이 문제를 모드로 흡수해 제거.
- 프로젝트 상태를 DB 태스크 카드에 두어야 추적·롤백·재배차 가능([[autobots]] 식별성/학습 경로 보존 제약).
- 눈꽃 리서치(2026-06)의 "하이브리드 라우팅 + 가격보다 태스크 적합도 가중" 방향과 정합.

## 제약 (불변)
- **라우팅 ≠ 실행 인가.** 고위험(sudo·결제·DB스키마)은 자동 라우팅돼도 승인 게이트 유지([[2026-06-21-autobots-sudo-auth-debugging]]).
- 런타임 소진 페일오버(고위험 자동승계 금지, §8) 불변.
- **백엔드 변경은 `docker compose build backend && up -d backend`** (소스가 이미지에 구워짐).

## 검증
- 백엔드 `tsc --noEmit` 통과 + 모듈 런타임 import 확인.
- 프론트 `tsc` + `eslint`(0 errors) + `next build` 통과.

## 백로그
- 레거시 단일 `bot_id` 챗을 핀으로 우대할지(현재는 자동 라우팅 + sticky가 연속성 유지, bot_id는 최종 폴백).
- 프론트 "봇 핀" 영역 접힘/숨김 옵션.
- `bot_routed` 로그 기반 라우팅 정확도 대시보드.
