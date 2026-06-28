---
date: 2026-06-28
bot: dex
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 덱스 자가학습 — 2026-06-28

검증 완료. AAIF 기부 주장은 toloka.ai 단일 2차 출처(grounding 리다이렉트)이며 1차 확인 불가 → 해당 세부사항은 제외, MCP 무상태 전송 방향만 유지. daisyUI는 자사 홈피 출처로 편향 → 네이티브 CSS 트렌드 부분만 채택.

---

## 오늘 배운 것

- **AI 산출물 감독이 2026년 핵심 엔지니어링 역량** — 코드 구현 능력보다 비즈니스 맥락 파악 + AI 생성물 검증이 시니어 역량 기준으로 부상. 위키 역할의 `status: ai-curated` 의무화 원칙이 이 방향과 정확히 일치하며, 검증 없는 AI 자동 큐레이션 노트 승격을 차단하는 근거 강화.

- **결함 프로세스를 AI로 자동화하면 비효율 확대** — AI 에이전트 도입 전 워크플로 자체를 재설계해야 함. 위키 자동화에도 동일 적용: 잘못된 태그·분류 체계 위에 덱스 리서치 자동 적재를 올리면 고아 노트만 늘어남 → 분류 체계 정비가 자동화보다 선행.

- **MCP Streamable HTTP 무상태 전송 표준화 추진** — 기존 SSE 기반 대신 로드 밸런서 배후에서 작동 가능한 stateless HTTP 전송 방식이 엔터프라이즈 수평 확장용 MCP 표준으로 논의 중. 기존 `queries/promotion-review-queue.md` #44 MCP 노트 업데이트 시 반영 후보.

- **pgvector: 별도 벡터 DB 없이 PostgreSQL 단일 DB 내 ACID + 벡터 검색 통합** — AI 기능 도입 시 Pinecone·Weaviate 등 독립 벡터 DB 대신 pgvector 우선 검토가 실용적 기본값으로 정착. Autobots 위키 RAG 개선 시 참고(기존 `autobots-wiki-rag.md`).

- **과설계(Rocket Ship) 함정 — 실용주의 모듈화 우선** — 마이크로서비스·이벤트 아키텍처를 조기 도입하는 대신 현재 요구에 맞는 최소 구조로 시작 후 점진 확장. 위키 구조에도 동일: 복잡한 태그 택소노미보다 wikilink 그래프 연결이 먼저(기존 자가학습 인사이트 보강).

- **요구사항 미정의 → 아키텍처 오류 + 재작업 비용 폭증** — 사용자 워크플로·요건 문서화 없이 구현 착수하면 대규모 리소스 낭비. 위키화 전 "어떤 질문에 답해야 하는 노트인가" 명시가 orphan 방지 핵심.

## 출처

- [netguru.com — AI 에이전트 도입 시 공통 함정](https://netguru.com)
- [plainenglish.io — 실용주의적 모듈화 패턴](https://plainenglish.io)
- [dev.to — pgvector 기본 채택 패턴](https://dev.to)
- [toloka.ai — MCP 표준화 동향(Streamable HTTP)](https://toloka.ai) ※ 2차 출처, AAIF 기부 세부사항 1차 미확인으로 제외
- [medium.com — AI 에이전트 감독 역량 트렌드](https://medium.com)
- [omega.ac — 요구사항 정의 생략 비용](https://omega.ac)

## 위키화 후보

- `pgvector` — PostgreSQL 벡터 검색 확장, ACID + RAG 단일 DB 통합 패턴 (`concepts/pgvector.md`) — 기존 `rag.md`에 링크 추가
- `MCP Streamable HTTP` — 기존 `concepts/mcp.md`(또는 승격 대기 #44) 내 섹션으로 추가, 독립 노트 불필요

## 프로필 반영 후보 (저위험)

- `pgvector` 패턴 — 벡터 검색 인프라 선택 기준으로 상식화, RAG 설계 논의 시 활용
- `Streamable HTTP (MCP)` — MCP 전송 계층 논의 시 무상태 수평확장 옵션으로 언급 가능

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

_(없음 — 기존 `wiki-linter` 에이전트가 AI 큐레이션 노트 검증 역할을 이미 담당)_
