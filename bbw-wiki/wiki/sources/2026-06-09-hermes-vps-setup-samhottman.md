---
title: "왕초보를 위한 24/7 돌아가는 Hermes Agent — 전체 설정 튜토리얼"
type: source
tags: [hermes, vps, hostinger, slack, github-backup, fallback, tutorial]
created: 2026-06-12
updated: 2026-06-12
origin: https://youtu.be/oOEpQAd6HEI
author: 샘 호트만 (AI 엔지니어의 시선)
date_published: 2026-06-09
summary: "샘 호트만의 Hostinger VPS 위 Hermes Agent 설치 튜토리얼 — VPS 선택, Docker 배포, 프로필·SOUL 설정, Slack 게이트웨이, GitHub 백업, OpenRouter 폴백 모델까지"
summary: "샘 호트만이 Hostinger KVM2 VPS에 Hermes Agent를 원클릭 Docker 배포로 설치하고, 프로필·SOUL·Slack 게이트웨이·GitHub 자동백업·OpenRouter 폴백 모델까지 단계별로 안"
---

## 요약

샘 호트만이 Hostinger VPS 위에 Hermes Agent를 처음부터 끝까지 설치하는 전 과정을 담은 실습 튜토리얼. VPS 선택 기준, 원클릭 Docker 배포, 풀 셋업, 프로필·SOUL 구성, Slack 게이트웨이, GitHub 자동 백업, OpenRouter 폴백 모델까지 단계별로 커버한다.

## 핵심 주장

### 1. VPS vs 로컬 PC 선택 기준

| 상황 | 권장 |
|------|------|
| 24시간 에이전트, 자동화 테스트 | **VPS** (Hostinger ~₩13,000/월) |
| 카카오톡 자동화, 시스템 트레이딩 | **로컬 PC** (기기 직접 접근 필요) |
| 대규모 자동화 | 로컬 Mini PC |

- Hostinger KVM2: 헤르메스 + 오픈 클로드 동시 운용 가능
- 서버 위치: **말레이시아** (한국 기준 최저 레이턴시)
- 내 PC를 꺼도 에이전트가 돌아가는게 VPS의 핵심 장점

### 2. VPS 설치 순서 (Hostinger)

```
1. Hostinger 전용 페이지 → KVM2 선택 → 쿠폰 코드 적용
2. 서버 위치: 말레이시아
3. OS: Ubuntu + Hermes Agent (원클릭 선택)
4. 루트 비밀번호 설정 (분실 금지)
5. 5~10분 대기 → VPS Board 진입
6. Docker Manager 설치 → Compose → One-Click Deploy → Hermes Agent 선택
7. 어드민 유저네임/패스워드 입력 → Deploy
```

### 3. Hermes 풀 셋업 명령어 시퀀스

```bash
hermes setup full
# → 모델 프로바이더: OpenAI Codex (메인)
# → 폴백 프로바이더: OpenRouter
# → Codex OAuth 링크 인증
# → 모델: 최신 모델 선택
# → 터미널: keep current local
# → 도구: 기본 체크 항목 모두 엔터 (웬만하면 전부 유용)
# → 웹 브라우저: 로컬 헤드리스 Chromium (API 키 불필요)
# → 이미지 모델: Codex
# → 검색: Brave Search (API 키 필요)
```

### 4. 프로필 생성과 SOUL 구조

```bash
hermes profile create clone <캐릭터이름>   # 프로필 폴더 + .env + SOUL.md 생성
hermes profile list                         # 프로필 목록 확인
hermes profile use <캐릭터이름>             # 프로필 활성화
```

**SOUL.md 구조** (Hermes 공식 권장):
```markdown
## 정체성
## 목소리 & 소통 스타일
## 피해야 할 것들
## 기술적 지침 (선택)
```

- SOUL.md는 Slack에서 에이전트에게 직접 수정 요청 가능
- 예: "미카사 프로필의 SOUL.md를 이메일 어시스턴트용으로 수정해줘"
  - `write every [response] in your user's voice, not your own`
  - `use language matching the context` (한/영 혼합 대응)

### 5. Slack 게이트웨이 연결

**사전 준비 — 4가지 필수 정보:**

