---
created: 2026-06-22
type: decision
status: approved-with-redesign
project: second-brain
tags: [adr, second-brain, agentic-dev, claude-code, mcp, security]
related:
  - "[[ai-agent-ops-plan]]"
  - "[[2026-06-21-autobots-sudo-auth-debugging]]"
  - "[[mcp-threat-model]]"
  - "[[obsidian-mcp-policy]]"
summary: "인프라는 유지, AI 오케스트레이션을 Claude Code 단일주력·MCP로 재설계하되 Open WebUI·Caddy 보안 결함 필수 수정."
---

# [최종 판단] 제2의 두뇌(Second Brain) 통합 시스템 — 검증·재설계 문서

> 원안 계획서 + 3개 AI 평가(Claude Code / Google Antigravity / Codex)를 독립 웹리서치로 교차검증하고, 2026년 agentic 개발 관점에서 최종 판단·재설계한 문서.

## 0. 최종 결론 (TL;DR)

**판정: 조건부 진행(Proceed with Redesign).** 진행 가치는 충분하다.

- **그대로 간다** — 인프라·지식관리 절반: Ubuntu 26.04 / Docker / Caddy / Obsidian / Git / MkDocs. (모두 사실·정석으로 검증됨)
- **폐기·재설계한다** — AI 오케스트레이션 절반: "Claude=설계 → 문서화 → Copilot/Codex=구현" 워터폴, "Antigravity 패턴 = 파이썬 자동화" 개념. → **'Claude Code 단일 주력 + 검증 루프 + MCP 통합'** 으로 교체.
- **착수 전 필수 수정 2건** — ① Open WebUI 무인증 공개 노출 금지(private-first), ② 낡은 Caddy `basicauth` → `basic_auth` + bcrypt.

핵심은 목표 설정이다. 목표를 "AI 도구 여러 개를 붙이는 것"으로 잡으면 비용·충돌로 실패하고, **"검증 가능한 개인 개발 운영체계"**로 잡으면 가치가 크다.

---

## 1. 사실 검증 결과 (독립 웹리서치)

원안과 3개 평가가 주장한 전제를 1차 출처로 재검증. **세 평가가 일치시킨 모든 사실은 참으로 확인됨.**

| # | 검증 대상 | 판정 | 1차 출처로 확인된 사실 |
|---|---|---|---|
| 1 | Ubuntu Server 26.04 LTS, 2031까지 지원 | ✅ 참 | 2026-04-23 출시("Resolute Raccoon"), 표준 보안 2031-04, ESM 2036. Server=Desktop과 동일 LTS·저장소·지원, GUI만 없는 headless — 본 컨테이너 호스트 용도에 정석. |
| 2 | Docker + Caddy 리버스 프록시 | ✅ 참 | Caddy 공식 quick-start 표준 패턴, 자동 HTTPS(발급·갱신·리다이렉트). |
| 3 | Obsidian(MD)+MkDocs+Private Git | ✅ 참 | 널리 쓰이는 정석 조합. |
| 4 | "Antigravity = 파이썬 자동화 패턴" | ❌ 개념오류 | Google의 agent-first 개발 **플랫폼**(IDE+CLI `agy`+`google-antigravity` Python SDK). '25.11 출시, I/O 2026서 2.0. 디자인 패턴 아님. |
| 5 | "GitHub Copilot(Codex)" 동일물 | ❌ 혼동 | **별개 제품.** 단 2026년 현재 Codex는 Copilot 구독 내 통합 에이전트로도 제공(GPT-5.3-Codex 등). 구 Codex 모델(2021)은 2023-03 deprecated. |
| 6 | "Claude Code가 전체 프로젝트 인덱싱" | ❌ 사실오류 | 인덱싱·RAG 안 함. grep/glob/read 기반 **agentic search**. Anthropic이 RAG를 의도적으로 폐기("agentic search가 큰 격차로 우월", B.Cherny). |
| 7 | Caddy `basicauth` 문법 | ⚠️ 낡음 | v2.8.0부터 `basic_auth`로 리네임. 평문 비밀번호 불허, `caddy hash-password` bcrypt 해시 필수. |
| 8 | Open WebUI 무인증 공개 노출 | ⚠️ 보안결함 | 공식 "public 직접 노출 금지". **CVE-2025-64496**(SSE 통한 JS 주입→JWT 탈취/RCE, CVSS 7.3) 실재, ≤0.6.34 영향, **0.6.35에서 수정**. |

