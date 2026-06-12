---
title: 헤르메스 에이전트 (Hermes Agent)
type: entity
tags: [product, ai-agent, multi-agent, open-source]
created: 2026-06-09
updated: 2026-06-12
sources: [2026-06-09-ai-native-hermes-report, 2026-06-10-free-roaming-agents-comparison, 2026-06-12-hermes-agents, 2026-06-09-hermes-vps-setup-samhottman]
---

## 개요

**Nous Research** 개발 오픈소스 에이전트 플랫폼. 2026년 2월 출시, GitHub 18,800+ stars.
"자유령 에이전트" 계열로 분류 — 메신저(Telegram/Discord 등)를 통해 원격에서 AI 에이전트를 조작하고,
크론잡·스킬·장기 기억으로 자율 성장하는 개인 AI 직원 개념.

단순 채팅 도구가 아닌 **에이전트 운영 플랫폼**: 게이트웨이 + 크론 + 스킬 + MCP 서버 + ACP 프로토콜.

## BBW 설치 현황

| 경로 | 버전 | 상태 |
|---|---|---|
| `/home/bbw/.local/bin/hermes` | v0.16.0 | 정상 (Codex OAuth 로그인) |
| `/opt/hermes/.venv/bin/hermes` | v0.16.0 | 서비스형, dashboard :19119 실행 중 |

**현재 설정**: gpt-5.5 via OpenAI Codex OAuth / docker 터미널 백엔드
**대시보드**: `https://snowball.me.kr:9119/` (Caddy 역방향 프록시, 2026-06-12 외부 접속 확인)
**P0 미완료**: gateway 중복 실행 중 (정리 필요), Telegram 미설정

## Claude Code와의 역할 분리

| 구분 | 헤르메스 | Claude Code |
|---|---|---|
| 비유 | 에이전시 (외주) | 인하우스 (사내) |
| 시간대 | 야간·상시 (크론잡) | 주간 (대화형) |
| 접근 방법 | 텔레그램·대시보드 | 터미널 |
| 특기 | 크론잡·비동기·장기 기억·알림 | 설계·검토·문서화·오케스트레이션 |
| BBW 플랜 | 작업 큐·wrapper 호출·health 갱신 | 위험 판단·사용자 승인·코드 리뷰 |
| 팀명 (김요일) | 린네이티브 | 린 프로젝트 |

## 핵심 기능 5가지

1. **모바일 원격 실행** — Telegram/Discord로 언제 어디서나 에이전트 실행 및 결과 수신
2. **멀티 에이전트 프로필** — 고유 ID의 독립 에이전트 인스턴스 (세션 복제 아님)
3. **크론잡** — 예약 작업 (`hermes cron`), 야간 자율 학습 루프 구현 가능
4. **스킬 시스템** — skills.sh/GitHub/ClawHub에서 설치, 35개+ 스킬로 전문성 부여
5. **자기 진화형 아키텍처** — 작업 중 오류를 마크다운에 기록 → 세션 간 학습 누적

## 자기 진화형 아키텍처

OpenClaw와의 핵심 차이: 헤르메스는 **학습 중심 자기 진화형** 구조를 가진다.
```
작업 수행 → 미스 발생 → 마크다운에 이슈·수정 기록 → 다음 세션 로드 → 반복 방지
```
기록이 쌓일수록 에이전트 전문성 증가. 스킬 35개 로드 시 UX 방법론 전문 에이전트화 사례 있음.

## 에이전트 행동 기준 규칙

CLAUDE.md와 동일 개념으로 에이전트마다 행동 규칙 정의:
```
AGENTS.md / SOUL.md — 에이전트별 페르소나·역할·제약 사전 약속
```
`--ignore-rules` 플래그로 세션별 규칙 무시 가능 (테스트용).

## 모델 교체 가능성

두뇌(LLM)와 플랫폼 분리 설계. BBW 현재: gpt-5.5 via OpenAI Codex OAuth.

