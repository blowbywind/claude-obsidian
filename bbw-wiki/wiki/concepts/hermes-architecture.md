---
title: Hermes 아키텍처 — 게이트웨이·스킬·크론·MCP 통합 구조
type: concept
tags: [hermes, architecture, gateway, skills, cron, mcp, acp, multi-agent]
created: 2026-06-12
updated: 2026-06-12
sources: [2026-06-12-hermes-agents, 2026-06-09-ai-native-hermes-report, 2026-06-10-free-roaming-agents-comparison]
---

## 정의

Hermes Agent는 단일 AI 어시스턴트가 아닌 **에이전트 운영 플랫폼**이다. 핵심 레이어는:
1. **추론 레이어** — LLM 모델 (교체 가능: OpenAI Codex, Claude, Gemini 등)
2. **실행 레이어** — docker/로컬 터미널 백엔드
3. **통신 레이어** — 게이트웨이(Telegram, Discord, WhatsApp 등)
4. **자동화 레이어** — 크론잡 + hooks
5. **확장 레이어** — 스킬/플러그인/번들
6. **통합 레이어** — MCP 서버/클라이언트, ACP 서버

## 아키텍처 다이어그램

```
사용자 (모바일/데스크톱)
  │
  ├─ Telegram/Discord/Slack/WhatsApp  ──► hermes gateway
  ├─ 브라우저                           ──► hermes dashboard (:19119)
  └─ 터미널                             ──► hermes chat/--tui

                    ▼
┌─────────────────────────────────────┐
│         Hermes Agent Core           │
│                                     │
│  ┌──────────┐  ┌──────────────────┐ │
│  │  Rules   │  │  Context         │ │
│  │ AGENTS.md│  │  Compression     │ │
│  │ SOUL.md  │  │  (50% threshold) │ │
│  └──────────┘  └──────────────────┘ │
│                                     │
│  ┌──────────┐  ┌──────────────────┐ │
│  │  Skills  │  │  Memory          │ │
│  │ (35+)    │  │  (외부 provider) │ │
│  └──────────┘  └──────────────────┘ │
└─────────────────────────────────────┘
  │              │            │
  ▼              ▼            ▼
LLM Provider  Terminal    MCP Servers
(Codex/Claude Backend    (외부 도구)
/Gemini)      (docker)
```

## 추론 레이어 — 모델 교체 가능성

Hermes의 핵심 설계: **두뇌(LLM)와 몸체(에이전트 플랫폼) 분리**.

```yaml
# ~/.hermes/config.yaml
model:
  default: gpt-5.5
  provider: openai-codex
  base_url: https://chatgpt.com/backend-api/codex
```

지원 프로바이더:
- **OpenAI Codex** (OAuth, ChatGPT 구독 무료 연동 가능)
- OpenAI API (sk-* API key)
- Anthropic Claude (API key)
- Gemini / Google (API key 또는 OAuth)
- OpenRouter (다수 모델 접근)
- xAI Grok (OAuth)
- Qwen, DeepSeek, MiniMax, Kimi 등

**폴백 체인**: `hermes fallback add`로 1차 모델 실패 시 자동 대체 설정.

**프록시**: `hermes proxy`로 로컬 OpenAI 호환 엔드포인트 생성 → OAuth 프로바이더를 API key 방식으로 사용하는 도구에 연결 가능.

## 실행 레이어 — Terminal Backend

코드 실행을 위한 격리된 환경:

| 백엔드 | 특징 | BBW 설정 |
|---|---|---|
| `docker` | 격리된 컨테이너, Python+Node 포함 | `nikolaik/python-nodejs:python3.11-nodejs20` |
| `local` | 로컬 셸 직접 실행 | sudo 가능하나 위험 |
| `ssh` | 원격 서버 실행 | 미설정 |

**BBW**: docker 백엔드, sudo 비활성화 (안전 기본값).

## 통신 레이어 — 게이트웨이 아키텍처

Hermes를 **모바일 원격 에이전트**로 만드는 핵심 레이어.

```
외부 메신저
  Telegram ──► hermes gateway ──► Agent Loop ──► 응답
  Discord  ──►                ──► Tool Call  ──► 알림
  WhatsApp ──►                ──► Cron 결과  ──►
  Slack    ──►
  Signal   ──►
  Webhook  ──►
```

**서비스 설치**:
```bash
hermes gateway install    # systemd 서비스로 설치
hermes gateway start      # 백그라운드 시작
```

**스크립트 알림** (`hermes send`): 게이트웨이 서비스 없이도 bot token 기반 플랫폼으로 메시지 전송 가능.
LLM 불필요 — 크론잡·CI 결과 알림에 최적.

```bash
# 크론잡 완료 후 알림
some-script.sh && hermes send "완료: 백업 성공" -t telegram
```

## 자동화 레이어 — 크론잡

