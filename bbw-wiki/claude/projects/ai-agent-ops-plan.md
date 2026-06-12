# AI Agent Ops 구현 계획

작성일: 2026-06-11
기준: AI_AGENT_OPS_DEVELOPMENT_PLAN.md + 서버 환경 진단 + Obsidian 위키 분석

---

## 1. 현황 요약

### 설치된 AI 도구
| 도구 | 버전 | 경로 | 상태 |
|------|------|------|------|
| Claude Code | 2.1.170 | `/home/bbw/.local/bin/claude` | 설치됨 |
| Hermes Agent | v0.16.0 (2026.6.5) | `/home/bbw/.local/bin/hermes` | 설치됨 |
| Codex CLI | 0.139.0 (@openai/codex) | `/usr/local/bin/codex` | 설치됨 |
| Node.js | v22.22.1 | `/usr/bin/node` | 설치됨 |
| Python3 | 3.14.4 | `/usr/bin/python3` | 설치됨 |
| Docker | 29.1.3 | `/usr/bin/docker` | 설치됨 |

### 미설치 도구
- `antigravity` CLI — **설치 필요** (Gemini CLI 공식 후속. `gemini` CLI는 2026-06-18 서비스 종료)
- Gemini Python SDK — 설치 필요 (api-key fallback 용)
- Anthropic Python SDK — 설치 필요
- OpenAI Python SDK — 설치 필요

> `gemini` CLI는 레거시로 분류. `run-gemini` wrapper에서 호출 시 자동 차단됨.

### 현재 MCP 서버
| 이름 | 종류 | 경로 | 권한 범위 |
|------|------|------|-----------|
| obsidian | Node.js | `/home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js` | vault 전체 쓰기 + delete-note 노출 (보안 취약) |

### 핵심 발견사항

**1. Gemini 전환 데드라인(2026-06-18)이 7일 후인데 OAuth CLI도, API 키도, wrapper도 전무하다.** 이것은 전환 리스크가 아니라 미구축 상태에서 데드라인이 도래하는 상황이다. 이번 주 내 API 키 발급 + wrapper 뼈대 완성이 최우선이다.

**2. settings.json에 `rm:*`가 allow에 등록되어 있어 `rm -rf`가 현재 허용 상태다.** systemctl, crontab, ~/.ssh 접근도 미차단이다. 에이전트가 파괴적 작업을 무승인 실행할 수 있는 상태다.

**3. Phase 0가 완료로 표시되었으나 /srv/ai/ 미생성, API 키 미설정, AGENTS.md 미작성 등 핵심 인프라가 실제로는 미완료 상태다.** obsidian-mcp의 delete-note 보안 취약점도 미조치 상태다.

---

## 2. 현황 갭 분석 테이블

| 항목 | 계획 | 현재 상태 | 갭 | 우선순위 |
|------|------|-----------|-----|----------|
| Antigravity CLI 및 API 키 | run-gemini wrapper(BACKEND=antigravity)로 리서치 담당 | Antigravity CLI 미설치, GEMINI_API_KEY 미발급, wrapper 완성 | Antigravity CLI 설치 + API 키 발급 필요 | **P0** |
| settings.json deny 정책 | rm -rf, systemctl, crontab, ~/.ssh, git push 전체 차단 | sudo·git push --force·.env는 차단, `rm:*`가 ALLOW에 있어 rm -rf 허용, systemctl·crontab·~/.ssh 미차단 | rm -rf 실행 가능한 위험 상태 | **P0** |
| /srv/ai/ 디렉터리 구조 | vault, repos, worktrees, tasks, logs, scripts, secrets 계층 | /srv/가 빈 디렉터리, /srv/ai/ 없음 | 에이전트 격리 작업공간 전무. 멀티에이전트 자동화 실행 불가 | **P0** |
| ~/.codex/AGENTS.md | Codex 금지 작업(git push 무승인, .env, ~/.ssh, /etc) 지침 파일 | ~/.codex/rules/default.rules에 hermes/dashboard allow 룰 1줄만 존재, AGENTS.md 없음 | Codex가 금지 작업 제약 없이 실행 중 | **P0** |
| GEMINI.md 및 .geminiignore | Gemini 역할·금지 작업·출력 형식 지침 + 시크릿 ignore | 전무 | Gemini 도입 시 역할 혼선 및 시크릿 노출 위험 | **P0** |
| run-gemini wrapper | BACKEND 환경변수로 antigravity\|api-key 분기 | **완료** — `~/ai-ops/scripts/agent-router/run-gemini` | Antigravity CLI 설치 후 즉시 사용 가능 | ~~P0~~ **완료** |
| Obsidian vault 신규 폴더 구조 (1단계) | 00-inbox/, 30-runbooks/, 50-prompts/, 60-agent-configs/, 90-agent-logs/, 99-archive/ 신규 생성 | claude/, wiki/, raw/, bbw-wiki/ 4개만 존재 | 자동화 흐름 지원 위치 없음 | **P0** |
| CLAUDE.md 멀티에이전트 운영 섹션 | Hermes 서브에이전트 호출 시 역할 정의, Codex output 리뷰 절차, worktree 원칙 | 개인 생산성 도구 기준으로만 작성됨 | 자동화 흐름에서 행동 기준 불명확 | **P1** |
| Hermes 운영 라우팅 정책 문서 | 60-agent-configs/routing/policy.md, 위험도 4단계 정의 | ~/.hermes/hermes-agent/AGENTS.md는 개발 기여 가이드 (운영 지침 대체 불가) | 위험 작업 차단 기준 없음 | **P1** |
| Obsidian vault 기존 파일 이관 (2~6단계) | ADR → 40-decisions/adr/, projects → 10-projects/, raw transcript → 20-research/99-archive/ | ADR 6개, projects 8개, transcript 6개 현 위치 유지 | CLAUDE.md 하드코딩 경로 수정 전 이동 불가 | **P1** |
| Obsidian 작업 카드 템플릿 | 00-inbox/requests/ 아래 표준 작업 카드 형식 | 없음 | Hermes 작업 수신·파싱 불가 | **P1** |
| obsidian-gateway MCP | path allowlist + delete-note 미노출 + 도메인 도구 | obsidian-mcp v1.0.6이 vault 전체 쓰기·delete-note 노출 | 에이전트가 vault 전체 삭제 가능 | **P1** |
| repo-index MCP | 코드베이스 읽기 전용 MCP | 미설치. @modelcontextprotocol/server-filesystem으로 즉시 대체 가능 | Hermes가 코드베이스 컨텍스트 읽는 경로 없음 | **P2** |
| run-claude, run-codex wrapper | 에이전트별 비대화형 실행 래퍼 | scripts/agent-router/ 미생성 | Hermes 자동 라우팅 파이프라인 구성 불가 | **P2** |
| 야간 자율 학습 루프 (Hermes 기반) | Hermes가 02:00 AI 뉴스·논문 탐색 후 Obsidian 위키화 | Claude Code 기반 02:00/02:30 크론잡 부분 운영 (Hermes 기반 아님) | Hermes 기반 전환 미완료, 3시간 자동 커밋 미구현 | **P2** |
| Linux 계정 분리 | 에이전트별 격리 계정 5개 | 단일 사용자 bbw | 오버엔지니어링 (계획서도 단일 사용자 시작 인정) | **P3** |
| task-queue MCP | /srv/ai/tasks/ 파일시스템 기반 큐 관리 | 미구현 | Phase 3 이후 필요, 파일 기반 큐로 대체 가능 | **P3** |
| server-control MCP | systemctl 상태 조회 전용 thin wrapper | 미구현, 오픈소스 대안 없음 | Phase 4 이후 필요 | **P3** |

