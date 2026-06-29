---
title: CLAUDE.md
type: concept
tags: [claude-code, configuration, memory]
created: 2026-06-05
updated: 2026-06-07
sources: [2026-06-05-how-claude-code-works, 2026-06-05-claude-code-7steps-mastery, 2026-06-07-ainow-claude-code-master-guide, 2026-06-07-harness-engineering-guide]
summary: "Claude Code의 영속 설정 파일로 프로젝트별 컨벤션·지시를 저장하고 글로벌·프로젝트·디렉토리 수준으로 적용 범위를 구분한다."
---

## 정의

Claude Code가 세션 시작 시 자동으로 로드하는 마크다운 파일. 프로젝트별 영구 지시, 컨벤션, 컨텍스트를 저장하는 공간. 대화 이력은 세션 종료 시 사라지지만 CLAUDE.md는 영속된다.

## 종류

| 위치 | 범위 |
|------|------|
| `~/.claude/CLAUDE.md` | 모든 프로젝트에 적용 (글로벌) |
| `프로젝트루트/CLAUDE.md` | 해당 프로젝트에만 적용 |
| 하위 디렉토리 `CLAUDE.md` | 해당 디렉토리와 하위에만 적용 |

## 언제 쓰는가

- 코딩 컨벤션, 금지 사항, 워크플로우 지시
- 자주 참조하는 파일 경로, 명령어
- 에이전트 행동 원칙 (bbw-wiki의 경우: 인제스트 워크플로, 링크 규칙 등)
- `Compact Instructions` 섹션: 컨텍스트 컴팩션 시 보존할 내용 지정

## 작성 원칙

- **글로벌 파일에는 100줄 핵심만**: Claude Code 창시자·해커톤 우승자·커뮤니티 공통 권장. 너무 많은 내용 넣지 말 것
- **프로젝트별 세분화**: 글로벌에는 공통 규칙만, 각 프로젝트 폴더에 목적별 CLAUDE.md 별도 생성
- 외부에서 만들어 놓은 베스트 프랙티스 템플릿(GitHub)을 가져다 커스터마이징하는 방식도 효과적
- **하네스 관점**: CLAUDE.md는 [[wiki/concepts/harness-engineering|하네스 엔지니어링]]의 컨텍스트 엔지니어링 레이어. 에이전트 실수마다 방지 규칙을 추가하는 [[wiki/concepts/boris-self-learning-loop|자기학습 루프]]의 저장소

## bbw에서의 활용

- `~/.claude/CLAUDE.md`: 전역 행동 원칙, 스택 정보, 안전 규칙
- `bbw-wiki/CLAUDE.md`: 위키 에이전트 스키마 (이 파일이 바로 CLAUDE.md의 실사례)

## 관련 개념

- [[wiki/concepts/context-window|컨텍스트 윈도우]] — CLAUDE.md는 세션 시작 시 컨텍스트에 로드됨
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 스키마 파일로서의 CLAUDE.md

## 관련 엔티티

- [[wiki/entities/claude-code|Claude Code]]

## 출처

- [[wiki/sources/2026-06-05-how-claude-code-works]]
- [[wiki/sources/2026-06-05-claude-code-7steps-mastery]]
