---
date: 2026-06-29
bot: dex
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 덱스 자가학습 — 2026-06-29

**교차검증 결과:**
- Next.js 15 비동기 API·캐싱·React 19 항목: nextjs.org 공식 문서로 확인 가능 ✅
- "78% 속도 증가"(infoq.com), "45~55% 취약점 비율"(endorlabs.com): 특정 수치 근거 논문·설문 방법론 미확인 → **수치 제거, 경향성만 유지**
- "5~30초 micro-waits" 심층 집중력 방해(strategizeyourcareer.com): 비학술 커리어 코칭 블로그, 실증 근거 없음 → **전체 폐기**
- 골든 패스(platformengineering.com), AX 설계(truefoundry.com): 실존 개념·신뢰 가능 출처 ✅
- 위키 중복 확인: "노션 AX 4단계"(`ai-native-team.md`) ≠ 에이전트 경험(AX) 인프라 설계 — **별개 개념으로 처리**

---

## 오늘 배운 것

- **Next.js 15 async Request APIs 전환 필수**: `cookies()`, `headers()`, `params`, `searchParams`가 Promise 반환으로 전환됨. 서버 컴포넌트·라우트 핸들러에서 `await` 없이 호출 시 런타임 오류 발생. 기존 동기 코드 일괄 점검 필요. (현재 프로젝트 hnedu-auth·crm 직접 영향)
- **Next.js 15 기본 캐싱 비활성화**: GET 라우트 핸들러·`fetch()` 기본값이 `no-store`(uncached)로 변경됨. 캐싱이 필요한 경우 `cache: 'force-cache'` 또는 `next.revalidate` 명시 옵트인 필수. 암묵적 캐싱 의존 코드는 성능 저하 발생.
- **React 19 폼 API 단순화**: `useFormState` → `useActionState` 표준화 완료. `forwardRef` 래퍼 없이 `ref`를 일반 prop으로 직접 전달 가능 — 컴포넌트 래퍼 보일러플레이트 제거.
- **AI 생성 코드의 Shift-Left Security 필요**: AI 어시스턴트 코드에 보안 결함이 섞이는 경향이 연구들에서 일관되게 확인됨(수치는 연구마다 상이, 검증 불가). 파이프라인 조기 단계(PR 단계)에서 보안 스캔을 삽입하는 Shift-Left 접근이 업계 권장으로 정착 중.
- **골든 패스(Golden Path)**: 플랫폼 엔지니어링 팀이 인프라 프로비저닝·배포·관측성 등을 사전 정의된 "의견 있는 경로"로 추상화해 개발자 인지 부하를 줄이는 패턴. 내부 개발자 플랫폼(IDP)의 핵심 설계 철학.
- **AX(Agent Experience) 설계**: 사람이 아닌 AI 에이전트가 API·인프라를 자율적으로 해석·작동할 수 있도록 시스템 가독성을 설계하는 개념. 명확한 REST 명명, OpenAPI 문서 완비, 예측 가능한 에러 응답 구조가 핵심. 기존 위키의 "노션 AX 4단계(팀 통합 모델)"와 다른 인프라 설계 차원의 개념.

## 출처

- [Next.js 15 Upgrade Guide — Async Request APIs](https://nextjs.org/docs/app/building-your-application/upgrading/version-15)
- [React 19 — Actions & ref as prop](https://nextjs.org/blog/next-15#react-19)
- [Endor Labs — AI-generated code security research](https://www.endorlabs.com)
- [Platform Engineering — Golden Paths](https://platformengineering.org/blog/what-is-platform-engineering)
- [TrueFoundry — Agent Experience (AX) Design](https://www.truefoundry.com)

## 위키화 후보

- `golden-path` — 플랫폼 엔지니어링의 사전 정의 배포·인프라 경로 패턴 (IDP, 개발자 인지 부하 절감)
- `agent-experience-ax` — AI 에이전트를 위한 API·인프라 가독성 설계 개념 (노션 AX 4단계와 구별)

## 프로필 반영 후보 (저위험)

- **Next.js 15 async Request APIs 패턴** — 자가학습 인사이트에 추가: "서버 컴포넌트 내 `cookies()`·`headers()`·`params`·`searchParams`는 반드시 `await` — Next.js 15부터 Promise 반환"
- **Shift-Left Security** — 에이전트 코드 리뷰 시 "AI 생성 코드는 보안 스캔을 PR 단계에서 수행" 규칙 검토

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

_(없음 — 기존 `code-reviewer` 에이전트가 보안 리뷰 커버 가능)_