---

## 3. 긴급 조치 (이번 주 — P0)

### 3-1. Antigravity CLI 설치 + GEMINI_API_KEY 발급 (소요: 10분, 리스크: 낮음)

**배경**: Gemini CLI 2026-06-18 종료. Antigravity CLI가 공식 후속 도구.
`run-gemini` wrapper 기본 경로는 이미 `BACKEND=antigravity`로 설정됨.

```bash
# 1) Antigravity CLI 설치 (공식 저장소에서 패키지명 재확인 권장)
npm install -g @google/antigravity-cli
antigravity --version

# 2) GEMINI_API_KEY 발급 (api-key fallback 용)
# https://aistudio.google.com/apikey 에서 발급 후:
echo 'export GEMINI_API_KEY="<발급받은키>"' >> ~/.bashrc
source ~/.bashrc

# 3) 검증
BACKEND=antigravity run-gemini "안녕하세요. 한 줄로 답하세요."
# Antigravity 미설치 시 fallback 테스트:
BACKEND=api-key run-gemini "안녕하세요. 한 줄로 답하세요."
```

**롤백**: `npm uninstall -g @google/antigravity-cli` / `~/.bashrc`에서 `GEMINI_API_KEY` export 줄 제거.

---

### 3-2. settings.json deny 정책 보완 (소요: 10분, 리스크: 낮음)

**배경**: 현재 `rm:*`가 allow에 등록되어 `rm -rf`가 허용 상태. systemctl, crontab, ~/.ssh 접근도 미차단.

`/home/bbw/.claude/settings.json`의 `"deny"` 배열에 아래 항목을 추가한다.

```json
"Bash(rm -rf*)",
"Bash(rm -rf /*)",
"Bash(systemctl *)",
"Bash(crontab *)",
"Read(~/.ssh/*)",
"Bash(ssh-keygen *)",
"Bash(git push *)"
```

> 주의: 기존 `"Bash(git push --force*)"` 는 유지하고, 상위 범위인 `"Bash(git push *)"` 를 추가하면 force 포함 모든 push가 차단된다. git push가 필요할 때는 `/commit` 커맨드를 통해 명시적 승인 후 실행한다.

**롤백**: 추가한 줄 4개를 deny 배열에서 제거.

---

### 3-3. /srv/ai/ 디렉터리 구조 생성 (소요: 5분, 리스크: 낮음)

**배경**: Phase 0 필수 인프라. 에이전트 격리 작업공간, 작업 큐, 로그 경로 전무.

```bash
sudo mkdir -p /srv/ai/{vault,repos,worktrees/{codex,claude,gemini},tasks/{pending,running,done,failed},logs/{hermes,codex,claude,gemini},scripts/agent-router,secrets}

sudo chown -R bbw:bbw /srv/ai

# 검증
find /srv/ai -type d | sort
```

**롤백**: `sudo rm -rf /srv/ai` (Phase 0 완성 전에는 데이터 없음).

---

### 3-4. ~/.codex/AGENTS.md 신규 생성 (소요: 15분, 리스크: 낮음)

**배경**: Codex가 현재 금지 작업 제약 없이 실행 중. git push, .env, ~/.ssh 접근이 무승인으로 가능한 상태.

파일 경로: `/home/bbw/.codex/AGENTS.md`

```markdown
# Codex Agent 운영 지침

## 역할
배치 코드 수정 실행자. 지정된 worktree(/srv/ai/worktrees/codex/) 내에서만
코드 변경을 수행한다. 코드 외 시스템 변경은 수행하지 않는다.

## Working Agreements

### 허용 작업
- /srv/ai/worktrees/codex/ 하위 파일 읽기·수정
- 테스트 실행 및 결과 보고
- 코드 분석 및 리팩토링 제안

### 금지 작업 (무승인 절대 금지)
- `git push` — 어떤 형태든 원격 push 불가
- `git commit --amend` — 히스토리 변경 불가
- `.env`, `*.key`, `*.pem`, `*secret*` 파일 읽기
- `~/.ssh/` 경로 접근
- `/etc/` 경로 수정
- `rm -rf` 실행
- `systemctl` / `service` 명령 실행
- `sudo` 명령 실행
- 배포 관련 명령 (deploy, release, publish)
- 외부 네트워크 호출 (curl, wget) — 패키지 설치 제외

### 변경 전 필수 확인
1. 변경 대상 파일의 구조와 의존성 파악
2. 기존 테스트 스위트 실행 결과 확인
3. 변경 범위를 최소화 (surgical change 원칙)

## Verification (완료 보고 형식)

작업 완료 시 아래 형식으로 보고:
```
STATUS: success|partial|failed
FILES_CHANGED: <파일 목록>
TESTS_RUN: <테스트 명령>
TESTS_RESULT: pass|fail — <요약>
NOTES: <이상 발견 사항 또는 미완료 사유>
```

## 에스컬레이션 조건
다음 상황에서는 작업을 중단하고 사용자 확인 요청:
- DB 스키마 변경 감지
- 인증·권한 코드 수정
- 외부 API 키 노출 가능성
- 지정 worktree 외부 파일 수정 요청
```

**롤백**: 파일 삭제. Codex 동작에 즉각 영향 없으므로 부작용 없음.

---

### 3-5. Obsidian Vault 신규 폴더 1단계 생성 (소요: 5분, 리스크: 낮음)

**배경**: 기존 파일을 건드리지 않고 새 폴더만 생성. CLAUDE.md 경로 충돌 없음.

```bash
mkdir -p ~/obsidian-vault/bbw-wiki/{00-inbox/requests,10-projects,20-research/{web,product-docs},30-runbooks/{security,operations},40-decisions/{adr,policies},50-prompts/{codex,claude,gemini,hermes},60-agent-configs/{permissions,routing,mcp},90-agent-logs/{daily,tasks,failures,weekly},99-archive}

# 검증
ls ~/obsidian-vault/bbw-wiki/
```

**롤백**: `rm -rf ~/obsidian-vault/bbw-wiki/{00-inbox,10-projects,20-research,30-runbooks,40-decisions,50-prompts,60-agent-configs,90-agent-logs,99-archive}` (기존 폴더 무관).

---

### 3-6. run-gemini wrapper — 완료 (Antigravity 기본)

**상태**: 완료 (`~/ai-ops/scripts/agent-router/run-gemini`, symlink `~/.local/bin/run-gemini`)

파일 경로: `~/ai-ops/scripts/agent-router/run-gemini`

