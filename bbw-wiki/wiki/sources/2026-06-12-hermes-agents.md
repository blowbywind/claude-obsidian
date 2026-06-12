---
title: Hermes Agent v0.16.0 — 실제 설치·명령 체계·BBW 운용 현황
type: source
tags: [hermes, ai-agent, multi-agent, gateway, cron, skills, mcp, acp, openai-codex]
created: 2026-06-12
updated: 2026-06-12
origin: /home/bbw/.local/bin/hermes (로컬 설치 직접 조사)
author: bbw (hermes --help, hermes status, hermes config 출력 기반)
date_published: 2026-06-12
---

## 요약

BBW 서버에 설치된 Hermes Agent v0.16.0의 전체 명령 체계·설정·운용 현황을 직접 조사한 기록.
단순한 채팅 도구가 아니라 **게이트웨이 + 크론 + 스킬 시스템 + MCP 서버 + ACP 프로토콜**을 갖춘
멀티에이전트 운영 플랫폼이다. 현재 BBW 환경에서는 OpenAI Codex OAuth로 gpt-5.5 모델을 사용하며,
docker 터미널 백엔드로 코드 실행, 대시보드는 19119 포트에서 운용 중이다.

## 핵심 주장

- Hermes는 채팅 UI가 아니라 **에이전트 런타임 플랫폼** — 스크립팅·크론·게이트웨이·MCP 서버 역할까지 담당
- `hermes send`로 게이트웨이 서비스 없이도 Telegram/Discord/Slack에 메시지 전송 가능 (LLM 불필요)
- `hermes --oneshot`(`-z`) 플래그로 셸 스크립트에서 에이전트 응답을 파이프로 받을 수 있음
- `hermes --worktree`로 병렬 에이전트가 각자 독립된 git worktree에서 작업 가능
- `hermes mcp`로 Hermes 자체가 MCP 서버가 됨 — Claude Code나 Codex에서 Hermes를 MCP로 호출 가능
- `hermes acp`로 ACP(Agent Client Protocol) 서버로 실행 — 표준화된 에이전트 간 통신

## 설치 현황 (BBW 서버)

| 경로 | 버전 | 상태 | 비고 |
|---|---|---|---|
| `/home/bbw/.local/bin/hermes` | v0.16.0 | 정상 | 사용자 설치, Codex OAuth 로그인 완료 |
| `/opt/hermes/.venv/bin/hermes` | v0.16.0 | 버전 확인 실패 | 서비스형, dashboard 19119 실행 중 |

현재 AI_AGENT_OPS_PLAN.md 기준 **중복 gateway 정리 필요**(P0).
active profile: `/opt/hermes` dashboard + `/opt/hermes` gateway 1세트를 권장.

## 현재 설정 (`hermes status` 기준)

```yaml
Model:    gpt-5.5
Provider: OpenAI Codex (OAuth 로그인 완료)
          auth refreshed: 2026-06-11 01:19:55 KST

Terminal Backend:
  type:   docker
  image:  nikolaik/python-nodejs:python3.11-nodejs20 (코드실행)
          python:3.11-slim (기본)
  sudo:   disabled

Context Compression:
  threshold:      50% (context 절반 소모 시 압축)
  target ratio:   20% (압축 후 유지 비율)
  protect last:   20 messages
  protect first:  3 messages

Max turns: 150

Messaging Platforms:
  Telegram: not configured (미설정)
```

## 전체 명령 체계

### 세션 및 채팅

| 명령 | 설명 |
|---|---|
| `hermes` | 대화형 채팅 (classic REPL) |
| `hermes --tui` | 모던 TUI 인터페이스 |
| `hermes -z "prompt"` | 원샷 모드 — 응답 텍스트만 stdout 출력 (스크립트/파이프용) |
| `hermes -c` | 최근 세션 이어서 |
| `hermes -c "이름"` | 이름으로 세션 재개 |
| `hermes -r <id>` | 세션 ID로 재개 |
| `hermes --worktree` | 독립 git worktree에서 실행 (병렬 에이전트) |
| `hermes --yolo` | 위험 명령 승인 자동 우회 (비권장) |
| `hermes --skills s1,s2` | 세션에 특정 스킬 사전 로드 |

### 게이트웨이 (모바일 원격 접속 핵심)

```bash
hermes gateway run        # 포그라운드 실행 (WSL/Docker/Termux 권장)
hermes gateway start      # systemd/launchd 백그라운드 서비스 시작
hermes gateway stop       # 서비스 중지
hermes gateway status     # 상태 확인
hermes gateway install    # systemd/launchd 서비스 설치
hermes gateway setup      # Telegram/Discord/WhatsApp 등 설정
hermes gateway list       # 프로필별 게이트웨이 상태 목록
```

지원 플랫폼: Telegram, Discord, WhatsApp, Weixin, Slack, Signal

### 메시지 전송 (LLM 없이)

```bash
# Telegram으로 단순 텍스트 전송 (게이트웨이 서비스 불필요)
hermes send "배포 완료" -t telegram

# 파일 내용 전송
hermes send -f /tmp/report.md -t telegram

# stdin 파이프
cat result.txt | hermes send -t telegram

# 특정 채널/채팅 지정
hermes send "alert" -t discord:#ops
hermes send "완료" -t telegram:-1001234567890:17585
```

크론잡·CI에서 알림 전송에 사용. **LLM, 에이전트 루프, 게이트웨이 서비스 미필요**.

### 크론잡 관리

