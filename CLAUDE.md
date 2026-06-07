# BBW Obsidian Vault — Agent Schema

> Claude Code가 이 볼트를 유지·관리하는 방법을 정의한다.
> 새 세션 시작 시 이 파일을 먼저 읽고, 이어서 `bbw-wiki/index.md`와 `bbw-wiki/log.md` 마지막 5개 항목을 확인한다.

---

## 1. 볼트 구조

```
obsidian-vault/
├── CLAUDE.md              # 이 파일 — 에이전트 스키마
└── bbw-wiki/
    ├── CLAUDE.md          # 위키 세부 스키마 (이 파일과 동기화)
    ├── index.md           # 전체 위키 카탈로그 (에이전트가 유지)
    ├── log.md             # 작업 이력 (에이전트가 유지, append-only)
    ├── raw/               # 원본 소스 (사용자가 추가, 에이전트는 읽기만)
    │   └── assets/
    └── wiki/
        ├── overview.md
        ├── entities/
        ├── concepts/
        ├── sources/
        └── queries/
```

---

## 2. 목적

이 위키는 bbw(blowbywind@hnedu.co.kr)의 **세컨드 브레인**이다.
- `raw/`는 에이전트가 읽지만 절대 수정하지 않는다.
- `wiki/`는 에이전트가 생성·유지하며, 사용자는 읽고 탐색한다.
- 지식은 질의마다 재발견되는 것이 아니라 **점진적으로 누적**된다.

---

## 3. 세션 시작 절차

1. 이 파일(`CLAUDE.md`) 읽기
2. `bbw-wiki/index.md` 읽기 — 현재 위키 상태 파악 (유일한 진입점)
3. `bbw-wiki/log.md` 마지막 5개 항목 확인 — 최근 작업 파악
4. 사용자 지시 대기
5. 태스크 관련 wiki 페이지만 선택 로드 (최대 3개)

**비용 상한 규칙:**
- `bbw-wiki/raw/` 인제스트 완료 파일 재읽기 금지
- queries/ 캐시 우선 확인 — 이미 답한 질문은 재분석 금지

---

## 4. 워크플로우

### 4-1. 소스 수집 방법 (클리핑)

1. Obsidian Web Clipper(크롬 확장)로 웹 페이지 클리핑 → `.md` 파일 로컬 저장
2. VSCode Remote SSH 탐색기에서 `bbw-wiki/raw/` 폴더에 우클릭 → **"Upload..."**
3. Claude Code에 `raw/파일명.md 인제스트해줘` 요청

### 4-2. 인제스트 (새 소스 추가)

`raw/`에 파일 추가 또는 URL 제공 시:

1. **읽기** — 소스 읽고 핵심 파악
2. **소스 페이지 생성** — `bbw-wiki/wiki/sources/<slug>.md`
3. **개념 페이지** — 언급된 개념 기존 페이지 갱신 또는 신규 생성
4. **엔티티 페이지** — 언급된 엔티티 기존 페이지 갱신 또는 신규 생성
5. **index.md 갱신** — 새 페이지 카탈로그 추가
6. **log.md 추가** — `## [YYYY-MM-DD] ingest | <제목>` 형식으로 append
7. **Git 동기화** — 인제스트 완료 후 반드시 아래 순서로 실행:
   ```bash
   git add -A
   git commit -m "feat: ingest <소스 제목 요약>"
   git push
   ```

### 4-3. 질의 (Query)

1. `bbw-wiki/index.md` 읽어 관련 페이지 파악
2. 해당 페이지들 읽어 답변 합성
3. 인용(출처 링크) 포함하여 답변
4. 가치 있는 분석은 `bbw-wiki/wiki/queries/<slug>.md` 저장 후 index.md 추가

### 4-4. 린트 (Wiki 건강 점검)

`위키 점검` 또는 `lint` 요청 시:
- 서로 모순되는 페이지 클레임 탐색
- 구식이 된 내용 탐색
- 인바운드 링크 없는 고아 페이지 탐색
- 페이지 없는 중요 개념(링크만 있고 파일 없음) 탐색
- 웹 검색으로 보완 가능한 데이터 공백 제안

---

## 5. 페이지 형식

### 공통 프론트매터

```yaml
---
title: 페이지 제목
type: entity | concept | source | query | overview
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [source-slug-1, source-slug-2]
---
```

### 소스 페이지 (`wiki/sources/`)

```markdown
---
title: 소스 제목
type: source
origin: URL 또는 파일 경로
author: 저자명
date_published: YYYY-MM-DD
---

## 요약
## 핵심 주장
## 연결된 개념
## 연결된 엔티티
## 메모
```

### 개념 페이지 (`wiki/concepts/`)

```markdown
---
title: 개념명
type: concept
---

## 정의
## 상세
## 관련 개념
## 관련 엔티티
## 출처
```

### 엔티티 페이지 (`wiki/entities/`)

```markdown
---
title: 엔티티명
type: entity
tags: [person | org | product | place]
---

## 개요
## 주요 연결
## 출처
```

---

## 6. 링크 규칙

- 내부 링크: `[[bbw-wiki/wiki/sources/slug]]`, `[[bbw-wiki/wiki/concepts/slug]]`, `[[bbw-wiki/wiki/entities/slug]]`
- 존재하지 않는 페이지 링크 허용 (나중에 채울 예정)
- 링크 텍스트는 파일명이 아닌 읽기 좋은 제목: `[[bbw-wiki/wiki/concepts/rag|RAG]]`

---

## 7. 에이전트 행동 원칙

- `raw/` 디렉토리 파일 절대 수정 금지
- 위키 페이지 생성 시 항상 프론트매터 포함
- 기존 페이지 수정 시 `updated:` 날짜 갱신
- 기존 클레임과 충돌하는 새 정보는 메모 섹션에 명시
- `log.md`는 append-only — 기존 항목 수정 금지
- 답변 언어: 한국어 (코드·파일명·태그는 영어)
- 소스 슬러그 규칙: `YYYY-MM-DD-kebab-title`