```bash
#!/usr/bin/env bash
# run-gemini — Gemini 호출 wrapper
# BACKEND 환경변수: gemini | antigravity | api-key (기본값: api-key)
# 사용법: run-gemini "프롬프트" [--model gemini-2.0-flash] [--format json|text]
set -euo pipefail

BACKEND="${BACKEND:-api-key}"
PROMPT="${1:-}"
MODEL="${MODEL:-gemini-2.0-flash}"
OUTPUT_FORMAT="text"
LOG_DIR="/srv/ai/logs/gemini"
LOG_FILE="$LOG_DIR/$(date +%Y-%m-%d).log"

if [[ -z "$PROMPT" ]]; then
  echo "오류: 프롬프트 인수가 필요합니다." >&2
  echo "사용법: run-gemini \"프롬프트\" [--model <모델>] [--format json|text]" >&2
  exit 1
fi

# 옵션 파싱
shift
while [[ $# -gt 0 ]]; do
  case "$1" in
    --model) MODEL="$2"; shift 2 ;;
    --format) OUTPUT_FORMAT="$2"; shift 2 ;;
    *) echo "알 수 없는 옵션: $1" >&2; exit 1 ;;
  esac
done

mkdir -p "$LOG_DIR"

log() {
  echo "[$(date '+%Y-%m-%dT%H:%M:%S')] [BACKEND=$BACKEND] $*" >> "$LOG_FILE"
}

run_api_key() {
  if [[ -z "${GEMINI_API_KEY:-}" ]]; then
    echo "오류: GEMINI_API_KEY 환경변수가 설정되지 않았습니다." >&2
    echo "발급: https://aistudio.google.com/apikey" >&2
    exit 1
  fi

  local payload
  payload=$(python3 -c "
import json, sys
prompt = sys.argv[1]
print(json.dumps({'contents': [{'parts': [{'text': prompt}]}]}))
" "$PROMPT")

  curl -s \
    -H "Content-Type: application/json" \
    -H "X-goog-api-key: $GEMINI_API_KEY" \
    -d "$payload" \
    "https://generativelanguage.googleapis.com/v1beta/models/${MODEL}:generateContent" \
  | python3 -c "
import json, sys
data = json.load(sys.stdin)
try:
    text = data['candidates'][0]['content']['parts'][0]['text']
    print(text)
except (KeyError, IndexError) as e:
    print(json.dumps(data), file=sys.stderr)
    sys.exit(1)
"
}

run_gemini_cli() {
  if ! command -v gemini &>/dev/null; then
    echo "오류: gemini CLI가 설치되지 않았습니다. BACKEND=api-key로 전환합니다." >&2
    BACKEND="api-key" run_api_key
    return
  fi
  gemini -p "$PROMPT" --model "$MODEL"
}

run_antigravity() {
  if ! command -v antigravity &>/dev/null; then
    echo "오류: antigravity CLI가 설치되지 않았습니다. BACKEND=api-key로 전환합니다." >&2
    BACKEND="api-key" run_api_key
    return
  fi
  # TODO: antigravity 인터페이스 확인 후 플래그 수정 필요
  antigravity -p "$PROMPT"
}

log "호출: PROMPT=${PROMPT:0:80}..."

case "$BACKEND" in
  gemini)      run_gemini_cli ;;
  antigravity) run_antigravity ;;
  api-key)     run_api_key ;;
  *)
    echo "오류: 알 수 없는 BACKEND=$BACKEND (gemini|antigravity|api-key 중 하나)" >&2
    exit 1
    ;;
esac

log "완료"
```

```bash
# 저장 후 실행 권한 부여
chmod +x /srv/ai/scripts/agent-router/run-gemini

# 심볼릭 링크 (선택)
ln -sf /srv/ai/scripts/agent-router/run-gemini ~/.local/bin/run-gemini

# 검증 (API 키 발급 후)
BACKEND=api-key run-gemini "1+1은?"
```

**롤백**: 파일 삭제. 상위 호출자에 영향 없음.

---

### 3-7. GEMINI.md 신규 생성 (소요: 20분, 리스크: 낮음)

파일 경로: `~/GEMINI.md`

```markdown
# Gemini Agent 운영 지침

## 역할 및 전문 영역
- 웹 리서치 및 최신 정보 검색 (기본 역할)
- 멀티모달 분석 (이미지, PDF, 문서 처리)
- 장문 컨텍스트 분석 (1M 토큰 컨텍스트 활용)
- AI 논문·뉴스 탐색 및 Obsidian 위키화

## 인증 방식
- **현재**: GEMINI_API_KEY 환경변수 기반 (Google AI Studio 무료 티어)
- **실행 경로**: run-gemini wrapper (`/srv/ai/scripts/agent-router/run-gemini`)를 통해서만 호출
- 직접 CLI 호출 금지 (wrapper 우회 방지)

## 금지 작업
- 코드 파일 단독 수정 (리서치 결과 제공까지만, 변경은 Claude Code 또는 Codex가 수행)
- 시크릿·API 키·자격증명 파일 읽기
- 배포·빌드·테스트 명령 실행
- 파일시스템 직접 쓰기 (Obsidian MCP를 통해서만 저장)
- ~/.ssh/, ~/.aws/, ~/.config/gcloud/ 경로 접근

## 출력 형식
- 기본: Markdown (헤더·목록·코드블록 구조화)
- API 연동 시: JSON 또는 stream-json
- **인용 필수**: 웹 정보 출력 시 URL 출처를 반드시 포함
- 리서치 결과는 `90-agent-logs/` 또는 `20-research/` 경로에 저장

## 모델 선택 기준
| 작업 유형 | 권장 모델 |
|-----------|-----------|
| 빠른 검색·요약 | gemini-2.0-flash |
| 장문 분석·멀티모달 | gemini-2.5-pro |
| 코드 리뷰 보조 | gemini-2.0-flash |
```

---

### 3-8. obsidian-mcp delete-note 임시 차단 (소요: 30분, 리스크: 중간)

**배경**: 현재 에이전트가 vault 전체 파일을 무제한 삭제 가능. Phase 4 obsidian-gateway 완성 전까지 임시 보호 조치 필요.

```bash
# 1) obsidian-mcp 소스 위치 확인
ls /home/bbw/.local/lib/node_modules/obsidian-mcp/build/

# 2) 현재 노출된 도구 목록 확인
node -e "
const m = require('/home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js');
" 2>&1 | head -20

# 3) settings.json에서 obsidian MCP 서버에 allowedTools 제한 추가
# (MCP 서버 레벨 도구 필터링이 지원되지 않는 경우 아래 방법 사용)
```

MCP 서버 레벨 allowedTools 미지원 시 대안:

```bash
# main.js에서 delete-note 도구 등록 라인 주석 처리
# 백업 후 수정
cp /home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js \
   /home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js.bak

# delete-note 관련 줄 확인 후 제거
grep -n "delete" /home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js | head -20
```

> 주의: Node.js 빌드 파일 직접 수정은 npm update 시 덮어쓰일 수 있다. Phase 4 obsidian-gateway 구현 완료 후 이 임시 조치를 제거한다.

**롤백**: `cp main.js.bak main.js` 후 MCP 서버 재시작.

---

## 4. Obsidian Vault 마이그레이션 전략

### 핵심 원칙

기존 `claude/`, `wiki/`, `raw/`, `bbw-wiki/` 폴더는 **CLAUDE.md와 hooks 경로 수정이 완료될 때까지 절대 이동하지 않는다**. 신규 폴더 생성 → 파일 복사(cp) → 검증 → 구 경로 제거 순서를 엄수한다.

### 단계별 실행 계획

**1단계 — 신규 폴더만 생성 (Phase 0, 즉시 실행)**

기존 파일 무관. 실행 명령은 §3-5 참조.

**2단계 — ADR 이관 (Phase 1)**

```bash
# 2-1) 하드코딩 경로 전체 추출
grep -r 'obsidian-vault/bbw-wiki' ~/.claude/CLAUDE.md ~/.claude/hooks/ 2>/dev/null

# 2-2) ADR 복사
cp ~/obsidian-vault/bbw-wiki/claude/decisions/*.md \
   ~/obsidian-vault/bbw-wiki/40-decisions/adr/

# 2-3) CLAUDE.md decisions 경로 수정
# Before: ~/obsidian-vault/bbw-wiki/claude/decisions/
# After:  ~/obsidian-vault/bbw-wiki/40-decisions/adr/

# 2-4) 검증: hooks 정상 동작 확인
bash -n ~/.claude/hooks/session-start/load-context.sh

# 2-5) 원본 제거 (검증 통과 후)
rm -rf ~/obsidian-vault/bbw-wiki/claude/decisions/
```