```bash
hermes cron list          # 등록된 잡 목록
hermes cron create        # 새 잡 생성
hermes cron edit <job>    # 잡 수정
hermes cron pause <job>   # 일시 중지
hermes cron resume <job>  # 재개
hermes cron run <job>     # 즉시 실행 (스케줄러 다음 틱에)
hermes cron tick          # 미실행 잡 한 번 실행
hermes cron status        # 스케줄러 실행 여부 확인
hermes cron remove <job>  # 잡 삭제
```

### 스킬 시스템

```bash
hermes skills browse        # 등록된 전체 스킬 탐색
hermes skills search <kw>   # 스킬 검색
hermes skills install <sk>  # 스킬 설치
hermes skills list          # 설치된 스킬 목록
hermes skills inspect <sk>  # 설치 전 미리보기
hermes skills update        # 스킬 업데이트
hermes skills uninstall <sk># 스킬 제거
hermes skills audit         # 설치된 허브 스킬 재스캔
```

스킬 소스: skills.sh, GitHub, ClawHub, 기타 레지스트리
(실무 사례: UX 방법론, 심리학 이론 등 35개 스킬 로드)

### 플러그인 & 번들

```bash
hermes plugins install/update/remove/list
hermes bundles create/list    # 여러 스킬을 하나의 별칭으로 묶기
hermes curator status/run/pause/pin  # 백그라운드 스킬 유지 관리 데몬
```

### MCP 통합

```bash
hermes mcp                    # Hermes를 MCP 서버로 실행
hermes mcp list               # 등록된 MCP 서버 목록
hermes mcp add/remove         # MCP 서버 추가/제거
```

**Hermes 자체가 MCP 서버**가 될 수 있음 → Claude Code나 Codex가 Hermes를 MCP 클라이언트로 호출 가능.

### ACP (Agent Client Protocol)

```bash
hermes acp                    # ACP 서버로 실행
```

표준화된 에이전트 간 통신 프로토콜. Claude Code Agent Teams(Session Send)와 유사 목적.

### 프로필 (다중 에이전트 격리)

```bash
hermes profile list           # 프로필 목록
hermes profile create <name>  # 새 프로필 생성
hermes profile switch <name>  # 프로필 전환
```

각 프로필은 독립된 config, memory, 게이트웨이 설정 유지.
`kanban` 명령으로 멀티프로필 협업 보드(태스크, 링크, 댓글) 관리.

### 메모리 및 세션

```bash
hermes memory                 # 외부 메모리 프로바이더 설정
hermes sessions list/browse/rename/export/prune/delete
hermes checkpoints list/prune/clear
```

### 보안 및 유지보수

```bash
hermes security               # OSV.dev 기반 공급망 감사 (venv, 플러그인, MCP 서버)
hermes secrets                # Bitwarden Secrets Manager 연동
hermes doctor                 # 설정 및 의존성 점검
hermes dump                   # 지원/디버그용 요약 덤프
hermes backup/import          # 백업 및 복원
hermes logs -f                # 로그 실시간 팔로우
hermes prompt-size            # 시스템 프롬프트 바이트 분석
```

### 모델 관리

```bash
hermes model                  # 기본 모델 선택 (interactive picker)
hermes fallback list/add/remove # 폴백 프로바이더 체인 관리
hermes proxy                  # 로컬 OpenAI 호환 프록시 (OAuth → API)
hermes portal                 # Nous Portal (로그인, 모델 선택, Tool Gateway)
hermes auth add/list/remove   # 풀링된 자격증명 관리
```

### 대시보드 및 UI

```bash
hermes dashboard              # 웹 UI 대시보드 시작 (기본 포트 9119)
hermes dashboard --stop       # 대시보드 중지
hermes dashboard --status     # 실행 중인 대시보드 목록
hermes --tui                  # 터미널 TUI
hermes desktop                # 네이티브 데스크톱 앱 빌드 및 실행 (macOS)
```

## BBW 아키텍처에서의 역할

AI_AGENT_OPS_PLAN.md 기준:

| 역할 | 상세 |
|---|---|
| 작업 큐 감시 | `00-inbox/requests/` 폴더 모니터링 후 작업 카드 처리 |
| wrapper 호출 | `run-codex`, `run-claude`, `run-gemini` wrapper 위임 |
| health registry 갱신 | `agent-status.json`, `agent-inventory.json` 업데이트 |
| 반복 작업 스케줄링 | `hermes cron`으로 야간 루틴, 3시간마다 자동 커밋 등 |
| 알림 전송 | `hermes send`로 Telegram 결과 보고 |

**불가침 원칙** (AI_AGENT_OPS_PLAN § 3.2):
- Hermes는 직접 위험 명령 실행 금지
- 작업 카드 + wrapper를 통해 위임
- High/Critical 작업은 `require-approval` 후 대기

## BBW P0 미완료 사항

| 항목 | 현황 |
|---|---|
| gateway 중복 실행 | `/home/bbw/.hermes` gateway + `/opt/hermes` gateway 2개 동시 실행 중 |
| Telegram 설정 | not configured |
| `hermes send` 테스트 | 미검증 |
| `hermes cron` 잡 | 미설정 |

## 연결된 개념

- [[wiki/concepts/hermes-architecture|Hermes 아키텍처]]
- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]]
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]]

## 연결된 엔티티

- [[wiki/entities/hermes-agent|헤르메스 에이전트]]

## 출처

- 로컬 설치 직접 조사: `hermes --help`, `hermes status`, `hermes config`, `hermes gateway --help`, `hermes cron --help`, `hermes skills --help`, `hermes send --help`
- `/home/bbw/AI_AGENT_OPS_PLAN.md` — BBW 운용 계획 v2
- [[wiki/sources/2026-06-09-ai-native-hermes-report]]
- [[wiki/sources/2026-06-10-free-roaming-agents-comparison]]
