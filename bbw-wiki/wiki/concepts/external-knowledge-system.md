---
title: 외부 지식 시스템
type: concept
tags: [pkm, ai, zotero, notebooklm, llm-wiki, research, architecture]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-zotero-notebooklm-llm-wiki-upgrade]
---

## 정의

AI OS의 외부 지식 축(LLM Wiki)을 완성하는 **3계층 지식 관리 아키텍처**. 원본 보관(Zotero) → 1차 정제(LLM Wiki) → 심층 탐구(NotebookLM)의 흐름으로, Claude Code가 전체를 MCP로 통합 제어한다.

## 3계층 구조

```
[Layer A] Zotero — 원본 도서관
    · 논문·동영상·웹페이지 원문 + 메타데이터 보관
    · Zotero Connector(크롬)으로 원클릭 수집
    · 언제나 원본 소스로 되돌아갈 수 있는 닻

[Layer B] LLM Wiki — 1차 정제 공간
    · Zotero 원본을 마크다운 카드로 소화
    · 개념·엔티티·소스 페이지로 구조화
    · Claude Code + 인제스트 스킬로 자동 처리

[Layer C] NotebookLM — 심층 탐구 공간
    · 특정 소스 묶음을 고정해 반복 Q&A
    · PPT·인포그래픽·팟캐스트 등 아웃풋 생성
    · 결과물은 Obsidian Efforts에 저장
```

**Claude Code (MCP)**가 A·B·C를 단일 인터페이스로 연결

## 해결하는 문제들

| 문제 | 해결 레이어 |
|------|-------------|
| 원본 소스(PDF 등) 보관 — Obsidian Sync 용량 한계 | Zotero |
| AI 대화 컨텍스트 유지 — 매번 파일 재업로드 필요 | NotebookLM |
| AI 답변 원본 출처 추적 어려움 | Zotero 메타데이터 |

## 지식 깊이 스펙트럼

```
얕음 ←────────────────────────────→ 깊음
[LLM Wiki]    [NotebookLM]    [My Notes]
빠른 소화      집중 탐구       내 경험·통찰
외부 지식      외부 지식       내 고유 생각
```

- **LLM Wiki**: 빠른 1차 정제, 광범위한 소스 커버
- **NotebookLM**: 특정 주제 심층 탐구, 아웃풋 생성
- **My Notes (Ideaverse)**: 내가 실제 경험하고 체화한 것

## 통합 워크플로우 예시 (연구 작업)

```
1. 논문 발견 → Zotero Connector로 저장
2. Claude Code: "조테로 서치로 PKM×AI 관련 논문 찾아 컬렉션 만들어줘"
3. Claude Code: "조테로 인제스트로 LLM Wiki에 소화시켜줘"
4. Claude Code: "이 노트들로 NotebookLM 만들어줘, 딥다이브 탐구"
5. NotebookLM에서 심층 Q&A, 인포그래픽 생성
6. 결과물 자동으로 Obsidian Efforts에 저장
```

## Gold in, Gold out 원칙과의 관계

- Zotero 저장 시: 왜 이 소스를 저장하는가? (목적성 명시)
- LLM Wiki 인제스트 시: 어떤 관점에서 소화할 것인가? (기준 입력)
- NotebookLM Q&A: 어떤 인사이트를 얻고 싶은가? (질문의 질)

→ 각 레이어에서 사용자의 의도가 개입할수록 최종 아웃풋 품질 향상

## 관련 개념

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 이 시스템의 Layer B
- [[wiki/concepts/ai-os|AI OS]] — 외부 지식 시스템이 속하는 더 큰 아키텍처
- [[wiki/concepts/mcp|MCP]] — 세 도구를 Claude Code로 통합하는 연결 수단
- [[wiki/concepts/목적성 있는 수집|목적성 있는 수집]] — 각 레이어 진입 시 적용되는 원칙

## 관련 엔티티

- [[wiki/entities/zotero|Zotero]] — Layer A
- [[wiki/entities/notebooklm|NotebookLM]] — Layer C
- [[wiki/entities/obsidian|Obsidian]] — LLM Wiki + 아웃풋 저장소
- [[wiki/entities/claude-code|Claude Code]] — 통합 제어

## 출처

- [[wiki/sources/2026-06-07-zotero-notebooklm-llm-wiki-upgrade]]