**3단계 — 프로젝트 노트 이관 (Phase 1)**

```bash
# 3-1) projects 복사
cp ~/obsidian-vault/bbw-wiki/claude/projects/*.md \
   ~/obsidian-vault/bbw-wiki/10-projects/

# 3-2) CLAUDE.md projects 경로 수정
# Before: ~/obsidian-vault/bbw-wiki/claude/projects/
# After:  ~/obsidian-vault/bbw-wiki/10-projects/

# 3-3) session-start hook 경로 동시 수정
grep -n 'projects' ~/.claude/hooks/session-start/load-context.sh

# 3-4) 검증 후 원본 제거
```

**4단계 — raw/ transcript 처리 (Phase 1)**

```bash
# 리서치 참조용 → 20-research/web/
cp ~/obsidian-vault/bbw-wiki/raw/2026-06-*-transcript.md \
   ~/obsidian-vault/bbw-wiki/20-research/web/

# 단순 보관용 → 99-archive/
# raw/assets/ 는 별도 결정 후 처리
```

**5단계 — wiki/ 폴더 처리**

```bash
# wiki/concepts/, entities/, queries/, sources/ 는 이관하지 않고 현행 유지
# 역할 명시 README만 추가
cat > ~/obsidian-vault/bbw-wiki/wiki/README.md << 'EOF'
# wiki/ — 지식 그래프 (현행 유지)

계획서 §4.1 신규 폴더 구조와 별도로 독립 유지.
- concepts/ : MCP, 에이전트 아키텍처 등 개념 정리
- entities/  : 도구·서비스 엔티티 정보
- queries/   : 자주 쓰는 검색 패턴
- sources/   : 외부 참조 자료

강제 통합 금지 — 현재 지식 그래프 구조 보존 우선.
EOF
```

**보류 항목**

| 항목 | 보류 사유 | 처리 시점 |
|------|-----------|-----------|
| `claude/session-log.md` | hooks/session-start/load-context.sh가 직접 참조 | 해당 hook 경로 수정과 동시 진행 |
| `work-in-progress.md` | 동일 이유 | 동일 |
| `bbw-wiki/bbw-wiki/` 중첩 폴더 | 내용 확인 필요 | Phase 1에서 확인 후 99-archive/ 또는 삭제 |
| `raw/assets/` | 용도 분류 필요 | Phase 1 말미에 결정 |

---

## 5. 조정된 구현 로드맵

### Phase 0 — 현황 진단 및 보안 기반 완성
**기간**: 2026-06-11~12 (1~2일)
**목표**: 필수 인프라 구축 + 보안 취약점 즉시 조치

**이미 완료**
- 서버 환경 진단 (AI 도구 목록, 실행 중인 서비스, 포트 현황)
- Obsidian 위키 구조 분석
- agent-architecture.md 에이전트 라우팅 매트릭스 작성
- MCP 서버 현황 파악
- Hermes v0.16.0, Codex v0.139.0, Claude Code v2.1.170 설치 확인

**수정된 작업 목록**
- [ ] GEMINI_API_KEY 발급 및 ~/.bashrc 등록 (§3-1)
- [ ] settings.json deny 정책 보완: rm -rf, systemctl, crontab, ~/.ssh, git push (§3-2)
- [ ] /srv/ai/ 전체 디렉터리 구조 생성 (§3-3)
- [ ] Obsidian vault 신규 폴더 1단계 생성 (§3-5)
- [ ] server-inventory.md 작성 → `60-agent-configs/` 저장
- [ ] Hermes 중복 실행 여부 확인 (3개 프로세스 정상 여부)
- [ ] 포트 80/443/9119 담당 프로세스 확인 (`ss -tlnp` 또는 `lsof -i`)

**원래 계획 대비 변경 사항**: Phase 0를 완료 처리했으나 /srv/ai/ 미생성·API 키 미설정이 확인되어 재개. Gemini 전환 데드라인 대응을 Phase 0에 포함.

---

### Phase 1 — 지식 원장 구축 및 Obsidian vault 재구조화
**기간**: 2026-06-12~15 (3~4일)
**목표**: vault 이관 + 작업 카드 체계 수립

**이미 완료**
- Hermes, 자유령 에이전트 3종 비교 리서치 완료
- MCP 개념 정리 (wiki/concepts/mcp.md)
- AI 네이티브 팀 구성 개념 정리
- Claude Code 기반 02:00/02:30 AI 리서치 크론잡 운영 중
- WIP 파일(work-in-progress.md) 운영 중

**수정된 작업 목록**
- [ ] Obsidian vault 2단계: ADR 6개 40-decisions/adr/ 이관 + CLAUDE.md 경로 수정
- [ ] Obsidian vault 3단계: claude/projects/ 8개 노트 10-projects/ 이관 + hooks 경로 수정
- [ ] Obsidian vault 4단계: raw/ transcript 분류 이동
- [ ] wiki/ 폴더 README.md 추가
- [ ] 00-inbox/requests/ 작업 카드 템플릿 생성
- [ ] bbw-wiki/bbw-wiki/ 중첩 폴더 내용 확인 및 처리
- [ ] 크론잡 실제 동작 여부 검증 (`crontab -l` 결과 없으므로 저장 방식 확인)

**원래 계획 대비 변경 사항**: Obsidian 이관을 5단계로 분리. wiki/ 폴더는 현행 유지. 크론잡 검증 항목 추가.

---

### Phase 2 — 에이전트 지침 파일 작성
**기간**: 2026-06-13~16 (Phase 1과 일부 병렬)
**목표**: 에이전트별 역할·금지 작업·출력 형식 명문화

**이미 완료**
- CLAUDE.md 핵심 운영 원칙 작성 (계획 우선, 검증 체크리스트, 금지 사항)
- ~/.claude/agents/ 에이전트 파일 존재 (orchestrator, senior-strategist, backend-agent 등)
- memory/agent-architecture.md 라우팅 매트릭스 완성
- settings.json deny 정책 부분 설정

**수정된 작업 목록**
- [ ] ~/.codex/AGENTS.md 신규 생성 (§3-4)
- [ ] ~/GEMINI.md 신규 생성 (§3-7)
- [ ] ~/.geminiignore 생성 (`~/.ssh/, ~/.aws/, **/.env, /srv/ai/secrets/` 차단)
- [ ] CLAUDE.md 멀티에이전트 운영 섹션 추가 (Hermes 서브에이전트 호출·Codex 리뷰 절차·worktree 원칙)
- [ ] ~/.codex/rules/default.rules에 금지 룰 추가 (git push, rm -rf, sudo, /etc 수정)
- [ ] 60-agent-configs/routing/policy.md 작성 (위험도 4단계, 승인 기반 분기)

**원래 계획 대비 변경 사항**: settings.json deny 정책 보완을 Phase 0에서 먼저 처리. CLAUDE.md는 기존 내용 보존 + 섹션 추가 방식 적용.

---

### Phase 3 — Hermes 라우터 및 wrapper 스크립트 구현
**기간**: 2026-06-14~21 (4~7일)
**목표**: 에이전트 자동 호출 파이프라인 구축

**이미 완료**
- Hermes v0.16.0 (cron, webhook, kanban, gateway 내장)
- Codex CLI v0.139.0 설치
- Claude Code v2.1.170 (`claude --print` 비대화형 지원)
- Hermes 내장 kanban_db.py, kanban.py 작업 큐 구현됨

