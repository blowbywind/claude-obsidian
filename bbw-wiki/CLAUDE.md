# BBW Wiki — Agent Schema

> 이 파일은 LLM 에이전트(Claude Code)가 이 위키를 유지·관리하는 방법을 정의한다.
> 새 세션이 시작되면 반드시 이 파일을 먼저 읽고 지시를 따른다.

---

## 1. 목적

이 위키는 bbw(blowbywind@hnedu.co.kr)의 **세컨드 브레인**이다.
- 원본 소스(`raw/`)는 에이전트가 읽지만 절대 수정하지 않는다.
- 위키(`wiki/`)는 에이전트가 생성·유지하며, 사용자는 읽고 탐색한다.
- 지식은 질의마다 재발견되는 것이 아니라 **점진적으로 누적**된다.

---

## 2. 디렉토리 구조

```
bbw-wiki/
├── CLAUDE.md          # 이 파일 — 에이전트 스키마
├── index.md           # 전체 위키 카탈로그 (에이전트가 유지)
├── log.md             # 작업 이력 (에이전트가 유지, append-only)
├── raw/               # 원본 소스 (사용자가 추가, 에이전트는 읽기만)
│   └── assets/        # 다운로드된 이미지·첨부파일
└── wiki/
    ├── overview.md    # 전체 지식 합성 요약 (에이전트가 유지)
    ├── entities/      # 인물·조직·제품·서비스 페이지
    ├── concepts/      # 아이디어·프레임워크·기법 페이지
    ├── sources/       # 소스별 요약 페이지
    └── queries/       # 저장된 질의 결과 페이지
```

---

## 3. 페이지 형식

### 3-1. 공통 프론트매터

```yaml
---
title: 페이지 제목
type: entity | concept | source | query | overview
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [source-slug-1, source-slug-2]   # 이 페이지를 뒷받침하는 소스들
---
```

### 3-2. 소스 페이지 (`wiki/sources/`)

```markdown
---
title: 소스 제목
type: source
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
origin: URL 또는 파일 경로
author: 저자명
date_published: YYYY-MM-DD (알 수 있으면)
---

## 요약
(2–4문장 핵심 요약)

## 핵심 주장
- 주장 1
- 주장 2

## 연결된 개념
- [[concept/개념명]]

## 연결된 엔티티
- [[entity/엔티티명]]

## 메모
(불확실한 점, 논쟁점, 후속 조사 필요 사항)
```

### 3-3. 개념 페이지 (`wiki/concepts/`)

```markdown
---
title: 개념명
type: concept
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: []
---

## 정의
(핵심 정의 1–3문장)

## 상세
(필요한 만큼)

## 관련 개념
- [[concepts/관련개념]] — 관계 설명

## 관련 엔티티
- [[entities/엔티티명]]

## 출처
- [[sources/소스슬러그]]
```

### 3-4. 엔티티 페이지 (`wiki/entities/`)

```markdown
---
title: 엔티티명
type: entity
tags: [person | org | product | place]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: []
---

## 개요

## 주요 연결
- [[concepts/개념명]]
- [[entities/다른엔티티]]

## 출처
- [[sources/소스슬러그]]
```

---

## 4. 링크 규칙

- 모든 내부 링크는 `[[wiki/sources/slug]]`, `[[wiki/concepts/slug]]`, `[[wiki/entities/slug]]` 형식 사용
- 존재하지 않는 페이지 링크도 허용 — 나중에 채울 예정임을 나타냄
- 링크 텍스트는 파일명이 아닌 읽기 좋은 제목 사용: `[[wiki/concepts/rag|RAG]]`

---

## 5. 워크플로우

### 5-0. 소스 수집 방법 (클리핑)

사용자는 회사 컴퓨터에서 Obsidian Web Clipper(크롬 확장)로 웹 페이지를 클리핑한다.

1. Web Clipper로 페이지 클리핑 → `.md` 파일 로컬 다운로드
2. VSCode Remote SSH 탐색기에서 서버의 `raw/` 폴더에 우클릭 → **"Upload..."** → 파일 선택
3. Claude Code에 `raw/파일명.md 인제스트해줘` 라고 요청

