---
title: `Tailwind v4 네이티브 스크롤바 API`
type: concept
status: ai-curated
learned_by: arthur
curated_at: 2026-06-30
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-30-arthur-learning]]
---

# `Tailwind v4 네이티브 스크롤바 API`

Tailwind v4.3부터 스크롤바를 네이티브로 제어하는 유틸리티 클래스를 공식 지원합니다. 기존 `tailwind-scrollbar` 같은 서드파티 플러그인 없이도 스크롤바의 모양과 동작을 Tailwind 유틸리티로 제어할 수 있습니다.

## 주요 유틸리티

**스크롤바 표시 제어**: `scrollbar-auto`(자동 표시), `scrollbar-thin`(좁은 스크롤바), `scrollbar-none`(숨김)으로 스크롤바 가시성과 크기를 조절합니다.

**색상 및 세부 스타일**: `scrollbar-thumb-{color}` / `scrollbar-track-{color}` 클래스로 스크롤바의 thumb(막대)와 track(배경) 색을 각각 설정하고, `scrollbar-gutter-{size}` 클래스로 스크롤바 예약 공간을 제어합니다.

**마이그레이션 용이성**: 플러그인 설치·설정 없이 Tailwind 기본 팔레트를 그대로 활용해 일관된 디자인 시스템을 유지할 수 있으며, ai-ops의 스크롤 패널(목록, 상세뷰)에 즉시 적용 가능합니다.

## 출처
- [Tailwind CSS v4.3.0 Release](https://github.com/tailwindlabs/tailwindcss/releases/tag/v4.3.0)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-30-arthur-learning]]. 사람 검증 후 status를 verified로 변경하세요.