**수정된 작업 목록**
- [x] **run-gemini wrapper 완성** — `~/ai-ops/scripts/agent-router/run-gemini` (BACKEND=antigravity 기본)
- [ ] Antigravity CLI 설치 (`npm install -g @google/antigravity-cli`) 및 인터페이스 검증
- [ ] GEMINI_API_KEY 발급 (fallback 용)
- [ ] run-claude wrapper (`/srv/ai/scripts/agent-router/run-claude`, `claude --print` 기반)
- [ ] run-codex wrapper (`/srv/ai/scripts/agent-router/run-codex`, `codex exec` 래핑)
- [ ] classify-task 스크립트 (작업 유형·위험도 분류, JSON 출력)
- [ ] append-log 스크립트 (90-agent-logs/ 직접 append)
- [ ] require-approval 스크립트 (High/Critical 위험도 차단 + 사용자 알림)
- [ ] Hermes cron으로 tasks/pending 감시 루프 구성

**원래 계획 대비 변경 사항**: run-gemini를 Phase 0/1과 병렬로 이번 주 완성. Hermes 내장 cron 활용으로 별도 감시 루프 구현 제거. Linux 계정 5개 분리는 P3 유지.

---

### Phase 4 — MCP Gateway 구현
**기간**: 2026-06-19~27 (5~8일)
**목표**: 에이전트 vault 접근 제어 + 코드베이스 읽기 MCP

**이미 완료**
- obsidian-mcp v1.0.6 설치 및 settings.json 등록
- Node.js v22.22.1 (@modelcontextprotocol/sdk v1.29.0 접근 가능)
- MCP 개념 및 활용 사례 리서치 완료

**수정된 작업 목록**
- [ ] repo-index 대안 즉시 적용: `npm install -g @modelcontextprotocol/server-filesystem` + settings.json 읽기 전용 등록
- [ ] obsidian-gateway MCP 구현: path allowlist (00-inbox, 40-decisions, 90-agent-logs 쓰기만), delete-note 미노출, append-only 보장
- [ ] 도메인 도구 추가: `create_task`, `append_task_log`, `update_task_status`, `create_adr`
- [ ] settings.json에서 기존 obsidian-mcp를 obsidian-gateway로 교체
- [ ] task-queue MCP 구현 여부 결정 (Hermes 내장 kanban과 역할 분리 후 판단)

**원래 계획 대비 변경 사항**: repo-index는 server-filesystem으로 즉시 대체 (별도 구현 제거). obsidian-gateway를 래퍼 레이어로 구현하면 3~5일 단축. Phase 3보다 obsidian-gateway 일부를 먼저 구현하는 순서 변경 검토 권장.

---

### Phase 5 — 정기 루틴 자동화
**기간**: 2026-06-25~30 (3~5일)
**목표**: 야간 학습 루프 Hermes 전환 + 주간 요약 자동화

**이미 완료**
- Claude Code 기반 02:00/02:30 AI 리서치 크론잡 운영 중 (Hermes 기반 아님)
- 05:00 git 자동 커밋 설정 존재 (1회/일)
- session-log.md, work-in-progress.md 운영 중

**수정된 작업 목록**
- [ ] 기존 Claude Code 기반 크론잡 현황 정확히 파악 후 Hermes 기반 전환 또는 공존 설계
- [ ] Hermes cron으로 3시간 자동 커밋 추가 (현재 1회/일 보완)
- [ ] 주간 요약 루틴 (매주 월요일 집계 → 90-agent-logs/weekly/)
- [ ] 야간 자율 학습 루프 Hermes 전환: 02:00 AI 뉴스·논문·Reddit 탐색 → wiki/ 자동 업데이트
- [ ] 디자인 에이전트 학습 루프 (Dribbble·Awwwards·Mobbin) 별도 검토

---

### Phase 6 — 보안 강화 및 감사
**기간**: 2026-07-01~03 (2~3일)
**목표**: deny 정책 전체 재검증 + 에이전트 로그 감사 체계 수립

**수정된 작업 목록**
- [ ] Phase 0에서 보완한 deny 정책 전체 재검증
- [ ] 에이전트별 작업 로그 감사 (90-agent-logs/ 이상 패턴 탐지)
- [ ] API 키 로테이션 절차 문서화 (30-runbooks/security/)
- [ ] obsidian-gateway path allowlist 실제 동작 검증
- [ ] Linux 계정 분리 필요성 재평가 (6개월 단일 사용자 운영 후 결정)

---

### Phase 7 — 고도화 및 확장 (백로그)
**기간**: 2026-07 이후

**수정된 작업 목록**
- [ ] Vertex AI 서비스 계정 키 구성 (장기 안정성, `BACKEND=vertex` 추가)
- [ ] Vertex AI 서비스 계정 키 구성 (BACKEND=vertex 장기 안정성)
- [ ] Zotero MCP 설치 및 연구 문헌 관리 통합
- [ ] notebooklm.py MCP (토큰 65~90% 절감 효과)
- [ ] Google Calendar/Drive MCP 연동
- [ ] server-control MCP (systemctl 상태 조회 전용)
- [ ] Linux 계정 분리 재검토 (팀 환경 전환 시 deploybot 1개 먼저)
- [ ] OpenDesign URL 확인 + 디자인 에이전트 학습 루프

---

## 6. 즉시 실행 명령 목록

승인 후 아래 순서대로 실행한다. 각 단계 완료 후 검증 명령 실행 필수.

### Step 1 — GEMINI_API_KEY 등록

```bash
# Google AI Studio(https://aistudio.google.com/apikey)에서 키 발급 후:
echo 'export GEMINI_API_KEY="YOUR_KEY_HERE"' >> ~/.bashrc
source ~/.bashrc
curl -s "https://generativelanguage.googleapis.com/v1beta/models?key=$GEMINI_API_KEY" \
  | python3 -m json.tool | grep "name" | head -5
# 롤백: ~/.bashrc에서 GEMINI_API_KEY export 줄 제거
```

### Step 2 — /srv/ai/ 구조 생성

```bash
sudo mkdir -p /srv/ai/{vault,repos,worktrees/{codex,claude,gemini},tasks/{pending,running,done,failed},logs/{hermes,codex,claude,gemini},scripts/agent-router,secrets}
sudo chown -R bbw:bbw /srv/ai
find /srv/ai -type d | sort
# 롤백: sudo rm -rf /srv/ai
```

### Step 3 — settings.json deny 정책 보완

```bash
# 수정 전 백업
cp ~/.claude/settings.json ~/.claude/settings.json.bak.$(date +%Y%m%d)
# 편집 후 JSON 유효성 검사
jq . ~/.claude/settings.json > /dev/null && echo "JSON OK" || echo "JSON 파싱 오류"
# 롤백: cp ~/.claude/settings.json.bak.<날짜> ~/.claude/settings.json
```

### Step 4 — Obsidian vault 신규 폴더 생성

```bash
mkdir -p ~/obsidian-vault/bbw-wiki/{00-inbox/requests,10-projects,20-research/{web,product-docs},30-runbooks/{security,operations},40-decisions/{adr,policies},50-prompts/{codex,claude,gemini,hermes},60-agent-configs/{permissions,routing,mcp},90-agent-logs/{daily,tasks,failures,weekly},99-archive}
ls ~/obsidian-vault/bbw-wiki/
# 롤백: rm -rf ~/obsidian-vault/bbw-wiki/{00-inbox,10-projects,...} (기존 폴더 무관)
```

### Step 5 — ~/.codex/AGENTS.md 생성

```bash
# §3-4의 내용으로 파일 생성
ls -la ~/.codex/
# 롤백: rm ~/.codex/AGENTS.md
```

### Step 6 — Antigravity CLI 설치 및 run-gemini 검증 (wrapper는 이미 완료)

