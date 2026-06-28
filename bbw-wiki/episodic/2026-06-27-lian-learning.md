---
date: 2026-06-27
bot: lian
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 리안 자가학습 — 2026-06-27

교차검증 완료. 정리한다.

---

**검증 결과 요약:**

| 항목 | 판정 |
|---|---|
| LongMemEval-V2 | 기존 위키 중복(2026-06-24 promoted). "451개 문제" vs 위키 "500 궤적" 불일치 — WebFetch 권한 없어 수치 검증 불가, 버림 |
| AI Control 연구 부상 | 위키 `defense.md` 중복. 동일 내용 이미 기록됨 |
| Next.js 16.2 Build Adapters | **버전 표기 오류** — `nextjs.org/blog/next-16` 원문 확인 결과 16.2 아님, Next.js 16에 **(alpha)**로 포함. 기존 메모리 "16.2" 표기 수정 필요 |
| Next.js 16 Cache Components | 원문 확인. 위키 중복이나 세부 API(`updateTag`, `refresh`, `proxy.ts`) 일부 미기록 |
| TanStack Start v1.0 | WebSearch 권한 없어 검증 불가. 기존 메모리 "v1 RC" 기록 유지, 버림 |
| Cursor + Claude Code 병용 | 위키 `ai.md` 중복 |

---

## 오늘 배운 것

- **Next.js 16 Build Adapters API는 alpha, 버전 표기 오류 수정**: 기존 메모리에 "16.2"로 잘못 기록됐으나, 공식 블로그(`nextjs.org/blog/next-16`) 원문 기준 Next.js 16에 experimental alpha로 포함. 비Vercel 배포 시 `experimental.adapterPath`로 사용
- **`proxy.ts` 신규 추가 (Next.js 16)**: `middleware.ts`를 `proxy.ts`로 대체. Node.js 런타임 고정, 네트워크 경계 명확화. `middleware.ts`는 Edge 한정 deprecated
- **캐싱 API 신규 2종 (Next.js 16)**: `updateTag()` — Server Action 전용, 즉시 반영(read-your-writes) / `refresh()` — 비캐시 데이터만 갱신. 기존 `revalidateTag()`는 두 번째 인수(`cacheLife` 프로파일) 필수로 변경
- **Next.js 16 릴리스일 확인**: 2025년 10월 21일. "16.2"는 현재 공식 블로그에 존재하지 않음

## 출처

- [Next.js 16 공식 블로그](https://nextjs.org/blog/next-16)

## 위키화 후보

- `proxy.ts` — Next.js 16 신규 네트워크 경계 파일, middleware 마이그레이션 가이드 포함 노트

## 프로필 반영 후보 (저위험)

- `updateTag()` / `refresh()` — Next.js 16 캐싱 API 2종을 문서 수집 체크리스트에 추가

## 승인 필요 (고위험)

- **기존 메모리 오류 수정**: `[2026-06-25] Build Adapters API: Next.js 16.2 기반...` → "Next.js 16 (alpha)" 로 정정. 메모리 파일 직접 수정 승인 요청

## 신규 도구 후보 (에이전트/스킬)

없음
