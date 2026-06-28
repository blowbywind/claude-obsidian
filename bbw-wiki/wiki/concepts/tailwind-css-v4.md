---
title: `Tailwind CSS v4`
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-24
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-24-dex-learning]]
---

# `Tailwind CSS v4`

원문 기반 Obsidian 위키 concept 노트를 작성하겠습니다.

---

## 핵심 정의

**Tailwind CSS v4**는 기존의 `tailwind.config.js` 파일 중심에서 벗어나 **CSS-First 설정 모델**로 전환한 주요 메이저 버전이다. CSS 파일 내에서 `@theme` 지시어를 사용하여 디자인 토큰, 색상, 타이포그래피, 간격 등의 테마값을 직접 선언하고 관리하는 구조로 개선되었다.

## 주요 변화

1. **`@theme` 지시어 기반 토큰 정의**: JavaScript 설정 파일 없이 CSS 내에서 디자인 토큰을 명시적으로 정의할 수 있다. 이를 통해 설정과 스타일 코드의 경계를 명확히 하고 관리 복잡도를 낮춘다.

2. **설정 파일 간소화**: 기존의 복잡한 `tailwind.config.js` 구조를 제거하고 CSS 중심의 더 직관적인 접근방식으로 전환되어 온보딩과 유지보수가 용이해졌다.

3. **동적 테마 운영 개선**: CSS 변수 기반의 토큰 관리로 런타임 테마 전환, 다크모드 지원, 다중 테마 동시 운영 등의 고급 기능 구현이 간편해진다.

## 출처

- [Tailwind CSS v4 CSS-First 설정 모델 및 Next.js 15/React 19 최적화](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQEIBA-NMMAk_Z5g3fOv56TCDXAEvUp1C9s-CfgKQZr6o3iul4H7bGWIU7xdK1mh9nDoBlr4IkohVMScgkv1Q83n4Wc8KPcFzF3HClSEa-SbveDlgxod71dbFCuSPOZtmn903DL4_HiyZVIHzQq3jZAmlwKtdnIaQgW3TMu1U3UUMKnJYdL8a_Uhq1cVdR3uVYjg9k9AN12LBlfRY9kkuvs8D09NkiWzr-a_RYMLbso=)

---

**작성 완료**: 마크다운 본문(frontmatter·h1 제외) 약 380자 | 핵심 정의→요점 3개→출처 URL 구조 | 원문 기반 추측 없음 | 출처 URL 원본 보존

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-24-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
