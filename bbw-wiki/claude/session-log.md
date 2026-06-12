## 2026-06-11 (오후) — 서버 인프라 (Hermes 대시보드 접속 복구 시도)

### 완료
- **원인 진단** — `https://snowball.me.kr:9119/sessions` ERR_CONNECTION_TIMED_OUT 다단계 원인 파악
  - hermes / hermes-dashboard 컨테이너 미실행 → `docker compose up -d`로 재기동
  - ufw-docker가 port 9119 차단 → `sudo ufw-docker allow web_caddy 9119/tcp` 적용
  - Caddy(bridge network) → dashboard(127.0.0.1:19119) 도달 불가 → iptables DNAT 규칙 추가
- **iptables 백엔드 복구** — `iptables-persistent` 설치로 UFW 바이너리 제거 + nf_tables 전환 문제 발생
  - `update-alternatives --set iptables iptables-legacy` 로 legacy 복원
  - UFW 재설치 + `ufw enable` + SSH/80/443/9119 규칙 재적용
  - `ufw-docker install` + Docker 재시작 + `ufw-docker allow web_caddy 9119/tcp` 재적용
- **서버 사이드 규칙 확인 완료** — DNAT(9119→172.18.0.5:9119), ufw-user-forward ACCEPT, Caddy·hermes 정상

### 미해결 / 현재 상태
- **여전히 TIMED_OUT** — 서버 내부 iptables 규칙은 정상이나 외부 접속 불가
- 모바일(모바일 데이터)에서도 동일 → 회사 방화벽 문제 아님
- 유력 원인: **KT 공유기 포트포워딩 9119 → 172.30.1.92 규칙 소실** (이전 세션에서 추가했으나 공유기 재설정으로 사라진 것으로 추정)

### 배운 점 / 주의사항
- `apt install iptables-persistent` 설치 시 iptables 백엔드가 nf_tables로 전환될 수 있음 → UFW·ufw-docker 오동작
- UFW 바이너리 제거(`rc` 상태)되면 `ufw-docker allow` 실패 → UFW 재설치 필요
- Docker 재시작 시 컨테이너 IP 재할당 → ufw-docker 규칙 목적지 IP 변경 (`.3` → `.5`)
- `iptables -L DOCKER-USER` 는 비권한으로 읽기 불가 → PuTTY sudo로 직접 확인 필요

### 다음 할 일
- KT 공유기 포트포워딩 9119 → 172.30.1.92 재확인·재설정
- 장기적으로 Cloudflare Tunnel 또는 Tailscale 도입 검토 (포트포워딩 의존 제거)

---

## 2026-06-11 — hnedu_auth (보안 감사 + 전체 취약점 패치 + 배포)

### 완료

**버그 수정**
- **관리자 UI 무한 루프** — `hanjunsu@hnedu.co.kr`(권한 없음) 접속 시 `/login` ↔ `/employees` 무한 리다이렉트 버그
  - 원인: `login/page.tsx`가 `accessToken` 존재만으로 리다이렉트, admin 권한 미검증
  - 수정: `isAdminToken()` 공용 유틸 추가 (`admin-ui/lib/utils.ts`), 로그인 제출·세션 복원 양쪽에서 체크
  - 빌드 + 배포 완료 (`admin-ui/` → `public/admin/` → `scp` → 서버)

**보안 감사 (ultracode Workflow)**
- Workflow 스크립트 작성·실행 — Scout → 정적분석 → 실제 HTTP 공격 → 패치 → 검증 5단계
- 세션 한도 초과(parallel 5개+ 동시 실행) 문제 발생 → 배치 3개 분할로 재실행 성공
- 발견된 취약점: INJ 10개 + JWT 3개 총 13개

**취약점 패치 (전체 완료)**

