---
title: "옵시디언 아직도 그냥 쓰세요? 한방에 클로드 스타일로 바뀝니다! 옵시디언 + Claude + VS Code"
type: source
tags: [obsidian, css, claude-code, customization, workflow, vscode]
created: 2026-06-08
updated: 2026-06-08
origin: https://youtu.be/Q33WveI7NqU
author: 오후다섯씨 (Mr.5pm)
date_published: 2026-06-06
---

## 요약

오후다섯씨(Mr.5pm)가 Obsidian을 Claude 인터페이스 스타일로 꾸미는 CSS 스니펫을 직접 제작해 무료 공유하는 13분 37초 튜토리얼. CSS 스니펫 설치 방법, Claude를 활용한 CSS 자동 생성·실시간 수정 워크플로우, Claude Code(VS Code) 연동까지 다룬다.

## 핵심 주장

- 이쁜 도구는 자꾸 보게 되고, 자꾸 보면 자꾸 쓴다 — 생산성 도구의 미적 경험이 사용 지속성을 좌우한다
- AI가 생성하는 텍스트를 어떻게 시각화하느냐에 따라 생산성이 달라진다
- "여러분만의 도구로 진화시키는 것"이 AI 트렌드

## 핵심 내용

### Claude 스타일 Obsidian의 특징

제작자가 정의한 "Claude 스타일":

| 요소 | 설정 |
|------|------|
| 배경 | 다크 모드 — 완전 검정이 아닌 다크 브라운 계열 |
| 강조색 | 주황색 (Claude 브랜드 컬러) |
| 폰트 | 명조체 (북극 폰트, 무료) — 책처럼 읽히는 스타일 |
| 테이블 | Claude 웹 인터페이스의 깔끔한 테이블 스타일 |
| 자간·줄 간격 | Claude 채팅창 텍스트 렌더링 기준 |
| 리스트 | 블릿·숫자 리스트 간격·들여쓰기 최적화 |

과거 Claude가 명조체로 채팅창 텍스트를 렌더링했던 시기를 참고해 설계됨.

### CSS 스니펫 설치 방법

1. Obsidian **설정 → 외관** → 하단 스크롤 → **CSS 스니펫** 항목
2. 폴더 아이콘 클릭 → 스니펫 폴더 열림
3. 다운로드한 `.css` 파일을 해당 폴더에 복사
4. 새로고침 후 파일 옆 토글 활성화

**팁**: 원본 CSS 파일은 보존하고 복사본을 수정 — AI로 작업할 때 항상 원본 보관

### Claude로 CSS 자동 생성하기

1. Claude 웹에서 요청: "CSS 파일을 작성해서 Obsidian 텍스트 모양을 바꾸려 한다"
2. 원하는 스타일의 **스크린샷(캡처 이미지)을 첨부**
3. "폰트·자간·줄 간격·리스트·테이블 모두 똑같이 Obsidian에서 보고 싶다" 요청
4. Claude가 완성된 CSS 파일 생성 → 다운로드 → 스니펫 폴더에 적용

### Claude Code(VS Code)로 실시간 수정

Claude Code를 VS Code에서 열고 Obsidian 볼트 폴더를 프로젝트 경로로 지정하면:
- 자연어로 즉시 수정 가능: "폰트를 고딕으로 변경해줘", "강조색을 주황색으로 바꿔줘"
- Claude Code가 CSS 파일을 직접 접근·수정
- Obsidian 화면이 **실시간 반영** (저장 즉시 적용)

**웹 Claude의 한계**: 컴퓨터 파일에 직접 접근 불가 → Claude Desktop / VS Code + Claude Code / 터미널 Claude Code 중 하나 필요. 제작자는 VS Code 방식을 가장 편리하다고 추천.

### 커스터마이징 전략

- 좋아하는 스타일의 UI 스크린샷을 Claude에게 참조 이미지로 제공
- 색상 코드(HEX)를 직접 지정하거나 브랜드명("Claude 주황색")으로 요청 가능
- 밝은 모드 선호 시 light 테마로 재설계 가능
- 작업하다 마음에 안 드는 부분이 생길 때마다 Claude Code에게 즉시 수정 요청

## 연결된 개념

- [[wiki/concepts/second-brain|세컨드 브레인]] — Obsidian이 세컨 브레인 인터페이스
- [[wiki/concepts/context-engineering|컨텍스트 엔지니어링]] — AI 생성 텍스트 시각화 최적화
- [[wiki/concepts/ai-os|AI OS]] — Obsidian Layer 1 역할과 연결

## 연결된 엔티티

- [[wiki/entities/mr5pm|오후다섯씨 (Mr.5pm)]] — 영상 제작·CSS 파일 제작 및 무료 배포
- [[wiki/entities/obsidian|Obsidian]] — CSS 스니펫 대상 앱
- [[wiki/entities/claude-code|Claude Code]] — CSS 실시간 수정 도구

## 메모

- CSS 파일은 영상 설명란 링크로 무료 배포 예정
- 제작자의 완성본 CSS: 14KB (여러 번 수정·보완), 시연용 즉석 생성본: 6KB
- "북극" 폰트: 국내 출판계에서 사용하는 무료 명조체
