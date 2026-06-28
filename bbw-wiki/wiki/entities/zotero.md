---
title: Zotero
type: entity
tags: [product, software, research, reference-manager]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-zotero-notebooklm-llm-wiki-upgrade]
summary: "논문·웹페이지·동영상을 메타데이터와 함께 저장하는 레퍼런스 매니저로, LLM Wiki 시스템의 원본 소스 보관층을 담당한다."
---

## 개요

학술 연구·논문 작성을 위한 **레퍼런스 매니저 (서지 관리 프로그램)**. 원본 소스(논문·동영상·웹페이지)를 메타데이터 포함으로 저장하는 "나만의 도서관" 역할. 무료이며 연구자 외 일반인도 사용 가능.

LLM Wiki + NotebookLM 외부 지식 시스템에서 **원본 소스 보관 레이어** 담당.

## 주요 기능

- 원본 소스 보관 및 메타데이터 자동 수집
- PDF·동영상·웹페이지 통합 관리
- 하이라이트, 캡처, 애노테이션 기능
- 인용 관리 (BibTeX, APA 등)
- 컬렉션(폴더) 단위 분류

## Zotero Connector

크롬 브라우저 확장 프로그램:
- 웹페이지 열람 중 원클릭으로 Zotero에 저장
- 메타데이터(제목·저자·날짜·URL 등) 자동 수집
- 논문 페이지에서 PDF 원문 자동 다운로드

## Claude Code 연동 (Zotero MCP)

GitHub 오픈소스 MCP를 Claude Code에 설치:
```
Claude Code에 MCP GitHub URL 붙여넣기 → "설치해 줘" 요청
```

**MCP로 가능한 것**:
- 시멘틱(의미 기반) 검색 + 최근 추가 논문 조회
- 태그·DOI 기반 검색, 컬렉션 자동 생성
- 하이라이트·풀텍스트 접근
- 조테로 → LLM Wiki 인제스트 자동화

## 스킬 3종 (Claude Code 연동 시)

| 스킬 | 역할 |
|------|------|
| 조테로 인제스트 | 원본+메타데이터+애노테이션 → LLM Wiki 마크다운 변환 |
| 조테로 서치 | 시멘틱 검색으로 논문 추천·컬렉션 생성 |
| 조테로 사이트 | BibTeX/인용 내보내기 |

## LLM Wiki 시스템에서의 위치

```
외부 소스 → [Zotero] → LLM Wiki → NotebookLM → Obsidian
```
원본을 영구 보관하여 언제든 출처로 돌아올 수 있게 함.

## 주요 연결

- [[wiki/concepts/external-knowledge-system|외부 지식 시스템]] — 시스템 내 원본 보관 레이어
- [[wiki/concepts/mcp|MCP]] — Zotero MCP로 Claude Code 연동
- [[wiki/entities/notebooklm|NotebookLM]] — Zotero 소스를 NotebookLM으로 전송 가능
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — Zotero에서 인제스트된 내용이 LLM Wiki로 정제

## 출처

- [[wiki/sources/2026-06-07-zotero-notebooklm-llm-wiki-upgrade]]
