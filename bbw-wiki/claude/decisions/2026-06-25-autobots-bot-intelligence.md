---
date: 2026-06-25
project: ai-ops (autobots)
status: 승인 — 구현 미착수 (집에서 이어감)
tags: [ai-ops, autobots, bots, agents, self-learning, sudo, passthrough, adr]
summary: "9봇 유지 및 agent 실시간 배선(B-full), Live·Chat·Projects 3경로 분리, 독립 복구 콘솔 추출, 학습루프 강화를 통해 봇의 전문성과 자가진화 체계 구축."
---

# autobots 봇 지능화 + 3경로 분리 + Live 독립 콘솔

날짜: 2026-06-25 / 프로젝트: ai-ops / 상태: 플랜 승인, 구현 미착수
관련: [[ai-ops-build-plan]] (Phase 4'·Phase 7 재작성), [[phase7-bot-fleet-gate]], [[agents-skills-catalog]], [[bot-autonomous-sudo]], [[platform-direction-discussion]]

## 배경
빌드플랜 옛 Phase 7은 "봇 함대·자율 dev-프록시·sudo executor 폐기/축소"였다(북극성: Phase 4 패스스루가 대화형을 대체하면 봇 불필요). 사용자와 재논의(2026-06-25, 게이트 절차 [[phase7-bot-fleet-gate]])에서 이 전제가 사용자 의도와 정면 충돌함이 드러나 전면 재작성했다.

**사용자 봇 철학(확정)**: 봇 = 기능별 전문성을 가진 "담당 직원". 사용자가 모든 agent의 기능·사용성을 기억·관리하는 건 비현실적 → 봇이 자기 역할에 맞게 agent를 **구성·관리**해 전문적 결과를 낸다. 자가학습은 사용자와 협업하며 의도를 더 잘 파악하기 위한 필수 기능.

## 결정 1: 9봇 전원 유지 (흡수/폐기 철회)
옛 "9봇→agent 흡수, 페르소나 폐기" 폐기. 봇=직원 모델이 사용자 핵심 의도. agent로 직접 대체하면 사용자가 agent 관리 부담을 떠안음 → 봇이 그 관리 계층.

## 결정 2: 봇↔agent 런타임 배선 = B-full ([[agents-skills-catalog]] "미배선" 번복)
2026-06-25 초 "agent 카탈로그 런타임 미배선(UI용, 토큰절약)" 결정을 **번복**. 봇이 실제로 agent를 호출·관리하게 배선.
- **구현방식 = B 기본 + 고부하 C**. A(정적주입=상시토큰) 거부.
  - B = DB 9 agent를 실제 `autobots/.claude/agents/*.md`로 실체화 + 봇 spawn에 경량 위임 주입(전담 agent명+1줄) + 네이티브 `Task`로 호출(전체 컨텍스트는 sub-context에만=지연로딩, 평상시 토큰≈0).
  - C = 고부하 병렬만 봇이 Task 다중 팬아웃(별도 기제 아님).
- **"구성·관리" = B-full**: 선택·호출 + 자가학습이 새 agent/skill 후보 제안→**사용자 승인 시** 로스터(.claude/agents+bot_agent_links) 편입. 봇이 시간이 지나며 전문성을 키움. 7-D는 승인 게이트 필수.
- 토큰 우려(미배선 사유) 해소: 지연로딩이라 평상시 비용 거의 0.
- 기검증: `Task`가 이미 CLAUDE_ALLOWED_TOOLS(stream-engine.ts:380), 보고 로직 존재(:761), capability_suggestions 큐가 이미 7-D 제안경로(learning-executor.ts:303). 빠진 것=9 agent의 .md 파일 + 경량 주입 + 승인분 실체화 배선.

## 결정 3: 3경로 목적 분리 (자율 dev-프록시 "폐기" 해소)
옛 "자율 dev-프록시 폐기"는 (가)one-shot 실행모드와 (나)봇 자율성을 혼동했다. (나)는 이제 핵심.
- **Live** = autobots 장애 복구/관리용 독립 콘솔(분리, 결정4).
- **Chat** = autobots 관리·Obsidian 관리를 사용자가 봇 도움으로 직접. 현행 one-shot `-p`+대화이력 유지(짧은 이산 턴=충분), B-full 위임 적용. 봇=사용자가 운전하는 보조자.
- **Projects** = 봇들이 사용자 명령으로 협업해 완벽한 결과물. 엔진=B-full(snow 리드 위임)+C(팬아웃)+`pipeline-executor.ts`+Phase 5 게이트. 봇=자율 협업 실행자.

## 결정 4: Live(패스스루) → autobots에서 추출 → 독립 복구 콘솔
검증: 현 Live(`session-manager.ts`)는 autobots DB(sessions/chat_messages)+stream-engine+botSpawnEnv 의존 → autobots 다운 시 Live도 죽음 → 복구 콘솔 불가. **실증**: snow의 `docker restart autobots_backend` = status=error(자기 실행중 백엔드를 자기가 재시작=프로세스 사망).
- 채택: 코어(persistent claude spawn+stream-json stdin+SSE+delta파싱) 추출 → 독립 빌드. autobots 자원 비의존, 자체 최소상태. 별도 호스트 systemd(autobots docker 아님)+별도 Caddy 라우트+독립 강인증. 호스트 셸 직접 접근(LLM/MODEL/MODE 선택, codex/agy 패스스루 귀속).
- ⚠️보안: 웹 노출+호스트 셸 = 웹 너머 root 셸 → 인증이 autobots 독립이면서 강해야 함(설계 최우선).

## 결정 5: sudo executor = 폐기 아닌 이원화 유지
검증: 실사용 sudo_jobs 29건(done24, apt-get/chown/docker). 활발히 쓰임 → "폐기" 무효. 복구용 in-band는 구조적 실패(결정4 실증).
- **in-band executor 현행 유지 + 자동허용 4종 유지**(봇 자율작업). 정책 SSOT sudo-policy.ts·시크릿경계·네트워크출처 승인게이트·테스트47 유지.
- **단 autobots 자기생명주기 명령(docker restart autobots_backend·systemctl restart autobots)은 in-band 제외** → Phase 4' 독립 콘솔로 이관(out-of-band, 사람 게이트).
- 시크릿 경계 = "단순화"가 아닌 **이원화**: in-band(정책게이트+봇 자가승인차단, 봇 운전) / out-of-band(사람게이트, 사용자 운전, 더 직접적 호스트접근).

## 결정 6: 학습루프 유지+연결+계측, 보고형 cron 제거
검증: 학습 매일 가동(9봇), 3분류 안전게이팅(저위험 자동+TTL / 고위험 항상 승인 / 신규 도구 후보→capability_suggestions 승인큐). 인사이트 품질 양호.
- 학습루프 **유지·연결**(자가진화 핵심, 7-D로 로스터 큐레이션 배선). "SLO 기여만 유지(솎기)" 전제 폐기 → 기준=봇 지능화 기여.
- 학습 빈도 현행(매일) 유지 + **Phase 1 SLO에 학습 토큰 계측**해 비악화 모니터(솎기보다 측정).
- 정비 cron 6종 유지. **보고형 agent cron 3종 제거**(dex-session-log·weekly-report·codex-experiment-log = 사용자 안 읽음). dex-heartbeat→script.

## 구현 순서 (승인)
7-A/B/C(봇 지능화 코어, chat·projects 공통혜택) → 7-D(로스터 큐레이션) → Phase 4'(독립 콘솔, 보안설계 선행) → 7-E/F. 추천 착수점=7-A. 각 phase는 code-reviewer→evaluator-strict 게이트.

## 상태
플랜 승인 완료, **구현 미착수**. 사용자가 집에서 이어감. 핸드오프 [[work-in-progress]].