```bash
# wrapper 경로 확인
ls -la ~/.local/bin/run-gemini
# → symlink: /home/bbw/ai-ops/scripts/agent-router/run-gemini

# Antigravity CLI 설치 (공식 저장소에서 패키지명 확인 후 실행)
npm install -g @google/antigravity-cli
antigravity --version

# 검증 (Antigravity)
BACKEND=antigravity run-gemini "안녕하세요. 한 줄로 답하세요."

# 검증 (api-key fallback)
BACKEND=api-key run-gemini "안녕하세요. 한 줄로 답하세요."

# 롤백: npm uninstall -g @google/antigravity-cli
```

### Step 7 — GEMINI.md 생성

```bash
# §3-7의 내용으로 ~/GEMINI.md 생성
cat << 'EOF' > ~/.geminiignore
~/.ssh/
~/.aws/
~/.config/gcloud/
**/.env
**/.env.*
**/*.key
**/*.pem
**/*secret*
/srv/ai/secrets/
EOF
# 롤백: rm ~/GEMINI.md ~/.geminiignore
```

### Step 8 — obsidian-mcp delete-note 임시 차단

```bash
# 소스 파일 백업
cp /home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js \
   /home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js.bak
# delete 관련 줄 확인
grep -n "delete" /home/bbw/.local/lib/node_modules/obsidian-mcp/build/main.js
# 롤백: cp main.js.bak main.js
```

---

## 7. 리스크 및 주의사항

### R1 — Gemini CLI 서비스 종료 → Antigravity CLI 전환 (심각도: 중간, 대응 완료)

- **상황**: Gemini CLI 2026-06-18 서비스 종료. **Antigravity CLI로 전환 결정됨.**
- **완료된 조치**:
  - `run-gemini` wrapper 작성 (`~/ai-ops/scripts/agent-router/run-gemini`)
  - 기본 `BACKEND=antigravity`로 설정
  - 레거시 `gemini` 경로는 wrapper 내 차단 처리
  - `BACKEND=api-key` fallback 유지
- **남은 작업**: Antigravity CLI 설치 (`npm install -g @google/antigravity-cli`), GEMINI_API_KEY 발급 (fallback 용)

### R2 — rm -rf 허용 상태 (심각도: 높음, 확률: 낮음)

- **리스크**: settings.json `allow` 배열에 `rm:*`가 등록되어 있어 에이전트가 `rm -rf` 실행 가능.
- **영향**: 파일시스템 파괴적 삭제 무승인 실행 가능.
- **대응**: Step 3에서 즉시 deny 정책 보완. 수정 전 settings.json 반드시 백업.

### R3 — Hermes 중복 실행 (심각도: 중간, 확률: 확인 필요)

- **리스크**: Hermes가 3개 프로세스로 실행 중 (systemd user service + /opt/hermes + ~/.hermes). 동일 작업 중복 실행, 포트 충돌, 로그 분산 가능성.
- **대응**: Phase 0에서 `ps aux | grep hermes` 결과 분석 후 중복 여부 확인. 불필요한 프로세스 정리.

### R4 — 외부 개방 포트 미확인 (심각도: 중간, 확률: 낮음)

- **리스크**: 포트 80/443/9119가 0.0.0.0으로 외부 개방되어 있으나 담당 프로세스 미확인. 비인가 서비스가 운영 중일 가능성.
- **대응**: `sudo ss -tlnp | grep -E '80|443|9119'` 또는 `sudo lsof -i :80,443,9119`로 담당 프로세스 확인. server-inventory.md에 기록.

### R5 — obsidian-mcp delete-note 노출 (심각도: 높음, 확률: 낮음)

- **리스크**: 에이전트가 vault 전체 파일을 삭제 가능.
- **대응**: Step 8에서 임시 차단. Phase 4 obsidian-gateway 완성 전까지 에이전트에 vault 쓰기 작업 직접 지시 자제.

### R6 — Obsidian vault 이관 중 경로 충돌 (심각도: 중간, 확률: 중간)

- **리스크**: ADR·projects 이관 시 CLAUDE.md·hooks 하드코딩 경로 미수정으로 세션 시작 컨텍스트 주입 실패.
- **대응**: 이관 전 반드시 `grep -r 'obsidian-vault/bbw-wiki' ~/.claude/` 전체 경로 추출. 복사(cp) 후 검증 → 원본 제거 순서 엄수.

### R7 — Ubuntu 26.04 LTS 개발 버전 (심각도: 낮음, 확률: 중간)

- **리스크**: 공식 릴리스 전 개발 버전 환경일 가능성. 패키지 불안정 또는 보안 패치 지연 가능성.
- **대응**: `lsb_release -a`로 정확한 버전 확인. 프로덕션 배포 전 OS 버전 재확인.

### R8 — API 키 시크릿 관리 (심각도: 높음, 확률: 높음)

- **리스크**: GEMINI_API_KEY를 ~/.bashrc에 평문 저장 시 git 커밋·로그 노출 위험.
- **대응**: `.gitignore`에 `.bashrc` 추가 확인. 장기적으로 `/srv/ai/secrets/` 또는 `~/.config/` 기반 파일 저장 + 환경변수 참조 방식 전환. API 키는 절대 커밋하지 않는다.

### R9 — Codex 금지 작업 무제약 (심각도: 높음, 확률: 낮음)

- **리스크**: ~/.codex/AGENTS.md 미존재로 Codex가 git push, .env 읽기, ~/.ssh 접근을 무승인 실행 가능.
- **대응**: Step 5에서 AGENTS.md 즉시 생성. ~/.codex/rules/default.rules에 금지 룰 추가 (Phase 2).

---

## 8. Agent Health Registry & Failover

> 운영 원칙: **한 AI가 빠져도 전체 시스템은 멈추지 않는다. 단, 위험한 작업은 자동 우회하지 않는다.**

---

### 8-1. 실패 유형 분류

| 코드 | 이름 | 설명 | 자동 재시도 가능 |
|------|------|------|----------------|
| `auth_expired` | 인증 만료 | API 키 만료, OAuth 토큰 만료, 세션 종료 | 불가 (재인증 필요) |
| `quota_exceeded` | 쿼터 초과 | 분당/일당 요청 한도 도달 | 가능 (대기 후 재시도) |
| `provider_down` | 공급자 장애 | API 엔드포인트 5xx, 타임아웃 | 가능 (지수 백오프) |
| `model_unavailable` | 모델 불가 | 지정 모델 deprecation, 지역 미지원 | 가능 (대체 모델 전환) |
| `context_overflow` | 컨텍스트 초과 | 입력 토큰 한도 초과 | 가능 (청크 분할 후 재시도) |
| `permission_denied` | 권한 거부 | settings.json deny 또는 AGENTS.md 위반 | 불가 (사용자 확인 필요) |

---

### 8-2. Agent Health Registry

상태 파일 경로: `/srv/ai/logs/health/agent-status.json`

```json
{
  "updated": "YYYY-MM-DDTHH:MM:SSZ",
  "agents": {
    "codex": {
      "status": "healthy",
      "last_success": "YYYY-MM-DDTHH:MM:SSZ",
      "last_failure": null,
      "failure_type": null,
      "consecutive_failures": 0,
      "auth_method": "openai_api_key",
      "auth_expires": null,
      "model": "@openai/codex@0.139.0",
      "notes": ""
    },
    "claude": {
      "status": "healthy",
      "last_success": "YYYY-MM-DDTHH:MM:SSZ",
      "last_failure": null,
      "failure_type": null,
      "consecutive_failures": 0,
      "auth_method": "anthropic_api_key",
      "auth_expires": null,
      "model": "claude-sonnet-4-6",
      "notes": ""
    },
    "gemini": {
      "status": "unavailable",
      "last_success": null,
      "last_failure": "YYYY-MM-DDTHH:MM:SSZ",
      "failure_type": "auth_expired",
      "consecutive_failures": 0,
      "auth_method": "gemini_api_key",
      "auth_expires": null,
      "model": "gemini-2.0-flash",
      "notes": "CLI 미설치, API 키 미발급 — 2026-06-11 현재"
    }
  }
}
```

