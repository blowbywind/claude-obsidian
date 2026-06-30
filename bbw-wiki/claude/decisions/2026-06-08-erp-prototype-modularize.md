---
date: 2026-06-08
project: hnedu_erp
status: 완료
tags: [architecture, modularization, prototype, javascript]
summary: "hnedu_erp 프로토타입의 5383줄 모노리식 HTML을 HTML 스켈레톤과 CSS, JS 8파일로 분리하여 모듈화 완료."
---

# ADR: hnedu_erp 프로토타입 모노리식 HTML → 모듈 분리

**날짜:** 2026-06-08  
**프로젝트:** hnedu_erp  
**상태:** 완료

## 결정

`prototype/index.html` 5383줄(HTML+CSS+JS 인라인) → HTML 스켈레톤 + `css/app.css` + `js/*.js` 8파일로 분리.

## 이유

- 5000줄 넘는 단일 파일로 특정 기능 편집 시 전체 파일을 컨텍스트에 올려야 했음
- HTML/CSS/JS 혼재로 공통 프론트엔드 규칙(프로젝트 CLAUDE.md) 위반 상태
- 기능별 책임 분리가 없어 검색·디버그 난이도 상승

## 제약

- WinForms WebView2 대신 일반 브라우저로 목업 서빙 → ES module 사용 불가
- `onclick="fn()"` 방식의 인라인 핸들러 전부 글로벌 스코프 의존 → `window.*` 또는 top-level `function` 선언 필수
- 스크립트 로드 순서를 명시적으로 관리해야 함 (db → utils → render → calendar → tasks → mail → forms → app)

## 결과

- HTML: 1602줄 (스켈레톤만)
- CSS: 911줄 (`css/app.css`)
- JS: 2872줄 (8파일, 75개 onclick 핸들러 전부 정상 참조 확인)
- 참조 무결성 검증 완료 (누락 함수 0개)