에이전트 루프를 정해진 시간에 자동 실행:

```bash
hermes cron create    # 새 크론잡 생성
hermes cron list      # 등록된 잡 목록
hermes cron tick      # 미실행 잡 즉시 실행
```

실무 패턴:
- **야간 학습 루프**: 새벽 3시 리서치 잡 실행 → Obsidian에 결과 저장 → 아침에 확인
- **3시간 자동 커밋**: 작업 중간 스냅샷
- **PR/CI 모니터링**: N분마다 상태 확인

## 확장 레이어 — 스킬 시스템

스킬 = 에이전트 행동 템플릿 (CLAUDE.md의 에이전트 특화 버전).

```
skills.sh / GitHub / ClawHub / 개인 정의
                ↓ hermes skills install
           ~/.hermes/skills/
                ↓ 세션 시작 시
        hermes --skills ux-research,github-auth
```

**실무 사례** (김요일, 카페 UX 프로젝트):
- 35개 스킬 로드 → 정성적 인터뷰 계획서, 페르소나, PRD, 코드 자동 생성
- 스킬이 쌓일수록 에이전트 전문성 증가 (자기 진화형)

**큐레이터**: `hermes curator`로 설치된 스킬의 업데이트·유지보수 자동화.

## 통합 레이어 — MCP & ACP

### Hermes as MCP Server
```bash
hermes mcp    # Hermes가 MCP 서버로 동작
```
Claude Code나 Codex가 Hermes를 MCP 도구로 호출 가능.
→ AI_AGENT_OPS_PLAN Phase 3 Gateway 구성의 대안.

### Hermes as MCP Client
Hermes 세션 안에서 외부 MCP 서버 사용:
```bash
hermes mcp list    # 등록된 MCP 서버 목록
```

### ACP (Agent Client Protocol)
```bash
hermes acp    # ACP 서버로 실행
```
표준화된 에이전트 간 통신. Hermes ↔ 다른 ACP 호환 에이전트 연결.

## 프로필 — 다중 에이전트 격리

각 프로필은 독립적인 에이전트 인스턴스:
```
~/.hermes/
  config.yaml       (기본 프로필)
  profiles/
    codex-worker/   (Codex 전담)
    researcher/     (리서치 전담)
    kanban-board/   (협업 보드)
```

**kanban**: 멀티프로필 협업 보드 — 프로필 간 태스크·링크·댓글 공유.

## 컨텍스트 압축

긴 대화에서 컨텍스트 초과를 자동 관리:
```yaml
context_compression:
  enabled: true
  threshold: 50%        # 컨텍스트 50% 사용 시 압축 시작
  target_ratio: 20%     # 압축 후 20% 수준으로 줄임
  protect_last: 20      # 마지막 20개 메시지 보호
  protect_first: 3      # 시스템 헤드 3개 보호
```

→ 장기 세션(크론잡·야간 루프)에서 메모리 폭발 방지.

## 자기 진화형 아키텍처

Hermes의 핵심 차별점: **학습 기록 → 성장 누적**.

```
작업 수행 → 미스 발생
              ↓
   스스로 마크다운에 이슈·수정 기록
              ↓
   다음 세션에 기록 로드
              ↓
   동일 실수 반복 방지 → 에이전트 성장
```

외부 메모리 (`hermes memory`)를 Vector DB나 Obsidian MCP에 연결하면 세션 간 장기 기억 유지.

## 보안 고려사항

| 위협 | Hermes 대응 | BBW 추가 조치 |
|---|---|---|
| 공급망 | `hermes security` (OSV.dev 감사) | 스킬/플러그인 설치 출처 기록 |
| 위험 명령 | 기본 승인 프롬프트 | `--yolo` 사용 금지 |
| Secrets | Bitwarden 연동 (`hermes secrets`) | `.env` 파일 Git 제외 |
| 파이링 | `hermes pairing` (DM 페어링 코드) | 승인된 사용자만 |

AI_AGENT_OPS_PLAN § 3.2 불가침 원칙: Hermes는 직접 위험 명령 실행 금지. wrapper 통해 위임.

## 관련 개념

- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]] — 헤르메스=에이전시, Claude Code=인하우스 분리
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]] — 크론잡 기반 학습
- [[wiki/concepts/caddy|Caddy]] — hermes dashboard의 역방향 프록시
- [[wiki/concepts/kt-hairpin-nat|KT hairpin NAT]] — 외부 접속 허용 방법

## 관련 엔티티

- [[wiki/entities/hermes-agent|헤르메스 에이전트]]
- [[wiki/entities/openclaw|OpenClaw]] — 유사 플랫폼, 병렬 처리 특화

## 출처

- [[wiki/sources/2026-06-12-hermes-agents]]
- [[wiki/sources/2026-06-09-ai-native-hermes-report]]
- [[wiki/sources/2026-06-10-free-roaming-agents-comparison]]
