---
title: Obsidian
type: entity
tags: [product, software, note-taking]
created: 2026-06-05
updated: 2026-06-07
sources: [2026-06-05-llm-wiki-pattern, 2026-06-05-claude-code-obsidian-lmwiki-graphify, 2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]
summary: "로컬 마크다운 기반 노트 앱으로서 Wiki 탐색·AI 콘텐츠 저장, 플러그인·CSS 커스터마이징 확장이 특징이며 AI OS의 Layer 1 저장소 역할을 한다."
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

## CSS 스니펫으로 외관 커스터마이징

Obsidian은 테마를 통째로 바꾸지 않고 **CSS 스니펫**으로 원하는 부분만 덮어쓸 수 있다.

### 설치 방법
1. 설정 → 외관 → 하단 스크롤 → CSS 스니펫 → 폴더 아이콘
2. 스니펫 폴더에 `.css` 파일 복사
3. 새로고침 후 토글 활성화 (여러 파일 동시 적용 가능)

### Claude Code로 실시간 CSS 수정
VS Code + Claude Code 확장에서 Obsidian 볼트 폴더를 열면 자연어로 즉시 수정 가능:
- "폰트를 고딕으로 바꿔줘", "강조색을 주황으로 변경해줘"
- 저장 즉시 Obsidian 화면에 반영

### Claude 스타일 CSS 참고
오후다섯씨(Mr.5pm)가 제작한 Claude 인터페이스 스타일 CSS:
- 다크 브라운 배경, 주황 강조색, 명조체(북극 폰트), 깔끔한 테이블
- 자세한 내용: [[wiki/sources/2026-06-08-obsidian-claude-style-css-mr5pm|CSS 스타일링 튜토리얼]]

## AI OS에서의 역할 (Nick Milo 프레임워크)

- **Ideaverse 호스팅**: ACE(Atlas·Calendar·Efforts) 폴더 구조로 17,000개+ 노트 관리
- **Layer 1 역할**: AI OS의 핵심 — 내 생각과 AI 생성 콘텐츠의 저장소
- **마크다운 이식성**: Obsidian이 사라져도 모든 노트는 어떤 앱에서도 열 수 있는 표준 마크다운
- **Daily Brief 수신함**: Calendar 폴더가 AI가 생성하는 일일 브리핑 저장 위치

## 주요 연결

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 이 위키의 탐색 IDE
- [[wiki/concepts/ai-os|AI OS]] — Obsidian이 Layer 1 역할
- [[wiki/concepts/ace-folder-framework|ACE 폴더 프레임워크]] — Nick Milo의 볼트 구조

## 출처

- [[wiki/sources/2026-06-05-llm-wiki-pattern]]
- [[wiki/sources/2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]]