### 5-1. 인제스트 (새 소스 추가)

사용자가 `raw/`에 파일을 추가하거나 URL을 제공하면:

1. **읽기**: 소스를 읽고 핵심 내용 파악
2. **논의**: 주요 시사점을 사용자와 간략히 공유하고 강조점 확인
3. **소스 페이지 생성**: `wiki/sources/<slug>.md` 작성
4. **개념 페이지 갱신**: 언급된 개념들의 기존 페이지 업데이트 또는 신규 생성
5. **엔티티 페이지 갱신**: 언급된 엔티티들의 기존 페이지 업데이트 또는 신규 생성
6. **index.md 갱신**: 새 페이지들을 카탈로그에 추가
7. **log.md 추가**: 인제스트 이력 한 줄 기록
8. **Git 동기화**: 인제스트 완료 후 반드시 실행:
   ```bash
   git add -A
   git commit -m "feat: ingest <소스 제목 요약>"
   git push
   ```

하나의 소스가 10–15개 위키 페이지를 건드릴 수 있다.

### 5-2. 질의 (Query)

사용자가 질문하면:

1. `index.md`를 읽어 관련 페이지 파악
2. 해당 페이지들을 읽어 답변 합성
3. 인용(출처 링크) 포함하여 답변
4. 가치 있는 분석은 `wiki/queries/<slug>.md`로 저장하고 index.md에 추가

### 5-3. 린트 (Wiki 건강 점검)

사용자가 "위키 점검" 또는 "lint" 요청 시:

- 서로 모순되는 페이지 클레임 탐색
- 최신 소스에 의해 구식이 된 내용 탐색
- 인바운드 링크 없는 고아 페이지 탐색
- 페이지가 없는 중요 개념 탐색 (링크만 있고 파일 없음)
- 데이터 공백 — 웹 검색으로 보완 가능한 항목 제안

---

## 6. 에이전트 행동 원칙

- `raw/` 디렉토리 내 파일은 절대 수정하지 않는다
- `raw/` 인제스트 완료 파일은 재읽기 금지 — wiki/에 이미 반영됨
- 위키 페이지 생성 시 항상 프론트매터를 포함한다
- 기존 페이지 수정 시 `updated:` 날짜를 갱신한다
- 기존 클레임과 충돌하는 새 정보는 메모 섹션에 명시한다
- `log.md`는 append-only — 기존 항목 수정 금지
- 답변 언어: 한국어 (코드·파일명·태그는 영어)
- 소스 슬러그 규칙: `YYYY-MM-DD-kebab-title` 형식
- wiki 페이지 200줄 초과 시 분할 검토
- 복잡한 질의 답변 후 가치 있으면 반드시 `wiki/queries/`에 저장

---

## 7. index.md 구조

```markdown
# BBW Wiki Index

## Sources
- [소스 제목](wiki/sources/slug.md) — 한 줄 요약

## Concepts
- [개념명](wiki/concepts/slug.md) — 한 줄 요약

## Entities
- [엔티티명](wiki/entities/slug.md) — 한 줄 요약

## Queries
- [질의 제목](wiki/queries/slug.md) — 한 줄 요약
```

---

## 8. log.md 구조

각 항목은 다음 형식을 따른다 (그레프 파싱 가능):

```
## [YYYY-MM-DD] <type> | <title>
<type>: ingest | query | lint | update
```

---

## 9. 세션 시작 절차

새 Claude Code 세션 시작 시:

1. 이 파일(`CLAUDE.md`) 읽기
2. `index.md` 읽기 — 현재 위키 상태 파악 (유일한 진입점)
3. `log.md` 마지막 5개 항목 확인 — 최근 작업 파악
4. 사용자 지시 대기
5. 태스크 관련 페이지만 선택 로드 (최대 3개)

**비용 상한 규칙 (반드시 준수):**
- `raw/` 인제스트 완료 파일 재읽기 금지 — 이미 wiki/에 반영됨
- 세션 시작 시 wiki 페이지 전체 로드 금지 — index.md로 필요 여부 판단 후 선택 로드
- queries/ 캐시 우선 확인 — 이미 답한 질문은 재분석 금지
