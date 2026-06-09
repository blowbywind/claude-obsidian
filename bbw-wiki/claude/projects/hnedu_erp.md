# hnedu_erp

## 핵심
해냄에듀 Windows 바탕화면 고정형 업무·근태 통합 대시보드 (win-screen).

## 현재 상태
- 위치: `/home/bbw/projects/hnedu_erp`
- 기획서: `docs/PLAN.md` (Ch.1~9, 최종)
- 디자인 시스템: `docs/DESIGN.md`
- **작업 리포트**: `docs/리포트.md` (2026-06-09~10 전체 작업 기록)
- 참조 이미지: `references/` (읽기 전용, 수정 금지)
- UI 목업: `prototype/index.html` (v3, 1920×1080)

## 프로토타입 구조 (2026-06-08 모듈화)

```
prototype/
├── index.html          # HTML 스켈레톤 (1602줄)
├── css/
│   └── app.css         # 전체 스타일 (911줄)
└── js/
    ├── db.js           # window.DB, TODAY, TOMORROW
    ├── utils.js        # 공용 유틸·CDN lazy-load
    ├── render.js       # 모든 렌더 함수, _renderAll()
    ├── calendar.js     # 월별 캘린더 그리드
    ├── tasks.js        # 업무 모달·드로어·상태머신
    ├── mail.js         # 메일 패널
    ├── forms.js        # 휴가·지출·회의·결재·신고
    └── app.js          # 초기화·spotlight·공지 페이지네이션
```

**로드 순서 의존성:** db → utils → render → calendar → tasks → mail → forms → app

## 현재 단계
**Phase 0 완료 — Phase 1(WinForms 셸 + 인증) 준비 중**

## 규칙
- `prototype/index.html` 수정 후 `docs/DESIGN.md` + `docs/PLAN.md` 반드시 동기화
- `references/`는 참조만, 기획 기준은 `docs/PLAN.md`
- Live Server 포트: **5502** 고정 (`http://127.0.0.1:5502/prototype/index.html`)
- JS는 글로벌 스코프 유지 (ES module 금지 — onclick 핸들러 호환성)

## 주의사항
- 배지 통합 작업 시 조건부 실행 지시 주의 (2026-06-07 사고)
- CDN `<script src>` 동기 로딩 금지 — lazy-load 패턴 필수 (utils.js `_loadScript` 사용)

## 작업 히스토리
- 2026-06-07: 배지 통합 (미열람·알림 → 단일 수로 표시)
- 2026-06-08~09: 공지 페이지네이션·Spotlight 검색 추가, docs/layout-mockup.html → prototype/index.html 이동, docs/기획서.md → docs/PLAN.md 개명, 모노리식 HTML(5383줄) → CSS+JS 8파일 모듈화