| ID | 파일 | 수정 내용 |
|----|------|----------|
| INJ-001 | `auditLogs.ts` | action 파라미터 enum 화이트리스트 + Prisma 오브젝트 인젝션 차단 |
| INJ-002 | `employees.ts` | GET / querystring 스키마 추가 (status enum + departmentId integer) |
| INJ-003 | `roles.ts` | grantSchema — systemRoleId integer + additionalProperties: false |
| INJ-004 | `employees.ts` | 모든 `/:id` 라우트에 `idParamsSchema` 적용 (NaN 차단) |
| INJ-005 | `avatar.ts` | magic bytes 검증 추가 (jpg/png/webp 실제 헤더 확인) |
| INJ-006 | `avatar.ts` | `fs.unlink` 경로 탈출 방지 — `path.resolve` + allowedBase 경계 확인 (업로드·삭제 모두) |
| INJ-007 | `departments.ts` | PUT updateDeptSchema + explicit fields (오브젝트 인젝션 차단) |
| INJ-008 | `departments.ts` | POST 입력 스키마 추가 (name required, additionalProperties: false) |
| INJ-009 | `employeeService.ts` | `Object.values(EmployeeStatus)` 화이트리스트 검증 후 Prisma where 적용 |
| INJ-010 | `employees.ts` | 자기삭제 방지 `string === string` 타입 버그 → `actorId === numId` (number 비교) |
| JWT-007 | `jwt.ts` | access token 만료 `"1h"` → `"15m"` |
| XSS | 서버 파일 | `/public/avatars/1.jpg` SVG XSS 파일 제거 |

- JWT-009(로그아웃 후 블랙리스트): JWT-007 15m TTL로 실질적 완화, 블랙리스트 미구현 수용

**서버 배포**
- 변경 파일 6개 `scp` → 서버 동기화
- `pnpm build` (tsc) 성공
- `docker compose restart hnedu-auth` — 정상 기동 확인 (`{"status":"ok"}`)

### 배운 점 / 주의사항
- **Workflow parallel() 세션 한도**: `parallel([5개])` × 2 = 동시 12개 → 전체 실패. 한 번에 최대 3개, 초과 시 배치 분할 필수 → `active-rules.md` Rule 10 추가
- **agent() null 반환 가드**: 세션 한도로 에이전트 실패 시 null 반환 → `.counts` 접근 시 TypeError → 항상 null 가드 필수
- **path.join vs path.resolve 차이**: `path.join`은 `..` 포함 경로를 그대로 연결 → 경로 탈출 가능. 파일 삭제 전 반드시 `path.resolve` + `startsWith(allowedBase)` 검증 필요
- **Prisma enum 런타임 검증**: TypeScript 타입 캐스팅(`as EmployeeStatus`)은 런타임 무효 → `Object.values(EmployeeStatus).includes()` 명시적 검증 추가

---

## 2026-06-11 — 서버 인프라 (Firecrawl · Hermes · Caddy)

### 완료
- **Firecrawl Self-Hosted 설치 및 실행** — `/home/bbw/projects/firecrawl/` 클론, `.env` 생성, Docker Compose 빌드·기동 (api/redis/rabbitmq/postgres/playwright 5개 컨테이너)
- **OpenAI API 요금 차단** — Hermes `auth.json` openai-api 크레덴셜 제거, `config.yaml` provider `openai-codex`로 전환, Firecrawl `.env` OPENAI_API_KEY 주석 처리
- **Hermes Codex OAuth 인증** — `hermes model` 실행 → ChatGPT 비즈니스(팀) 계정 OAuth 연결 완료
- **Hermes 대시보드 외부 HTTPS 접속** — `https://snowball.me.kr:9119/` 개통
  - Hermes 내부 포트 9119 → 19119 변경 (0.0.0.0 바인딩 + --insecure)
  - Caddy 컨테이너 포트 9119 추가 (`/opt/web-infra/docker-compose.yml`)
  - Caddyfile에 `snowball.me.kr:9119` 블록 추가 (proxy → 172.18.0.1:19119)
  - UFW: `allow 9119/tcp`, `route allow in on eth0 to 172.18.0.3 port 9119`, `allow from 172.18.0.0/16 to any port 19119`
  - 공유기 포트포워딩 9119 추가
