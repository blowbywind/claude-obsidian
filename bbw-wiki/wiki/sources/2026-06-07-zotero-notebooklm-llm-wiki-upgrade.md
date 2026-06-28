---
title: "LLM Wiki를 업그레이드하는 외부 지식 시스템: Zotero × NotebookLM × Obsidian × Claude Code"
type: source
tags: [zotero, notebooklm, llm-wiki, obsidian, claude-code, pkm, mcp, research]
created: 2026-06-07
updated: 2026-06-07
origin: https://youtu.be/ulhEyDIxj6Q
author: 브레인 트리니티 (브라인)
date_published: 2026-06
summary: "LLM Wiki 단독 한계(원본보관·컨텍스트·출처추적)를 Zotero와 NotebookLM MCP로 보완해 Claude Code 단일 인터페이스에서 외부 지식 시스템을 완성하는 3도구 통합 아키텍처."
summary: "LLM Wiki 단독 한계(원본보관·컨텍스트·출처추적)를 진단하고 Zotero·NotebookLM을 MCP로 연결해 Claude Code 단일 인터페이스로 외부 지식 시스템을 완성하는 통합 워크플로우 실연."
---

## 요약

LLM Wiki 단독 사용의 3가지 한계를 진단하고, **Zotero**(원본 도서관)와 **NotebookLM**(심층 Q&A·아웃풋)을 추가해 외부 지식 시스템을 완성하는 방법을 실연한다. Claude Code가 Zotero MCP와 NotebookLM MCP를 통해 세 도구를 하나의 워크플로우로 통합한다.

## 핵심 주장

- LLM Wiki는 외부 지식의 "1차 정제 공간"이며, 원본 보관·심층 탐구를 위한 별도 도구가 필요하다
- **Zotero**는 원본 소스(논문·동영상·웹페이지)를 메타데이터 포함 보관하는 나만의 도서관
- **NotebookLM**은 특정 소스 묶음을 고정해 컨텍스트 유지 Q&A 및 아웃풋(PPT·인포그래픽) 생성
- MCP로 연결하면 Claude Code 단일 인터페이스에서 세 도구를 통합 제어 가능

## 3가지 문제와 해결책

| # | 문제 | 해결 도구 |
|---|------|-----------|
| 1 | 원본 소스(PDF·동영상 등) 보관 공간 부재 — Obsidian Sync 용량 제한 | **Zotero** |
| 2 | 여러 소스 기반 AI 대화 시 컨텍스트 윈도우 한계, 파일 재설명 번거로움 | **NotebookLM** |
| 3 | AI 답변에서 원본 출처 추적·연결 유지 어려움 | **Zotero 메타데이터** |

## 외부 지식 시스템 아키텍처

```
외부 소스 (논문 / 동영상 / 웹페이지)
    ↓ Zotero Connector (크롬 확장)
[Zotero] — 원본 보관, 메타데이터+하이라이트+풀텍스트
    ↓ Zotero MCP + 조테로 인제스트 스킬
[LLM Wiki] — 1차 정제, 마크다운 카드 형태
    ↓ notebooklm.py MCP + 노트북 스킬
[NotebookLM] — 고정 소스 기반 Q&A, 아웃풋 생성
    ↓ 결과물
[Obsidian Efforts] — 아웃풋(인포그래픽·PPT 등) 저장
```

**Claude Code**가 전체 파이프라인을 단일 인터페이스에서 제어

## Zotero 활용 상세

### Zotero Connector
- 크롬 확장 프로그램
- 웹페이지 소스 저장 시 메타데이터 자동 수집 (매우 중요 — 출처 추적 기반)
- 논문·동영상·웹페이지 모두 저장 가능

### Zotero MCP
- Claude Code와 Zotero를 직접 연결
- 시멘틱 기반 검색, 하이라이트, 풀텍스트 접근 가능
- GitHub에 오픈소스로 공개된 MCP 설치: Claude Code에 URL 붙여넣기 후 "설치해 줘" 요청

### Zotero 스킬 3종

| 스킬 | 기능 |
|------|------|
| 조테로 인제스트 | Zotero → LLM Wiki 마크다운 변환 (메타데이터+애노테이션+풀텍스트, 폴더 구조 맞춤화) |
| 조테로 서치 | 시멘틱/키워드/리서치 퀘스천 기반 논문 검색, 컬렉션 자동 생성 |
| 조테로 사이트 | 인용 관리, BibTeX 내보내기 |

## NotebookLM 활용 상세

### notebooklm.py MCP
- Claude Code에서 NotebookLM을 코드로 제어
- 처리는 Gemini가 담당 (Claude 토큰 절약)
- 아웃풋(인포그래픽·PPT 등)을 Obsidian에 직접 저장

### 워크플로우 예시
1. `노트북LM 이용해서 [소스들] 바탕으로 노트북 하나 만들어줘` → 자동 생성
2. Obsidian + Zotero 소스가 노트북에 자동 업로드
3. `인포그래픽 만들어서 [Efforts 폴더]에 저장해 줘` → Claude Code가 명령 → Obsidian 저장

## 연결된 개념

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 이 시스템에서 1차 정제 레이어
- [[wiki/concepts/external-knowledge-system|외부 지식 시스템]] — 3개 도구 통합 아키텍처
- [[wiki/concepts/mcp|MCP]] — Zotero MCP, NotebookLM MCP 활용
- [[wiki/concepts/purposeful-collection|목적성 있는 수집]] — Gold in, Gold out 원칙

## 연결된 엔티티

- [[wiki/entities/brain-trinity|브레인 트리니티]] — 영상 제작자
- [[wiki/entities/zotero|Zotero]] — 원본 소스 관리
- [[wiki/entities/notebooklm|NotebookLM]] — 심층 Q&A·아웃풋
- [[wiki/entities/obsidian|Obsidian]] — LLM Wiki + 아웃풋 저장
- [[wiki/entities/claude-code|Claude Code]] — 통합 제어 인터페이스

## 메모

- "조테로 인제스트" 스킬은 내 폴더 구조에 맞게 커스터마이징 필요 — 범용 스킬이 아님
- 인제스트 시 `why I save this` 필드는 사용자가 직접 채워야 함 (목적성 원칙)
- 대량 인제스트 시 토큰 소모에 주의 — 한 번씩 진행 후 커피 한 잔 마시고 확인 권장
- notebooklm.py MCP는 Claude가 아닌 Gemini를 사용하므로 Claude 토큰 절약 효과 있음
- 조테로는 무료 (연구자·일반인 모두 사용 가능), API 외에 MCP 방식 연결 권장