상태 값:
- `healthy` — 정상 동작 중
- `degraded` — 동작하지만 간헐적 실패 (consecutive_failures 1~2)
- `unavailable` — 실패 중 (consecutive_failures 3+)
- `maintenance` — 수동 비활성화

Health Registry 업데이트 스크립트: `/srv/ai/scripts/agent-router/update-health`

```bash
#!/usr/bin/env bash
# update-health <agent> <status> <failure_type?>
# 예: update-health gemini unavailable auth_expired
AGENT="$1"; STATUS="$2"; FAILURE_TYPE="${3:-null}"
HEALTH_FILE="/srv/ai/logs/health/agent-status.json"
mkdir -p "$(dirname "$HEALTH_FILE")"
NOW=$(date -u +%Y-%m-%dT%H:%M:%SZ)

python3 - "$AGENT" "$STATUS" "$FAILURE_TYPE" "$NOW" "$HEALTH_FILE" << 'PYEOF'
import json, sys
agent, status, failure_type, now, path = sys.argv[1:]
try:
    with open(path) as f:
        data = json.load(f)
except FileNotFoundError:
    data = {"agents": {}}
if agent not in data["agents"]:
    data["agents"][agent] = {}
a = data["agents"][agent]
a["status"] = status
a["updated"] = now
if status == "healthy":
    a["last_success"] = now
    a["consecutive_failures"] = 0
    a["failure_type"] = None
else:
    a["last_failure"] = now
    a["failure_type"] = failure_type if failure_type != "null" else None
    a["consecutive_failures"] = a.get("consecutive_failures", 0) + 1
data["updated"] = now
with open(path, "w") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)
print(f"[update-health] {agent} -> {status}")
PYEOF
```

---

### 8-3. Failover Matrix

| 만료 에이전트 | 작업 유형 | Failover 경로 | 제약 |
|--------------|-----------|--------------|------|
| **Codex** | 기능 구현 / 버그 수정 | → 사용자 승인 대기 | **Gemini 자동 대체 금지** — 리서치 전용 에이전트에 코드 변경 위임 불가 |
| **Codex** | 테스트 실행 | → 사용자가 수동 실행 | 자동 우회 없음 |
| **Codex** | 읽기 전용 코드 분석 | → Claude Code 대체 가능 | Medium 이하 위험도만 |
| **Claude Code** | 설계 검토 / 문서화 | → Gemini 부분 대체 가능 | 최종 승인은 사용자 |
| **Claude Code** | 위험도 판단 (High/Critical) | → **자동 진행 금지** | 반드시 사용자 수동 승인 |
| **Claude Code** | diff 리뷰 | → Gemini 대체 가능 (Low/Medium만) | High risk diff는 대기 |
| **Gemini** | 웹 리서치 | → Claude Code WebSearch 대체 | 토큰 비용 증가 인지 필요 |
| **Gemini** | PDF/이미지 분석 | → 사용자 승인 대기 | Claude Code 멀티모달 미지원 |
| **Gemini** | 장문 분석 | → 청크 분할 후 Claude Code | 품질 저하 가능, 사용자 확인 |
| **Hermes** | 작업 라우팅 | → 사용자가 직접 에이전트 호출 | 자동화 일시 중단 |

**역할 경계 원칙**:
1. Codex 만료 → Gemini가 코드를 작성하는 자동 경로는 절대 없다.
2. Claude Code 만료 → High/Critical 위험도 작업은 에이전트 대체 없이 `approval_required` 상태로 전환한다.
3. Gemini 만료 → 리서치 작업은 Claude Code 대체 또는 사용자 승인 대기 중 하나를 명시적으로 선택해야 한다. 암묵적 우회 없음.

---

### 8-4. 에이전트 만료 감지 Runbook

**파일 경로**: `30-runbooks/operations/agent-token-expiry.md`

#### Step A — 만료 감지

```bash
# run-gemini, run-codex, run-claude wrapper 내 공통 감지 로직
# 각 wrapper의 오류 출력에서 아래 패턴 매칭
detect_failure_type() {
  local stderr_output="$1"
  if echo "$stderr_output" | grep -qiE "expired|invalid.*key|unauthorized|401"; then
    echo "auth_expired"
  elif echo "$stderr_output" | grep -qiE "rate.limit|quota|429|too many"; then
    echo "quota_exceeded"
  elif echo "$stderr_output" | grep -qiE "503|502|timeout|connection|unavailable"; then
    echo "provider_down"
  elif echo "$stderr_output" | grep -qiE "model.*not.*found|deprecated|not.*available"; then
    echo "model_unavailable"
  else
    echo "unknown"
  fi
}
```

#### Step B — Obsidian 기록

만료 감지 즉시 작업 카드에 append:

```bash
# append-log 스크립트 호출
/srv/ai/scripts/agent-router/append-log \
  --task-id "$TASK_ID" \
  --agent "$AGENT" \
  --level "ERROR" \
  --message "failure_type=$FAILURE_TYPE detected. Entering failover state."

# Health Registry 업데이트
/srv/ai/scripts/agent-router/update-health "$AGENT" "unavailable" "$FAILURE_TYPE"

# 90-agent-logs/failures/ 에 별도 기록
cat >> /srv/ai/logs/failures/$(date +%Y-%m-%d)-failures.log << EOF
[$(date -u +%Y-%m-%dT%H:%M:%SZ)] AGENT=$AGENT TASK=$TASK_ID FAILURE=$FAILURE_TYPE
EOF
```

#### Step C — 대체 실행 (Failover Matrix 참조)

```bash
run_with_failover() {
  local agent="$1"; local task_type="$2"; local prompt="$3"

  # Health 확인
  local status
  status=$(python3 -c "
import json
with open('/srv/ai/logs/health/agent-status.json') as f:
    d = json.load(f)
print(d['agents'].get('$agent', {}).get('status', 'unknown'))
")

  if [[ "$status" != "healthy" ]]; then
    local failover
    failover=$(lookup_failover "$agent" "$task_type")  # Failover Matrix 참조

    if [[ "$failover" == "user_approval" ]]; then
      /srv/ai/scripts/agent-router/require-approval \
        --reason "agent=$agent status=$status task_type=$task_type" \
        --task-id "$TASK_ID"
      exit 0  # 승인 대기 상태로 전환
    fi

    echo "[failover] $agent unavailable. Routing to $failover" | tee -a "$LOG_FILE"
    agent="$failover"
  fi

  # 실제 실행
  "/srv/ai/scripts/agent-router/run-${agent}" "$prompt"
}
```

#### Step D — 재인증 요청

`auth_expired` 감지 시 사용자에게 알림:

```bash
# Hermes를 통한 텔레그램/Slack 알림 (Phase 3 이후)
# 그 전까지는 Obsidian approval 노트 생성
cat > ~/obsidian-vault/bbw-wiki/00-inbox/requests/reauth-$(date +%Y%m%d-%H%M).md << EOF
---
id: reauth-$(date +%Y%m%d-%H%M)
status: pending
type: reauth_required
agent: $AGENT
failure_type: auth_expired
created: $(date +%Y-%m-%d)
requires_approval: true
---

# 재인증 요청: $AGENT

## 상황
- 에이전트: $AGENT
- 실패 유형: auth_expired
- 감지 시각: $(date -u +%Y-%m-%dT%H:%M:%SZ)
- 영향 작업: $TASK_ID

## 필요한 조치
1. API 키 또는 OAuth 토큰 재발급
2. ~/.bashrc 또는 /srv/ai/secrets/ 업데이트
3. \`update-health $AGENT healthy\` 실행
4. \`resume-task $TASK_ID\` 실행

## 재인증 후 재개 명령
\`\`\`bash
source ~/.bashrc
/srv/ai/scripts/agent-router/update-health $AGENT healthy
# 이후 Hermes에서 작업 재시작
\`\`\`
EOF
```

#### Step E — 재개

```bash
# 재인증 완료 후 실행
resume_task() {
  local task_id="$1"
  # tasks/failed/ → tasks/pending/ 이동
  mv /srv/ai/tasks/failed/${task_id}.md /srv/ai/tasks/pending/${task_id}.md
  # 작업 카드 status 업데이트
  /srv/ai/scripts/agent-router/append-log \
    --task-id "$task_id" \
    --agent "hermes" \
    --level "INFO" \
    --message "Task resumed after re-authentication."
  echo "작업 $task_id 재시작됨"
}
```

---

### 8-5. 에이전트별 만료 대응 정책 요약

#### Codex 만료 시

```yaml
# 60-agent-configs/routing/codex-failover.yaml
codex_failure_policy:
  auth_expired:
    action: user_approval_required
    message: "Codex 인증 만료. 코드 변경 작업을 자동으로 다른 에이전트에 위임하지 않음."
    blocked_auto_failover_to: [gemini, claude]

  quota_exceeded:
    action: queue_and_wait
    retry_after_minutes: 60
    notify: true

  provider_down:
    action: exponential_backoff
    max_retries: 3
    base_delay_seconds: 30

  model_unavailable:
    action: update_model_config
    fallback_model: "codex-mini-latest"
```

> **핵심 제약**: Codex 만료 시 Gemini가 코드 구현을 자동으로 맡는 경로는 존재하지 않는다. Gemini는 리서치 전용이며 코드 변경의 책임 경계를 넘지 않는다.

#### Claude Code 만료 시

```yaml
# 60-agent-configs/routing/claude-failover.yaml
claude_failure_policy:
  auth_expired:
    low_medium_risk:
      action: gemini_partial_substitute
      scope: [design_review, documentation, diff_review]
      notes: "최종 승인은 반드시 사용자"
    high_critical_risk:
      action: hard_block
      message: "Claude Code 만료 상태에서 High/Critical 작업은 자동 진행 금지."
      blocked_actions: [deploy, db_migration, auth_change, secret_access]
```

#### Gemini 만료 시

```yaml
# 60-agent-configs/routing/gemini-failover.yaml
# Gemini 역할 = Antigravity CLI 기반 리서치 에이전트 (run-gemini wrapper)
antigravity_failure_policy:
  auth_expired:
    primary_action: switch_to_api_key_backend   # BACKEND=api-key fallback 자동 시도
    if_api_key_also_fails:
      web_research:
        action: claude_websearch_or_user_approval
        preference: user_approval               # 토큰 비용 증가 인지 후 명시적 선택
      pdf_image_analysis:
        action: user_approval_required
        message: "멀티모달 분석은 자동 대체 없음. 사용자 수동 처리 필요."
      long_context_analysis:
        action: chunk_and_claude
        warning: "품질 저하 가능. 사용자 확인 권장."
  model_unavailable:
    action: update_model_config                 # GEMINI.md 모델명 수정 후 재시도
  legacy_gemini_cli:
    action: hard_block                          # gemini CLI 직접 호출 차단
    message: "Gemini CLI 2026-06-18 서비스 종료. BACKEND=antigravity 또는 api-key 사용."
```

---

## 9. 보강된 검증 및 백로그

### 복구 테스트 추가 항목 (§11.3 보강)

- [ ] `auth_expired` 시뮬레이션: 가짜 GEMINI_API_KEY 설정 → 만료 감지 로직 동작 확인
- [ ] `quota_exceeded` 시뮬레이션: 429 응답 mock → 지수 백오프 동작 확인
- [ ] `provider_down` 시뮬레이션: 존재하지 않는 엔드포인트 → 재시도 3회 후 failover 전환 확인
- [ ] Codex 만료 시 Gemini 자동 실행 차단 확인 (코드 변경 작업)
- [ ] Claude Code 만료 시 High risk 작업 `approval_required` 전환 확인
- [ ] Gemini 만료 시 리서치 작업이 user_approval 상태로 멈추는 확인
- [ ] 재인증 후 `resume_task` 명령으로 작업 재개 확인
- [ ] Health Registry 파일이 실패 직후 갱신되는지 확인

### 보안 테스트 추가 항목 (§11.2 보강)

- [ ] Codex 만료 상태에서 Gemini에 `"이 코드를 수정해줘"` 지시 시 차단 확인
- [ ] Claude Code 만료 상태에서 `git push`·배포 명령 자동 실행 차단 확인
- [ ] approval 노트 없이 High risk 작업 실행 시도 차단 확인
- [ ] Health Registry 파일 직접 수정 → `healthy`로 위조 후 실행 가능한지 검증

### P1 백로그 추가 항목

- [ ] `update-health` 스크립트 구현 및 run-gemini/run-codex/run-claude wrapper에 통합
- [ ] `run_with_failover` 함수 구현 및 classify-task와 연동
- [ ] `60-agent-configs/routing/` 아래 에이전트별 failover policy YAML 작성
- [ ] Health Registry 파일 초기화 스크립트 (`init-health`)
- [ ] 재인증 Obsidian 노트 자동 생성 로직 wrapper에 추가

### P2 백로그 추가 항목

- [ ] Health Registry 기반 Hermes 라우팅 전 상태 체크 통합
- [ ] `quota_exceeded` 자동 재시도 큐 (`tasks/waiting/`) 구현
- [ ] 에이전트 상태 대시보드 (§7 관측성, Health Registry JSON 기반 뷰)
- [ ] 재인증 알림 Hermes → 텔레그램 연동 (Phase 5 이후)

### 리스크 목록 추가 항목 (§7 보강)

**R10 — Codex 인증 만료 시 코드 변경 공백 (심각도: 높음, 확률: 중간)**
- Codex는 유일한 코드 구현 담당. 만료 시 코드 변경 작업 전면 중단.
- 대응: Failover Matrix에 따라 `user_approval_required` 전환. Gemini 자동 위임 코드 경로 미생성.

**R11 — Claude Code 만료 시 High risk 작업 묵시적 진행 (심각도: 높음, 확률: 낮음)**
- 리뷰어 없이 배포·DB 변경이 자동 진행될 위험.
- 대응: claude failover policy에서 high_critical_risk → hard_block 강제 적용.

**R12 — Gemini 만료 시 리서치 공백을 Claude Code가 임시 채워 토큰 과소비 (심각도: 중간, 확률: 높음)**
- Claude Code WebSearch 사용 시 토큰 비용 급증.
- 대응: gemini failover policy에서 web_research → `preference: user_approval`로 기본값 설정. 비용 인지 후 명시적 선택.

---

**작성 기준일**: 2026-06-11
**보강 일자**: 2026-06-11 (§8~9 Agent Health Registry & Failover 추가)
**다음 검토 시점**: Phase 0 완료 후 (2026-06-12), Gemini 전환일 전날(2026-06-17) 진행 상황 확인 필수
