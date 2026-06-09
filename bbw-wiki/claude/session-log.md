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

