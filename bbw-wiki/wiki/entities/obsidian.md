---
title: Obsidian
type: entity
tags: [product, software, note-taking]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-llm-wiki-pattern, 2026-06-05-claude-code-obsidian-lmwiki-graphify]
---

## 개요

로컬 마크다운 파일 기반 노트 앱. 이 위키의 **탐색 IDE** 역할을 한다.

## LLM Wiki에서의 역할

- **그래프 뷰**: 위키 페이지 간 연결 관계를 시각화 — 허브 페이지와 고아 페이지 파악
- **Web Clipper**: 브라우저 확장으로 웹 아티클을 마크다운으로 변환해 raw/에 추가
- **Marp 플러그인**: 위키 콘텐츠에서 슬라이드 덱 직접 생성
- **Dataview 플러그인**: 프론트매터 기반 동적 테이블·리스트 쿼리

## Web Clipper 커스텀 템플릿

기본 템플릿은 LM Wiki 스키마와 맞지 않으므로 커스텀 필요:
1. 웹 스토어에서 "Obsidian Web Clipper" 크롬 확장 설치 → 고정
2. 옵션 → 기존 템플릿 내보내기(JSON)
3. Claude Code에 JSON 제공 → article/youtube/podcast/book/research 5종 템플릿 생성 요청
4. 임포트 버튼으로 각 템플릿 추가
5. 유튜브 페이지 방문 시 유튜브 템플릿이 자동 트리거 (트랜스크립트 포함)

## 이미지 관련 팁

Settings → Files and links에서 Attachment folder를 `raw/assets/`로 설정.
Hotkeys에서 "Download attachments" 단축키 설정 → 클립 후 이미지 로컬 다운로드.

## 주요 연결

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 이 위키의 탐색 IDE

## 출처

- [[wiki/sources/2026-06-05-llm-wiki-pattern]]