지원 프로바이더: OpenAI Codex(OAuth), Claude(API), Gemini(API/OAuth), OpenRouter, xAI Grok, Qwen, DeepSeek 등.
ChatGPT 구독자는 Codex 모델을 **무료 연동** 가능 — OpenClaw는 API 과금만 지원.

## 주요 명령 (빠른 참조)

```bash
hermes                        # 대화형 채팅
hermes --tui                  # 모던 TUI
hermes -z "prompt"            # 원샷 모드 (스크립트/파이프용)
hermes -c                     # 최근 세션 이어서
hermes --worktree             # 병렬 에이전트 (격리 git worktree)

hermes gateway install        # systemd 서비스 설치
hermes gateway start/stop     # 게이트웨이 시작/중지
hermes send "메시지" -t telegram  # LLM 없이 Telegram 알림 전송

hermes cron list/create       # 크론잡 관리
hermes skills browse/install  # 스킬 설치
hermes mcp                    # Hermes를 MCP 서버로 실행

hermes dashboard              # 웹 UI (:9119)
hermes status                 # 전체 상태 확인
hermes doctor                 # 설정·의존성 점검
hermes security               # OSV.dev 공급망 감사
```

## OpenClaw vs 헤르메스 선택 기준

| 상황 | 추천 |
|---|---|
| 하나의 에이전트를 장기 육성·전문화 | 헤르메스 |
| 여러 에이전트를 병렬 대량 처리 | OpenClaw |
| ChatGPT 구독 중 (Codex 무료 연동) | 헤르메스 |
| 보안 우선 | 헤르메스 (보안성 높다는 평가) |

## GitHub 자동 백업

스킬·메모리 변경 시 자동 커밋. 민감한 토큰 값은 자동 제외.

```bash
hermes config set GIT_TOKEN <fine-grained-PAT>
# PAT 권한: 특정 private 레포 → Contents Read/Write
# 이후 에이전트에게 "의미 있는 변경 시마다 GitHub에 커밋해줘" 요청
```

## 폴백 모델 설정

주 모델 장애 시 자동 전환. OpenRouter 무료/저렴 모델 활용 권장.

```bash
hermes fallback add     # 폴백 추가 (OpenRouter → 모델 선택)
hermes fallback list    # 현재 폴백 체인 확인
hermes fallback remove  # 폴백 제거
```

**주의**: 헤르메스는 여러 스킬 동시 호출 시 컨텍스트 윈도우에 올라가므로 폴백 모델도 어느 정도 성능이 필요. 지나치게 저렴한 모델은 멀티 스킬 시 성능 저하.

## 설치 방법

```bash
hermes install          # 공식 사이트 명령어
hermes setup full       # 풀 셋업 (모델·도구·브라우저·검색 전체 대화형 선택)
hermes setup quick      # 빠른 설정
```

## 주요 연결

- [[wiki/concepts/hermes-architecture|Hermes 아키텍처]] — 전체 레이어 구조 상세
- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]]
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]]
- [[wiki/entities/openclaw|OpenClaw]] — 유사 로컬 에이전트, 병렬 처리 특화
- [[wiki/entities/caddy|Caddy]] — dashboard 외부 노출 역방향 프록시
- [[wiki/entities/kimyoil|김요일]] — AI 네이티브 팀 운영 실무 사례

## 출처

- [[wiki/sources/2026-06-12-hermes-agents]] — 실제 설치 직접 조사 (v0.16.0, 전체 명령 체계)
- [[wiki/sources/2026-06-09-hermes-vps-setup-samhottman]] — VPS 풀 셋업 튜토리얼 (GitHub 백업·폴백 모델·Slack 게이트웨이)
- [[wiki/sources/2026-06-09-ai-native-hermes-report]] — AI 네이티브 팀 운영 실무
- [[wiki/sources/2026-06-10-free-roaming-agents-comparison]] — 자유령 에이전트 3종 비교
- [[wiki/sources/2026-06-12-hermes-external-access]] — dashboard 외부 접속 설정