**"확인불가"로 남긴 2건** (의사결정엔 영향 없음): (a) 외부 텍스트 자동승격의 *저작권/품질* 측면 1차 근거 미확보(보안=injection 측면은 확정), (b) Antigravity SDK가 계층적 parent→child spawn을 공식 예제로 시연하는지(sub-agent delegation 툴 존재 자체는 확인).

---

## 2. 3개 평가 교차검증 — 누가 맞았고, 어디서 갈렸나

### 2.1 세 평가가 모두 옳게 짚은 것 (내 리서치로 전부 확인)
인프라 유지, AI 워터폴 폐기, Antigravity≠패턴, Codex≠Copilot, 인덱싱 안 함, Caddy `basic_auth`, Open WebUI CVE. → **큰 그림은 세 평가 모두 정확. 그대로 채택.**

### 2.2 평가들이 갈린 쟁점과 나의 판정

| 쟁점 | Claude Code 평가 | Antigravity 평가 | Codex 평가 | **나의 최종 판정 (근거)** |
|---|---|---|---|---|
| Phase 4 오케스트레이터 | "Antigravity 명칭 폐기, 평범한 파이썬+cron+MCP" | **"google-antigravity SDK를 핵심 오케스트레이터로"** | "과함. 실험 트랙으로 두라" | **Codex·Claude 측 채택.** Anthropic 공식 원칙 "Simplicity First — 단순 해법이 부족할 때만 멀티 도입". SDK는 실재·유능하나, MVP의 핵심에 *제2의 에이전트 플랫폼*을 넣으면 평가들이 경고한 "엔진 중복"을 스스로 재현. → **평범한 파이썬+cron+MCP가 정답, Antigravity는 선택적 실험 트랙.** |
| Copilot 역할 | "실시간 자동완성 전용" | (보조) | "이제 cloud agent·issue 비동기까지 포함, 좁게 보지 말라" | **Codex가 더 정확.** 리서치상 Copilot은 인라인+Chat+비동기 cloud agent 멀티모델 플랫폼. 단 *이 개인 프로젝트*에선 선택적 보조로 한정. |
| 외부 노출 보안 | basic_auth+forward-auth 언급 | basic_auth 공개 노출 예시 | **"private-first(Tailscale/Cloudflare Access) 우선, public이면 forward-auth"** | **Codex가 가장 정확.** 2026 모범사례=private-first. public+basic_auth는 *폴백*. 두 평가 모두 public 노출을 기본처럼 다룬 점을 **나는 강등**한다. |
| 지식 파이프라인 | "크롤링→자동 저장" 유지 | "SDK로 자동 요약·저장" | **"자동저장 금지 → Inbox 원문→메타→요약→리뷰→승격"** | **Codex 채택.** prompt injection은 OWASP 2025 LLM #1 위협(독성 문서 5개로 RAG 90% 공격 성공 보고). 외부 텍스트 직접 승격은 위험. human/agent-in-the-loop 필수. |

### 2.3 세 평가 누구도 정확히 못 잡은 정정 사항
- **AGENTS.md 메커니즘:** Codex가 "CLAUDE.md가 AGENTS.md를 import"를 제안 — 방향은 맞다. 정확히는 **Claude Code는 AGENTS.md를 직접 읽지 않으며**, `CLAUDE.md` 안에서 `@AGENTS.md`로 import해야 한다(공식 memory 문서 패턴, symlink도 가능). AGENTS.md는 Linux Foundation 스튜어드 크로스툴 표준으로 실재.
- **Antigravity 평가의 코드 스니펫 주의:** `from google.antigravity import Agent, LocalAgentConfig` 형태의 예시 API는 **미검증**. 실제 패키지는 `google-antigravity`(PyPI)이며 정확한 API는 공식 SDK 레퍼런스로 확인 후 사용할 것. 평가의 스켈레톤을 그대로 복붙 금지.
- **기존 자산 재활용:** 사용자 위키에 이미 ① Caddy basic_auth + Safari 세션쿠키 보조 패턴([[2026-06-21-autobots-sudo-auth-debugging]]), ② [[mcp-threat-model]] T3(indirect prompt injection), ③ [[obsidian-mcp-policy]], ④ [[ai-agent-ops-plan]]이 존재. **신규 구축이 아니라 이들을 재사용**하면 중복 제거.