- **Hermes Slack 게이트웨이 연결** — `config.yaml` slack.allowed_channels `C0BAF1PH5JL` 설정, `hermes gateway run` 기동, `@hermes in workspace Snowball` 연결 확인

### 배운 점 / 주의사항
- ChatGPT 비즈니스 구독과 platform.openai.com API 크레딧은 완전히 별개 — Codex OAuth 사용 시 API 요금 미발생
- `docker compose restart`는 환경변수를 재주입하지 않음 → `--force-recreate` 필요
- Docker 컨테이너 → 호스트 포트 접근 시 호스트가 127.0.0.1 바인딩이면 컨테이너에서 접근 불가 → 0.0.0.0 바인딩 필요
- Docker 컨테이너 → 호스트 게이트웨이 IP는 `172.18.0.1` (docker network inspect로 확인)
- UFW + Docker 조합: 외부 포트 허용 외에 Docker 브리지 → 호스트 INPUT 규칙도 별도 필요
- 서버에서 자기 공인 IP로 curl 테스트 시 NAT 헤어핀 문제로 실패 → 외부 브라우저로 직접 확인

### 내일 할 일
- Hermes 게이트웨이·대시보드 systemd 서비스 등록 (서버 재부팅 시 자동 시작)
- Firecrawl AI 추출 기능 재검토 (OpenAI 크레딧 충전 or Ollama 연동)

---

## 2026-06-10 14:51 — hnedu_erp

**최근 커밋:**
- df86216 feat: 가상 DB 구축 — 비상연락망 기반 실제 직원 데이터 29명 반영
- 4baa52a 1차 검증 완료
- fe467b5 1차 검수 전 분기점

**변경 파일 (마지막 커밋):**
- `docs/layout-mockup.html`

---

## 2026-06-10 14:41 — hnedu_erp

**최근 커밋:**
- df86216 feat: 가상 DB 구축 — 비상연락망 기반 실제 직원 데이터 29명 반영
- 4baa52a 1차 검증 완료
- fe467b5 1차 검수 전 분기점

**변경 파일 (마지막 커밋):**
- `docs/layout-mockup.html`

---

## 2026-06-10 13:58 — hnedu_erp

**최근 커밋:**
- df86216 feat: 가상 DB 구축 — 비상연락망 기반 실제 직원 데이터 29명 반영
- 4baa52a 1차 검증 완료
- fe467b5 1차 검수 전 분기점

**변경 파일 (마지막 커밋):**
- `docs/layout-mockup.html`

---

## 2026-06-10 13:47 — hnedu_erp

**최근 커밋:**
- df86216 feat: 가상 DB 구축 — 비상연락망 기반 실제 직원 데이터 29명 반영
- 4baa52a 1차 검증 완료
- fe467b5 1차 검수 전 분기점

**변경 파일 (마지막 커밋):**
- `docs/layout-mockup.html`

---

## 2026-06-10 13:44 — hnedu_erp

**최근 커밋:**
- df86216 feat: 가상 DB 구축 — 비상연락망 기반 실제 직원 데이터 29명 반영
- 4baa52a 1차 검증 완료
- fe467b5 1차 검수 전 분기점

**변경 파일 (마지막 커밋):**
- `docs/layout-mockup.html`

---

## 2026-06-10 13:37 — .claude

**최근 커밋:**
- 9432c5f 회사 글러벌 설정
- cde3c61 Initial: Claude Code 글로벌 설정

**변경 파일 (마지막 커밋):**
- `.credentials.json`
- `backups/.claude.json.backup.1779419264612`
- `mcp-needs-auth-cache.json`

**미커밋 스테이지 파일:**
- `.credentials.json`
- `.last-cleanup`
- `backups/.claude.json.backup.1779377952644`
- `backups/.claude.json.backup.1779419264612`
- `ide/22655.lock`

---

## 2026-06-10 13:36 — .claude