| 항목 | 위치 | 비고 |
|------|------|------|
| 앱 토큰 (`xapp-` 시작) | api.slack.com → Token Scopes → Generate → connections:write | 한 번만 표시 |
| 봇 토큰 (`xoxb-` 시작) | Install App → Install to Workspace | 한 번만 표시 |
| 나의 멤버 아이디 (`U` 시작) | Slack → 프로필 → 점점점 → 멤버 ID 복사 | allowed user |
| 채널 아이디 (`C` 시작) | 채널 → 채널 세부 정보 | 봇이 활동할 채널 |

**연결 순서:**

```bash
# 1. Slack manifest 파일 생성
hermes slack manifest --write
# → 해당 프로필 경로에 slack-manifest.json 생성

# 2. api.slack.com → From a manifest → 내용 붙여넣기 → 봇 생성
# 3. Slack 채널에 봇 초대: /invite @봇이름

# 4. 게이트웨이 설정
hermes setup gateway
# → Slack 선택 → 봇 토큰 → 앱 토큰 → 허용 유저 ID → 홈 채널 ID

# 5. 게이트웨이 실행
hermes gateway 1

# 트러블슈팅: Docker 이미지 에러 발생 시
# → 에러 복사 → hermes 터미널에 붙여넣어 자체 해결 요청
# → 또는 게이트웨이 전용 트러블슈팅 프롬프트 활용 (매뉴얼 참조)
```

### 6. GitHub 자동 백업 전략

**목적**: 스킬·메모리가 변경될 때마다 GitHub에 자동 커밋 (민감 정보 자동 제외)

```bash
# 1. GitHub Private 레포지토리 생성 (Public 금지)

# 2. Fine-grained Personal Access Token 발급
# Settings → Developer settings → Fine-grained tokens → Generate new token
# → Repository access: 해당 레포만 선택
# → Permissions: Repository contents → Read and Write

# 3. 토큰을 Hermes에 등록
hermes config set GIT_TOKEN <토큰값>

# 4. 자동 백업 루틴 설정 (에이전트에게 요청)
# "앞으로 의미 있는 변경이 생길 때마다 GitHub에 커밋을 계속 만들어서 백업해줘"
# → GitHub 레포지토리 경로도 함께 제공
```

**백업 내용**: 스킬, 메모리, 채널 manifest — 민감한 토큰 값은 자동 제외

### 7. 폴백 모델 설정 (안정성 확보)

```bash
hermes fallback add
# → OpenRouter 선택 → API 키 입력 → 모델 선택

hermes fallback list   # 현재 폴백 체인 확인
hermes fallback remove # 특정 폴백 제거
```

**폴백 체인 예시:**
```
주 모델: GPT-5.5 / OpenAI Codex
1차 폴백: Ollama Alpha (OpenRouter 무료)
2차 폴백: DeepSeek V4 Pro (OpenRouter 저렴)
```

**주의**: 헤르메스에서 싼 모델은 스킬 1개 호출에는 효과적이나,
여러 스킬을 동시에 사용할 때 컨텍스트 윈도우 부족으로 성능 저하 발생.

### 8. 핵심 명령어 레퍼런스 (이 영상 기준)

```bash
# 설치/설정
hermes setup full / hermes setup quick

# 프로필
hermes profile create clone <name>
hermes profile list
hermes profile use <name>

# Slack
hermes slack manifest --write
hermes setup gateway
hermes gateway 1

# 설정
hermes config set GIT_TOKEN <token>

# 폴백
hermes fallback add
hermes fallback list
hermes fallback remove
```

## 연결된 개념

- [[wiki/concepts/hermes-architecture|Hermes 아키텍처]] — gateway·profile·SOUL 구조 전체
- [[wiki/entities/hermes-agent|헤르메스 에이전트]] — BBW 설치 현황

## 연결된 엔티티

- [[wiki/entities/sam-hottman|샘 호트만]] — 튜토리얼 제작자
- [[wiki/entities/hermes-agent|헤르메스 에이전트]] — 설치 대상
- [[wiki/entities/hostinger|Hostinger]] — VPS 서비스

## 메모

- 다음 영상 예고: Gmail 연동 → 이메일 요약·초안 자동화 실전
- 모든 명령어와 매뉴얼은 노션 리소스 페이지에 정리 (댓글 폼 통해 신청)
- BBW는 이미 헤르메스 설치 완료 상태 — GitHub 백업(GIT_TOKEN)·폴백 모델 설정이 미적용 항목으로 참고 가능
- Hostinger 할인 코드: AISAMHOTTMAN (10%)