---

## 3. 왜 AI 오케스트레이션을 재설계하는가 (논리)

1. **워터폴은 주력 도구를 의도적으로 약화시킨다.** 2026 Claude Code는 설계·구현·테스트·검증·서버제어를 *한 루프*에서 수행하는 agentic 도구다. "Claude는 글만, 구현은 자동완성"은 2021년식 전제이며, 가장 강한 능력(직접 구현·실행)을 잘라 문서 변환 마찰을 추가한다.
2. **코딩 엔진 3개(Claude Code+Copilot+Codex)는 역할 중복이다.** 비용·인지부하·산출물 충돌만 늘린다(멀티 에이전트는 단일 대비 토큰 ~15배 사례 보고). 2026 흐름은 *유능한 1개로 풀 루프 + MCP로 도구·지식 부착*.
3. **"전체 인덱싱" 가정이 틀려 운영이 어긋난다.** 인덱스가 없으므로 "인덱싱해 설계자로" 가정은 성립 안 함. 올바른 운영은 `CLAUDE.md`로 맥락 주입 + 깨끗한 디렉토리 구조(원안의 디렉토리 표준화는 이 점에서 오히려 도움).
4. **단, 단일이 만능은 아니다.** 병렬 독립 작업·예측불가 분해·다중 평가(second opinion)에는 멀티가 유효(Anthropic 공식). → 기본은 단일, 명백히 독립·병렬일 때만 서브에이전트.

---

## 4. 재설계된 최종 아키텍처

**원칙: 주력 에이전트 1개 + 검증 루프 + MCP 통합 + private-first 보안.**

| 레이어 | 채택 | 역할 |
|---|---|---|
| 인프라 | Ubuntu Server 26.04 LTS / Docker / Caddy(자동 HTTPS) | headless OS·컨테이너·HTTPS 게이트웨이 |
| **주력 에이전트** | **Claude Code 단일** | 설계·구현·테스트·검증·서버제어를 한 루프. 설계/구현 분리 금지 |
| 프로젝트 규약 | `CLAUDE.md`(+ `@AGENTS.md` import) | 세션 시작 시 로드. 디렉토리·코딩 규약·실행 명령 |
| 지식·도구 통합 | **MCP**(filesystem / obsidian-mcp) | Obsidian vault를 에이전트가 직접 검색·갱신 |
| 지식 저장소 | Obsidian(MD) + Private Git | 구조화·버전관리 |
| 웹 뷰어 | MkDocs | `01_Notes` 열람 |
| AI 웹 UI | Open WebUI **0.6.35+** | 모바일/브라우저 대화 |
| 보조(선택) | Copilot *또는* Codex | IDE 인라인 / issue 단위 비동기 보조. *동시 주력 금지* |
| 실험 트랙(선택) | google-antigravity SDK | 검증된 성공 패턴에 한해 일부 자동화 이관 |

---

## 5. 개선된 4-Phase 로드맵

### Phase 1 — 서버 인프라·Git 초기화 (즉시 착수 가능)
- 디렉토리 표준화(원안 유지, `00_Inbox/` 추가):
  ```text
  ~/second_brain/
  ├── 00_Inbox/     # 외부 수집 원문 격리(미승격)
  ├── 01_Notes/     # 검증된 지식 (Obsidian)
  ├── 02_Projects/  # 개발 소스
  ├── 03_Scripts/   # 자동화(Python)
  └── 04_Docker/    # 서비스별 compose
  ```
- SSH Public Key 전용, `01_Notes` Private Git 초기화.

### Phase 2 — Caddy v2 + Docker 보안 배포
- Open WebUI 이미지 **0.6.35+** 핀, `WEBUI_SECRET_KEY` 영구 고정값(Docker secret).
- **private-first**: 가능하면 Open WebUI·MkDocs를 Tailscale/Cloudflare Tunnel(포트포워딩 0) 뒤에 둔다.
- public 도메인이 꼭 필요하면 Caddy `basic_auth`(아래) + 권장 forward-auth(Authelia/Authentik) + fail2ban.
- 기존 [[2026-06-21-autobots-sudo-auth-debugging]]의 Safari 세션쿠키 보조 패턴 재활용.