**최근 커밋:**
- 9432c5f 회사 글러벌 설정
- cde3c61 Initial: Claude Code 글로벌 설정

**변경 파일 (마지막 커밋):**
- `.credentials.json`
- `backups/.claude.json.backup.1779419264612`
- `mcp-needs-auth-cache.json`

**미커밋 스테이지 파일:**
- `.credentials.json`
- `.last-cleanup`
- `backups/.claude.json.backup.1779377952644`
- `backups/.claude.json.backup.1779419264612`
- `ide/22655.lock`

---

## 2026-06-10 13:34 — .claude

**최근 커밋:**
- 9432c5f 회사 글러벌 설정
- cde3c61 Initial: Claude Code 글로벌 설정

**변경 파일 (마지막 커밋):**
- `.credentials.json`
- `backups/.claude.json.backup.1779419264612`
- `mcp-needs-auth-cache.json`

**미커밋 스테이지 파일:**
- `.credentials.json`
- `.last-cleanup`
- `backups/.claude.json.backup.1779377952644`
- `backups/.claude.json.backup.1779419264612`
- `ide/22655.lock`

---

## 2026-06-10 13:29 — 

_커밋 없음 — 세션 중 작업 내용을 "오늘 작업 노트에 기록해줘"로 추가 가능_

---

## 2026-06-10 13:28 — 

_커밋 없음 — 세션 중 작업 내용을 "오늘 작업 노트에 기록해줘"로 추가 가능_

---

## 2026-06-10 11:29 — .claude

**최근 커밋:**
- 9432c5f 회사 글러벌 설정
- cde3c61 Initial: Claude Code 글로벌 설정

**변경 파일 (마지막 커밋):**
- `.credentials.json`
- `backups/.claude.json.backup.1779419264612`
- `mcp-needs-auth-cache.json`

**미커밋 스테이지 파일:**
- `.credentials.json`
- `.last-cleanup`
- `backups/.claude.json.backup.1779377952644`
- `backups/.claude.json.backup.1779419264612`
- `ide/22655.lock`

---

## 2026-06-10 11:15 — .claude

**최근 커밋:**
- 9432c5f 회사 글러벌 설정
- cde3c61 Initial: Claude Code 글로벌 설정

**변경 파일 (마지막 커밋):**
- `.credentials.json`
- `backups/.claude.json.backup.1779419264612`
- `mcp-needs-auth-cache.json`

**미커밋 스테이지 파일:**
- `.credentials.json`
- `.last-cleanup`
- `backups/.claude.json.backup.1779377952644`
- `backups/.claude.json.backup.1779419264612`
- `ide/22655.lock`

---

## 2026-06-10 — .claude (Claude Code 진화 전략 + 하네스 개선)

### 완료
- **ultracode 진화 분석 워크플로우 실행** — 에이전트 7개(A·B·C·D·E·F + 종합), 116회 툴 호출, 258k 토큰으로 현황 진단·벤치마크·아키텍처·소통 전략 분석
- **`docs/evolution-report.md` 생성** — 현황 진단·로드맵·소통 가이드 포함 종합 보고서
- **Phase 0 즉시 적용** (워크플로우 자동 처리)
  - `memory/agent-architecture.md` 신규 생성 — 에이전트 3계층 구조·라우팅 매트릭스·품질 게이트 조건
  - `memory/active-rules.md` 번호 순서 수정 + Rule 5(UI 작업 전 파일시스템 확인) + Rule 6(@멘션 금지·5k줄 세션 분리·/compact 타이밍) 추가
