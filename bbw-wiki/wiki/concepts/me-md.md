---
title: ME.MD (AI 포터블 아이덴티티)
type: concept
tags: [ai, pkm, context, claude]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]
---

## 정의

어떤 AI 도구에서도 동작하는 **AI-agnostic 포터블 아이덴티티 파일**. 내가 누구인지, 어떻게 생각하는지, AI와 어떻게 협업할지를 마크다운으로 기술한 단일 파일이다.

## CLAUDE.md와의 차이

| 항목 | CLAUDE.md | ME.MD |
|------|-----------|-------|
| 대상 | Claude 전용 | 모든 AI |
| 이식성 | Claude 종속 | AI-agnostic |
| 위치 | 볼트 루트 | AIOS/ 폴더 |
| 용도 | Claude 세션 지시 | 포터블 아이덴티티 |

Nick Milo의 실제 구현: `claude.md`는 한 줄짜리 파일로, "go immediately to me.md"만 적혀 있다. Claude가 시작되면 즉시 ME.MD로 이동해 나를 파악한다.

## 파일 내용 구조

```markdown
# ME.MD

## 나는 누구인가
(역할, 직업, 관심사)

## 나는 어떻게 생각하는가
(사고 방식, 글쓰기 스타일)

## AI와 어떻게 협업하길 원하는가
(응답 형식, 금지 사항, 선호 방식)
```

## 실전 운용

- 위치: Claude가 접근하는 루트 폴더 안 `AIOS/me.md`
- 세션 시작 시 프롬프트로 명시 지시:
  ```
  Please read the ME.MD file in the ideaverse folder.
  Then review vault map and skill map for relevant context.
  Confirm you've read, then await instruction.
  ```
- 텍스트 확장 앱(Typonator, Mac 텍스트 대치)에 단축키 등록 → 매 세션 빠른 붙여넣기

## 관련 개념

- [[wiki/concepts/ai-os|AI OS]] — ME.MD가 속하는 Layer 2
- [[wiki/concepts/claude-md|CLAUDE.md]] — Claude 전용 버전
- [[wiki/concepts/vault-map|Vault Map & Skill Map]] — ME.MD와 함께 사용하는 Layer 2 파일들

## 출처

- [[wiki/sources/2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]]