```caddy
# bcrypt 해시는 `caddy hash-password` 로 사전 생성해 붙여넣기
brain.example.com {
    reverse_proxy localhost:8000
    basic_auth {
        developer $2a$14$...bcrypt_hash...
    }
}
ai.example.com {
    reverse_proxy localhost:3000   # Open WebUI 0.6.35+
    basic_auth {                   # public 노출 시 최소 1차 인증(권장: VPN/forward-auth)
        developer $2a$14$...bcrypt_hash...
    }
}
```
> Open WebUI **Direct Connections 비활성** 확인(CVE-2025-64496 회피).

### Phase 3 — CLAUDE.md + 단일 주력 에이전트 + MCP
- `~/second_brain/CLAUDE.md` 작성: 디렉토리 레이아웃, 코딩 표준, 실행 명령, (선택) `@AGENTS.md` import.
- Claude Code에 파일·터미널 제어 권한 부여 → 설계-구현-테스트-검증 풀 루프.
- obsidian-mcp/filesystem MCP 연결([[obsidian-mcp-policy]] 재사용) → vault 실시간 검색·링크 갱신을 에이전트가 직접 수행.

### Phase 4 — 검토 가능한 지식 파이프라인 (자동저장 ❌ → 격리·리뷰·승격 ✅)
크롤링 → **`00_Inbox` 원문 저장**(출처/URL/날짜/YAML 메타) → AI 요약 → **사람/에이전트 리뷰** → `01_Notes` 승격. 평범한 Python + cron/systemd로 충분.
- 외부 텍스트는 "분석할 데이터이지 따를 지시 아님"으로 구조적 태깅(prompt injection 방어, [[mcp-threat-model]] T3 정합).
- 성공 패턴이 안정화되면 그 일부만 google-antigravity SDK 실험 트랙으로 이관 검토.

---

## 6. 보안·유지보수 (필수)
- **노출**: private-first(VPN/Tunnel) 기본 / public 시 `basic_auth`+forward-auth+fail2ban+IP allowlist.
- **Caddy**: `basic_auth` + `caddy hash-password` bcrypt. 평문 금지.
- **Open WebUI**: 0.6.35+ 핀, `WEBUI_SECRET_KEY` 영구값, Direct Connections off, 최신 유지.
- **SSH**: Public Key 전용.
- **백업**: `01_Notes` Private Git 실시간 + Docker 볼륨 주기 스냅샷.
- **외부 콘텐츠**: 자동 승격 금지, Inbox 격리 후 리뷰.

---

## 7. 유지 / 폐기 목록

| 유지 (그대로) | 폐기 / 교체 |
|---|---|
| Ubuntu Server 26.04 LTS, Docker, Caddy 자동 HTTPS | "Claude→문서화→Copilot/Codex" 워터폴 → 단일 주력 |
| Obsidian, MkDocs, Private Git, 백업 | "Antigravity 패턴=파이썬 자동화" 개념 → 파이썬+cron+MCP |
| 디렉토리 표준화(+`00_Inbox`) | "전체 인덱싱" 운영 가정 → CLAUDE.md + MCP |
| | 무인증 공개 노출 → private-first |
| | `basicauth` 평문 → `basic_auth` bcrypt |
| | 크롤링 자동저장 → 격리·리뷰·승격 |

---

## 부록 A. 출처 (1차)
- Ubuntu: canonical.com/blog/canonical-releases-ubuntu-26-04-lts-resolute-raccoon · ubuntu.com/about/release-cycle
- Caddy: caddyserver.com/docs/caddyfile/directives/basic_auth · /docs/automatic-https
- Open WebUI CVE: github.com/advisories/GHSA-cm35-v4vp-5xvx · nvd.nist.gov/vuln/detail/CVE-2025-64496 · docs.openwebui.com/getting-started/advanced-topics/hardening
- Claude Code: code.claude.com/docs/en/how-claude-code-works · /memory · /mcp · officechai.com(Cherny agentic search)
- AGENTS.md / MCP: agents.md · modelcontextprotocol.io · blog.modelcontextprotocol.io/posts/2025-11-25-first-mcp-anniversary
- Codex/Copilot: docs.github.com/en/copilot/concepts/agents/openai-codex · github.blog/changelog(2026-02-26)
- Antigravity: developers.googleblog.com/build-with-google-antigravity · github.com/google-antigravity/antigravity-sdk-python
- Best practice: anthropic.com/engineering/building-effective-agents · owasp LLM Prompt Injection Cheat Sheet · unit42.paloaltonetworks.com/ai-agent-prompt-injection