- **Phase 1~2 순차 적용** (9건)
  - `agents/evaluator-strict.md` — 공통 통과 기준 3항목(빌드 성공·타입체크·린트) 추가
  - `CLAUDE.md` — 계획 원칙에 자동처리 허용/인간 확인 기준 추가, 위키 3규칙 1·3번 추가, 서버 디버깅 참조 파일 보완
  - `memory/lessons.md` — [2026-06-04] 항목 승격 완료 표시
  - `agents/research-agent.md` 신규 생성 — WebSearch/WebFetch 전담 에이전트
  - `hooks/pre-tool-use/block-dangerous.sh` — rm 허용 범위 주석 보완
  - `obsidian-vault/bbw-wiki/claude/decisions/README.md` — ADR 체크리스트에 active-rules 반영 여부 Y/N 항목 추가
- **헤르메스 에이전트 도입 이점·단점 분석** — 위키 리서치 자료 기반 정리

### 배운 점 / 주의사항
- **ultracode 목적어 확인 필수**: `ultracode 프롬프트 만들어줘`는 실행이 아닌 문서 생성 — CLAUDE.md 원칙 0번(사용자 의도 최우선) 적용
- **자동 모드 분류기**: CLAUDE.md 직접 편집은 "권한 확장형 자기 수정"으로 차단됨 → 사용자가 직접 편집하거나 별도 승인 필요
- **ultracode ROI 기준**: 병렬 분해 가능 + 완료 기준 명확 + 30분 이상 소요 + 서브태스크 의존성 낮음 — 3개 이상 해당할 때 사용
- **헤르메스 핵심 교훈**: 철학(역할 분리·위키 공유 메모리)은 채택, 규모(10명 팀·크론 루프·외부 API)는 1인 개발자 규모 초과로 보류
- **@파일멘션 금지 실효성 확인**: active-rules Rule 6로 세션 시작 시 자동 주입됨

### 내일 할 일
- hnedu_erp Phase 1 개발환경 구성 재개 (GitHub 레포 구조, Docker Compose 초안)
- evolution-report.md Phase 2 잔여 항목 검토 (`save-session.sh` 멀티 세션 기록, `lessons.md` 보관 정책)

---

## 2026-06-10 09:18 — .claude

_작업 내용을 여기에 기록하려면 세션 중 "오늘 작업 노트에 기록해줘"라고 하세요._

---

## 2026-06-10 08:03 — obsidian-vault

_작업 내용을 여기에 기록하려면 세션 중 "오늘 작업 노트에 기록해줘"라고 하세요._

---

## 2026-06-10 06:41 — hnedu_erp

_작업 내용을 여기에 기록하려면 세션 중 "오늘 작업 노트에 기록해줘"라고 하세요._

---

## 2026-06-10 — hnedu_erp (컨텍스트 소진 원인 분석)

### 완료
- **세션 트랜스크립트 분석** — `5405aa58.jsonl` (448턴, 6시간 40분) 파싱
- **토큰 소진 원인 5가지 특정**: `@파일멘션` 대형 파일 로드 → 세션 누적 → 반복 읽기 → autoCompactThreshold 0.8 → 훅 전문 주입 순

### 핵심 발견
- **방아쇠**: `@prototype/index.html` 멘션 시점(15:20)에 이미 컨텍스트 147k 누적 → 5383줄 파일 로드로 162k 돌파
- **압축 기준**: `autoCompactThreshold: 0.8` = 200k × 80% = 160k에서 자동 압축 발동
- **압축 시각**: 21:15 (167k 도달 직후) — 이후 39k로 축소, 요약으로 대체
- **이미 개선된 항목**: INDEX.md 경량 주입으로 훅 부담 감소

### 재발 방지 규칙
- 5k줄 이상 대형 파일 작업 시작 전 **새 세션** 열기
- `@파일멘션` 대신 경로 텍스트로 언급 (자동 로드 방지)
- ADR 기록: [2026-06-10-context-exhaustion](decisions/2026-06-10-context-exhaustion.md)

---

## 2026-06-10 — hnedu_erp (Claude Code × Obsidian 연동 고도화)

