---
title: "bbw_ebook — eBook Viewer"
id: "P-06"
status: "기획중"
phase: "Phase 기획"
stack: [Vanilla HTML, CSS, JavaScript]
created: 2026-06-13
updated: 2026-06-08
summary: "사용자 개발 승인 전까지 분석·설계만 진행하는 정적 HTML eBook viewer 프로토타입 프로젝트"
---

## 현재 상태

- **Phase**: 기획·설계 단계
- **진행 상황**: 정적 eBook viewer. 서버·DB·빌드 도구 없음.

## 서버 / 인프라

| 항목 | 값 |
|------|-----|
| 배포 형태 | 정적 HTML (서버 없음) |
| 진입점 | `prototype/index.html` |

## 스택

- 언어: Vanilla HTML/CSS/JavaScript
- 서버: 없음
- 빌드: 없음

## 에이전트 허용 범위

| 에이전트 | 허용 | 금지 |
|---------|------|------|
| Claude Code | 분석·계획·화면 설계·수정안 제시 | **Dev Gate 전 코드 작성·수정 일체 금지** |
| Codex | **Dev Gate 전 금지** | |
| agy | 리서치만 | 코드 수정 불가 |

## Dev Gate

> **Critical**: 사용자가 명시적으로 "개발해줘"라고 말하기 전에는 코드나 파일을 작성·수정하지 않는다.
> 그 전까지는 분석, 계획, 화면 설계, 수정안 제시만 수행.

```
활성화 조건: 사용자가 명시적으로 "개발해줘" 발화
```

## 위험 구역

- `references/`는 읽기만, 임의 수정 금지 (엔진 동작 기준)
- `backup/CLAUDE.md`에 상세 규칙 있음 — 작업 전 반드시 읽기

## 자주 쓰는 명령

```bash
# 프로토타입 확인
open /home/bbw/projects/bbw_ebook/prototype/index.html

# 상세 규칙 확인 (작업 전 필수)
cat /home/bbw/projects/bbw_ebook/backup/CLAUDE.md
```

## 최근 작업

- 기획·설계 단계

## 다음 작업

- [ ] 사용자 "개발해줘" 승인 후 구현 시작
