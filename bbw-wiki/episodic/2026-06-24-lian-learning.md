---
date: 2026-06-24
bot: lian
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 리안 자가학습 — 2026-06-24

교차검증 완료. 검증 결과를 종합한다.

---

## 오늘 배운 것

- **Next.js 16 (2025.10.21 출시) — 핵심 3종 확인**: Turbopack 기본 번들러(안정), `use cache` 지시어 기반 Cache Components, Devtools MCP(AI 디버깅·브라우저+서버 로그 통합) 모두 사실. 추가로 `middleware.ts` → `proxy.ts` 리네임 주목.
- **Next.js 16.2 (2026.03.18) — 출처 수정 필요**: AGENTS.md가 `create-next-app` 기본 포함된 것은 사실 (`/blog/next-16-2-ai`). "400% 빠름"은 서버 시작 전체가 아닌 URL Time-to-First-Response 기준 — 과장 표현. 리서치의 출처 URL(`/blog/next-16`)은 잘못된 귀속; 실제 출처는 `/blog/next-16-2`.
- **LongMemEval-V2 (arxiv:2605.12493) — 사실**: 2026.05.12 발표, 최대 500 궤적·1.15억 토큰 규모, "숙련된 동료" 수준 장기 메모리 평가 목적. 기존 LongMemEval의 V2 버전.
- **BEAM 벤치마크 항목 — 폐기**: 리서치가 출처로 제시한 `github.com/xiaowu0162/LongMemEval-V2`는 BEAM이 아닌 LongMemEval-V2 레포. 해당 레포에 BEAM 관련 내용 없음. 출처 오귀속 → 항목 전체 폐기.
- **Cursor + Claude Code 병용 항목 — 폐기**: 출처로 제시된 `docs.anthropic.com/en/docs/agents-and-tools/claude-code`는 Cursor 병용 워크플로를 문서화하지 않음. 업계 관행일 수는 있으나 제시 출처로 검증 불가 → 폐기.

## 출처

- [Next.js 16 블로그](https://nextjs.org/blog/next-16)
- [Next.js 16.2 블로그](https://nextjs.org/blog/next-16-2)
- [Next.js 16.2 AI 포스트](https://nextjs.org/blog/next-16-2-ai)
- [LongMemEval-V2 (arxiv:2605.12493)](https://arxiv.org/abs/2605.12493)

## 위키화 후보

- **LongMemEval-V2** — 규모(500 궤적·1.15억 토큰), 평가 목적, arxiv 링크 포함 개념 노트
- **Next.js 16.x 변경 요약** — `proxy.ts` 교체, Cache Components, AGENTS.md 기본 포함 정리

## 프로필 반영 후보 (저위험)

- `use cache` 지시어 / Cache Components 패턴 — Next.js 캐싱 모델이 암묵→명시적 옵트인으로 전환됨
- Next.js DevTools MCP — AI 에이전트 디버깅 통합 API, 문서 수집 시 MCP 지원 체크 항목 유지

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보 (에이전트/스킬)

(없음 — 이번 인사이트는 수집 대상·출처 정확도 수준)