### 완료
- **renderNotices/initNotices 이중 구조 통합** — `DB.announcements` 단일 소스, `initNotices()`만 유지. `render.js`에서 `renderNotices()` 완전 제거
- **웹리서치: Claude Code × Obsidian 최적 활용법** — MCP 서버, 역할 분리 전략, ADR frontmatter 표준 등 상세 분석
- **obsidian-mcp 설치 및 MCP 서버 설정** — `~/.local/lib/node_modules/obsidian-mcp`, `~/.claude/settings.json` 등록, `read-note`/`search-vault` 동작 확인
- **`claude/INDEX.md` 생성** — 프로젝트 8개 + ADR 5개 한 줄 요약 인덱스
- **ADR frontmatter 표준화** — 기존 5개 파일에 `date/project/status/tags` 추가 (Dataview 쿼리 가능)
- **`load-context.sh` 개선** — 전문 주입 → INDEX 요약 + 최근 ADR 2개 + 프로젝트 노트 3단계 구조로 경량화
- **`save-session.sh` 개선** — 당일 동일 레포 중복 빈 항목 방지 로직 추가, 기존 빈 항목 41개 일괄 제거
- **프로젝트 노트 현행화** — `hnedu_erp.md` 모듈화 구조·경로·히스토리 반영
- **`docs/리포트.md` 작성** — 전체 작업 + 웹리서치 결과 상세 기록

### 배운 점 / 주의사항
- `obsidian-mcp`은 REST API 방식이 아닌 **볼트 경로 직접 접근** — Obsidian이 실행 중이 아니어도 동작
- `read-note` 파라미터는 `path`가 아니라 `filename` + `folder` 분리 방식
- Stop 훅 시점엔 Claude가 종료 중이라 LLM 요약 자동 생성 불가 — `/daily-log` 수동 실행이 현실적 최선
- 3-레이어 메모리: TodoWrite(즉시) → `.claude/memory/`(규칙) → Obsidian(지식) 역할 명확히 분리

### 내일 할 일
- Phase 1 개발환경 구성 시작 (GitHub 레포 `/client` `/server` `/db` 구조)
- Docker Compose 초안 (ERP API + PostgreSQL + hnedu-auth)

---

## 2026-06-09 — hnedu_erp (prototype 모듈화 + 위키 연동)

### 완료
- 공지사항 스트립 페이지네이션 — 좌우 버튼, 3개/페이지, `noticeNav()` 구현
- Spotlight 전역 검색 활성화 — Ctrl+K 단축키, `DB.tasks` · `DB.employees` · `DB.calendarEvents` 대상
- `docs/layout-mockup.html` → `prototype/index.html` 이동 및 전체 참조 업데이트
- `docs/기획서.md` → `docs/PLAN.md` 개명 및 전체 참조 업데이트
- 모노리식 HTML(5383줄) → `css/app.css` + `js/*.js` 8파일로 모듈화 (글로벌 스코프 유지)
- `openTaskDetailById` 버그 수정 — spotlight에서 `openTaskDetail(task.id)` 잘못 호출하던 것 수정
- 모듈화 참조 무결성 검증 완료 — onclick 핸들러 75개 전부 정상 참조 확인
- 옵시디언 위키 연동 업데이트 (프로젝트 노트 현행화, ADR 신규 기록)

### 배운 점 / 주의사항
- JS 모듈화 시 ES module 사용 불가 (onclick 핸들러가 글로벌 스코프 의존) — `type="module"` 사용 시 모든 onclick 핸들러 깨짐
- 스크립트 로드 순서 강제: db → utils → render → calendar → tasks → mail → forms → app (의존성 순서 엄수)
- `renderNotices()`(render.js, DB 기반)와 `initNotices()`(app.js, 하드코딩) 두 시스템이 동일한 `#noticesStrip`에 쓰는 구조적 부채 존재 — 추후 통합 필요

### 내일 할 일
- Phase 1 개발환경 구성 시작 (GitHub 레포 구조 설정, Docker Compose 초안)
- `renderNotices` / `initNotices` 중복 시스템 통합 (DB.announcements 단일 소스로)

---

# Claude 세션 로그

> 세션 종료 시 자동 기록됩니다.

---

