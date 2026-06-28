---
date: 2026-06-24
bot: dex
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 덱스 자가학습 — 2026-06-24

## 오늘 배운 것
- **Tailwind CSS v4 CSS-First 설정 모델**: 기존 `tailwind.config.js`를 사용하지 않고, CSS 내의 `@theme` 지시어로 디자인 토큰과 테마를 직접 정의하여 관리합니다.
- **Model Context Protocol (MCP) 서버 연동 제약**: 에이전트당 연결하는 MCP 서버를 5~7개 이하로 제한하여 컨텍스트 윈도우 낭비와 도구 오선택 등 성능 저하를 방지합니다.
- **Next.js 15 비동기 API 및 비캐싱 전환**: `cookies()`, `headers()`, `params` 등의 API가 Promise를 반환하는 비동기 방식으로 변경되었으며, `fetch` 요청과 GET 라우트 핸들러가 기본적으로 캐싱되지 않도록 변경되었습니다.
- **서버 컴포넌트(RSC) 내부 fetch 방지**: 서버 컴포넌트 내부에서 동일 서버의 API Route를 `fetch()`로 호출하지 않고, 데이터베이스 접근이나 서비스 모듈을 직접 가져와 호출하여 불필요한 네트워크 홉과 직렬화 오버헤드를 방지합니다.
- **React 19 클라이언트 경계선 최소화**: 부모 컴포넌트에 `"use client"`를 설정하는 대신 경계선을 컴포넌트 트리 하단으로 좁혀 번들 크기를 최적화하고, 컴포넌트 내부 비동기 데이터 처리에 `use()` 훅을 적극 활용합니다.

## 출처
- [Tailwind CSS v4 CSS-First 설정 모델 및 Next.js 15/React 19 최적화](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQEIBA-NMMAk_Z5g3fOv56TCDXAEvUp1C9s-CfgKQZr6o3iul4H7bGWIU7xdK1mh9nDoBlr4IkohVMScgkv1Q83n4Wc8KPcFzF3HClSEa-SbveDlgxod71dbFCuSPOZtmn903DL4_HiyZVIHzQq3jZAmlwKtdnIaQgW3TMu1U3UUMKnJYdL8a_Uhq1cVdR3uVYjg9k9AN12LBlfRY9kkuvs8D09NkiWzr-a_RYMLbso=)
- [MCP 설계 가이드라인 및 제한된 컨텍스트](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQGdNChAHAYGtQ5h9n-YybjibtVaYv44jc2XgBRQV9SdZNYE6NKDBdjUptbpVpx5OfZ1PyHKT75L91_G8rYuHc1a3NBSdpS52N4dgpv5Prr6UFSZ6TzUkq2wklSXAUkGQkQ28lhujUt5gJrZ_zk7fcoT-rV4ltBTO5Vg9OOn5Q==)
- [React 19 클라이언트 경계선 최소화](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQHsMXbPV4gqbiH0zeE3k6AIsXqOZrsmRYp356zSKZIHfJU88w7GL01NjAXadKo2hd826b6HhZhfOpMNqtgW9LL12RdYi009_Gc3hNeQnl1vM0bvfBYdIRGndyhj06BAqJ9NPIR6ij2fdA7XgU--0Yehy7lbUHbbAeFmbw==)
- [Core Web Vitals INP 핵심 지표 전환](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQF7auyP4-wFfTgAHM5Fzosb1g3LOK-x4RSyPxboEibk2hGmvwoaelCYUSgkQ317_uHrrJgBX2nsx9soK2dkfocqbqv0itBhG8_HyICCFmH-4Ua7NLzMwb2fwaZEA0bnHkEeiu29BakgJ1qK57tV)

## 위키화 후보
- `Tailwind CSS v4`: `@theme` 지시어를 사용하는 CSS-First 설정 모델 및 디자인 토큰 정의 규격 정리.
- `INP (Interaction to Next Paint)`: 2026년에 완전 정착된 상호작용 반응성 지표와 렌더링 최적화 방안 정리.

## 프로필 반영 후보 (저위험)
- `RSC 데이터 페칭 아키텍처`: 서버 컴포넌트에서 API 라우트를 fetch하지 않고 직접 데이터베이스/서비스 레이어에 접근하여 불필요한 네트워크 홉을 방지하는 설계 패턴.
- `MCP 오케스트레이션 제약`: 에이전트당 MCP 서버 연동 개수를 5~7개 이하로 제한하여 모델의 도구 선택 성능 저하 및 컨텍스트 낭비를 방지하는 아키텍처 규칙.

## 승인 필요 (고위험)


## 신규 도구 후보 (에이전트/스킬)
- `[skill] mcp-optimizer` — 현재 프로젝트에 활성화된 MCP 서버 개수 및 토큰 점유율을 모니터링하여 5~7개 최적 상태를 유지하고, 사용하지 않는 도구를 정리하는 유틸리티 스킬.
