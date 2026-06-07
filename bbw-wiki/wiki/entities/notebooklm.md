---
title: NotebookLM
type: entity
tags: [product, software, ai, google, research]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-zotero-notebooklm-llm-wiki-upgrade]
---

## 개요

Google이 만든 연구·학습 목적의 AI 도구. 여러 소스를 하나의 노트북에 고정해 넣고, 해당 소스들만을 기반으로 Q&A·아웃풋 생성을 수행한다. **Gemini** 모델 기반.

LLM Wiki + Zotero 외부 지식 시스템에서 **심층 Q&A 및 아웃풋 생성 레이어** 담당.

## 핵심 차별점

LLM 일반 대화와의 차이:
- 소스를 노트북에 고정 → 컨텍스트 윈도우 한계 없이 반복 질의 가능
- 매번 파일 재업로드·컨텍스트 재설명 불필요
- 답변이 어느 소스의 어느 부분에서 왔는지 출처 표시

## 아웃풋 기능

- 질의 응답 (멀티 소스 기반)
- 팟캐스트 생성
- 인포그래픽 생성
- 프레젠테이션(PPT) 생성
- 스터디 가이드

## Claude Code 연동 (notebooklm.py MCP)

오픈소스 MCP 설치 후 Claude Code에서 NotebookLM을 코드로 제어:

**주요 장점**:
- Claude Code 단일 인터페이스에서 NotebookLM 명령 실행
- Obsidian의 LLM Wiki + Zotero 소스를 자동으로 NotebookLM에 업로드
- 생성된 아웃풋을 Obsidian Efforts 폴더에 자동 저장
- 처리는 Gemini가 담당 → Claude 토큰 절약

**사용 예시**:
```
"노트북LM 이용해서 인제스트한 노트들과 원래 소스들을 바탕으로
노트북 하나 만들어줘. PKM×AI 딥다이브라는 이름으로"
→ NotebookLM에 새 노트북 자동 생성, 소스 업로드

"인포그래픽 만들어서 내 브레인 Efforts 폴더에 추가해줘"
→ 인포그래픽 생성 후 Obsidian에 저장
```

## 주요 연결

- [[wiki/concepts/external-knowledge-system|외부 지식 시스템]] — 시스템 내 심층 Q&A 레이어
- [[wiki/concepts/mcp|MCP]] — notebooklm.py MCP로 Claude Code 연동
- [[wiki/entities/zotero|Zotero]] — Zotero 소스를 NotebookLM으로 전송
- [[wiki/entities/claude-code|Claude Code]] — 통합 제어 인터페이스

## 출처

- [[wiki/sources/2026-06-07-zotero-notebooklm-llm-wiki-upgrade]]
