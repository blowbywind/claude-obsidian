---
title: 승격 검토 큐 (promotion-review-queue)
type: query
status: review
count: 95
---

# 승격 검토 큐 — _review-queue 초안 95개

> 봇 자가학습에서 파생된 위키화 후보 초안입니다. **삭제·자동승격 없음.** 각 항목을 검토 후 `승격/보류/폐기`에 체크하고 "승격분 적용해"라고 지시하면 체크된 것만 정식 concepts/로 이동합니다.

### 1. Base UI vs Radix (shadcn 프리미티브 선택)
- 토픽: `2026-06-20-arthur-base-ui-vs-radix-shadcn-프리미티브-선택`
- 출처: [[episodic/2026-06-20-arthur-learning]]
- 요약: Base UI vs Radix (shadcn 프리미티브 선택) — components.json 전환 방식·번들/컴포넌트 차이·전환 기준 정리 (
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 2. CSS `contrast
- 토픽: `2026-06-20-arthur-css-contrast`
- 출처: [[episodic/2026-06-20-arthur-learning]]
- 요약: CSS `contrast-color()` 함수 — 접근성 자동화 + 동적 테마링 신규 CSS 기능, 브라우저 지원 및 폴백 전략 포함
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 3. css
- 토픽: `2026-06-20-arthur-css`
- 출처: [[episodic/2026-06-20-arthur-learning]]
- 요약: css-cascade-layers-design-system — @layer 표준 레이어 순서 및 디자인 시스템 적용 패턴
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 4. shadcn CLI v4 워크플로
- 토픽: `2026-06-20-arthur-shadcn-cli-v4-워크플로`
- 출처: [[episodic/2026-06-20-arthur-learning]]
- 요약: shadcn CLI v4 워크플로 — `--dry-run/--diff/--view` 검수 플래그 + Presets 엔진 활용 패턴
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 5. shadcn
- 토픽: `2026-06-20-arthur-shadcn`
- 출처: [[episodic/2026-06-20-arthur-learning]]
- 요약: shadcn-ui-2026-update — Base UI migration(`asChild` 제거), Luma 테마, Component Comp
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 6. Zustand v5 슬라이스 패턴
- 토픽: `2026-06-20-arthur-zustand-v5-슬라이스-패턴`
- 출처: [[episodic/2026-06-20-arthur-learning]]
- 요약: Zustand v5 슬라이스 패턴 — `useShallow`·slice 구성·Next.js 하이드레이션 전략 실무 레퍼런스
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 7. archive
- 토픽: `2026-06-20-dex-archive`
- 출처: [[episodic/2026-06-20-dex-learning]]
- 요약: `archive-strategy` — move-not-delete 원칙, 아카이브 폴더 운영 기준, 비활성 토픽 판단 조건 (기존 `note-l
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 8. decision
- 토픽: `2026-06-20-dex-decision`
- 출처: [[episodic/2026-06-20-dex-learning]]
- 요약: `decision-fatigue-pkm.md` — 캡처마다 분류 결정 강요 시 인지 자원 고갈, `capture-first` 원칙의 근거 개념
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 9. MOC (Maps of Content)
- 토픽: `2026-06-20-dex-moc-maps-of-content`
- 출처: [[episodic/2026-06-20-dex-learning]]
- 요약: `MOC (Maps of Content)` — 단일 폴더 제약을 우회하는 wikilink 기반 다중 맥락 인덱스 패턴. 폴더·태그와 역할 분리 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 10. obsidian
- 토픽: `2026-06-20-dex-obsidian`
- 출처: [[episodic/2026-06-20-dex-learning]]
- 요약: `obsidian-cli` — 2026-02 출시 공식 CLI; 볼트 자동화 파이프라인 진입점.
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 11. taxonomy
- 토픽: `2026-06-20-dex-taxonomy`
- 출처: [[episodic/2026-06-20-dex-learning]]
- 요약: `taxonomy-brittleness.md` — 고정 태그 트리의 시간적 부패 vs wikilink 그래프의 견고성
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 12. Execution
- 토픽: `2026-06-20-haeri-execution`
- 출처: [[episodic/2026-06-20-haeri-learning]]
- 요약: Execution-Aware 테스트 생성: 정적 코드 기반 LLM 테스트의 한계와 런타임 피드백 기반 대안 패턴 (TestWeaver)
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 13. llm
- 토픽: `2026-06-20-haeri-llm`
- 출처: [[episodic/2026-06-20-haeri-learning]]
- 요약: `llm-judge-bias-mitigation` — LLM-judge 5대 편향과 앙상블·프롬프트 완화법 (기존 agent-evaluation
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 14. Mutation
- 토픽: `2026-06-20-haeri-mutation`
- 출처: [[episodic/2026-06-20-haeri-learning]]
- 요약: Mutation-Guided Test Generation (ACH 패턴) — 커버리지 % 대신 미탐지 결함(mutant)을 타깃으로 테스트를 생
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 15. non
- 토픽: `2026-06-20-haeri-non`
- 출처: [[episodic/2026-06-20-haeri-learning]]
- 요약: `non-deterministic-agent-testing` — 비결정성 1급 처리, mock-DI/quarantine/객관적 검증 시나리오 원
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 16. RAG Triad Evaluation
- 토픽: `2026-06-20-haeri-rag-triad-evaluation`
- 출처: [[episodic/2026-06-20-haeri-learning]]
- 요약: RAG Triad Evaluation: Faithfulness/Context Recall/Answer Relevance 3지표 체계 — LLM 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 17. Tree of Thoughts (ToT) 프롬프팅
- 토픽: `2026-06-20-haeri-tree-of-thoughts-tot-프롬프팅`
- 출처: [[episodic/2026-06-20-haeri-learning]]
- 요약: Tree of Thoughts (ToT) 프롬프팅 — CoT의 선형 추론을 트리 구조 분기 탐색으로 확장. 복잡한 테스트 시나리오 생성 시 활용
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 18. Definition of Ready (DoR)
- 토픽: `2026-06-20-kiel-definition-of-ready-dor`
- 출처: [[episodic/2026-06-20-kiel-learning]]
- 요약: Definition of Ready (DoR): 스프린트 투입 전 최소 품질 게이트 — INVEST 기준 외 추가 체크포인트로 활용
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 19. EARS notation
- 토픽: `2026-06-20-kiel-ears-notation`
- 출처: [[episodic/2026-06-20-kiel-learning]]
- 요약: EARS notation — 인수 조건 모호성 제거 구문 패턴, 백로그 작성 실무 표준
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 20. EARS 표기법
- 토픽: `2026-06-20-kiel-ears-표기법`
- 출처: [[episodic/2026-06-20-kiel-learning]]
- 요약: EARS 표기법: AI 에이전트 호환 요구사항 작성 문법 — 기획자가 직접 적용 가능한 구조화 표기법
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 21. Figma Make
- 토픽: `2026-06-20-kiel-figma-make`
- 출처: [[episodic/2026-06-20-kiel-learning]]
- 요약: Figma Make: PRD 작성 전 인터랙티브 플로우 시각화 도구 — 엣지케이스 조기 발견, 문서 전 정렬(align-before-write)
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 22. SDD 3문서 패턴
- 토픽: `2026-06-20-kiel-sdd-3문서-패턴`
- 출처: [[episodic/2026-06-20-kiel-learning]]
- 요약: SDD 3문서 패턴: Kiro의 requirements/design/tasks 분리 구조 — PRD 산출물 재편 기준
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 23. Spec
- 토픽: `2026-06-20-kiel-spec`
- 출처: [[episodic/2026-06-20-kiel-learning]]
- 요약: Spec-Driven Development (SDD) — PRD를 코드 생성 소스로 삼는 방법론, Spec-Kit·constitution·EAR
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 24. A2A Protocol
- 토픽: `2026-06-20-lian-a2a-protocol`
- 출처: [[episodic/2026-06-20-lian-learning]]
- 요약: A2A Protocol — MCP와 짝을 이루는 에이전트 간 통신 표준(Linux Foundation 관리, v1.0, Agent Cards 기
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 25. AI 수학 연구 에이전트
- 토픽: `2026-06-20-lian-ai-수학-연구-에이전트`
- 출처: [[episodic/2026-06-20-lian-learning]]
- 요약: AI 수학 연구 에이전트 — AI Co-Mathematician 패턴: 병렬 에이전트 + 정리 증명 + 문헌 검색 조합으로 FrontierMat
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 26. LangGraph
- 토픽: `2026-06-20-lian-langgraph`
- 출처: [[episodic/2026-06-20-lian-learning]]
- 요약: LangGraph — 멀티에이전트 프레임워크 비교(vs CrewAI, AutoGen) 포함 개념 노트화 권장
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 27. tanstack
- 토픽: `2026-06-20-lian-tanstack`
- 출처: [[episodic/2026-06-20-lian-learning]]
- 요약: `tanstack-start.md` — Vite+Nitro 기반 client-first React 풀스택 프레임워크, Next.js 대안 (신규
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 28. Vercel AI SDK 5
- 토픽: `2026-06-20-lian-vercel-ai-sdk-5`
- 출처: [[episodic/2026-06-20-lian-learning]]
- 요약: Vercel AI SDK 5 — 풀스택 AI 앱 표준 SDK, `UIMessage/ModelMessage` 아키텍처·에이전트 루프 제어 패턴 정
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 29. 기존 `mcp.md` 업데이트
- 토픽: `2026-06-20-lian-기존-mcp-md-업데이트`
- 출처: [[episodic/2026-06-20-lian-learning]]
- 요약: 기존 `mcp.md` 업데이트 — 2026-07-28 신규 스펙(stateless core/Extensions/Tasks/MCP Apps) 반영
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 30. Bento Grid 레이아웃 패턴
- 토픽: `2026-06-20-rina-bento-grid-레이아웃-패턴`
- 출처: [[episodic/2026-06-20-rina-learning]]
- 요약: Bento Grid 레이아웃 패턴 — CSS Grid `grid-template-areas` + span 기반 불규칙 카드 격자; 모바일 fal
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 31. dtcg
- 토픽: `2026-06-20-rina-dtcg`
- 출처: [[episodic/2026-06-20-rina-learning]]
- 요약: `dtcg-design-tokens-표준` — W3C DTCG v2025.10 포맷 모듈, 3계층 구조 표준화 (기존 shadcn-토큰-계층 노
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 32. HTML Invoker Commands API 패턴
- 토픽: `2026-06-20-rina-html-invoker-commands-api-패턴`
- 출처: [[episodic/2026-06-20-rina-learning]]
- 요약: HTML Invoker Commands API 패턴 — `commandfor`/`command` 속성으로 JS 없이 dialog·popover 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 33. scroll
- 토픽: `2026-06-20-rina-scroll`
- 출처: [[episodic/2026-06-20-rina-learning]]
- 요약: `scroll-driven-animations-패턴` — CSS scroll/view timeline 베이스라인 + motion-safe 접근성
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 34. shadcn/ui Rhea 스타일
- 토픽: `2026-06-20-rina-shadcn-ui-rhea-스타일`
- 출처: [[episodic/2026-06-20-rina-learning]]
- 요약: shadcn/ui Rhea 스타일: compact density 적용 시기·기준(밀도 높은 product UI), Rhea vs Default/
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 35. WCAG 3.0 로드맵
- 토픽: `2026-06-20-rina-wcag-3-0-로드맵`
- 출처: [[episodic/2026-06-20-rina-learning]]
- 요약: WCAG 3.0 로드맵: 2026 Working Draft 현황 + 2028 이후 최종 권고안 예정 타임라인 정리 노트
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 36. Expand
- 토픽: `2026-06-20-roun-expand`
- 출처: [[episodic/2026-06-20-roun-learning]]
- 요약: Expand-Contract 마이그레이션 패턴 — 무중단 스키마 변경 3단계 절차, Prisma CONCURRENTLY 우회법
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 37. JWT 알고리즘 혼동 공격
- 토픽: `2026-06-20-roun-jwt-알고리즘-혼동-공격`
- 출처: [[episodic/2026-06-20-roun-learning]]
- 요약: JWT 알고리즘 혼동 공격 — RS256 서버에 HS256 위조 토큰 전송 공격 원리·방어 패턴 (2026 CVE 포함)
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 38. owasp
- 토픽: `2026-06-20-roun-owasp`
- 출처: [[episodic/2026-06-20-roun-learning]]
- 요약: `owasp-top10-2025.md` — BAC#1(SSRF 편입)·Misconfig#2·API BOLA 정리 (기존 web-security-
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 39. PostgreSQL Partial & Composite Index 패턴
- 토픽: `2026-06-20-roun-postgresql-partial-composite-index-패턴`
- 출처: [[episodic/2026-06-20-roun-learning]]
- 요약: PostgreSQL Partial & Composite Index 패턴: 조건부 인덱스 설계 기준, 컬럼 순서 규칙, 쓰기 성능 트레이드오프 정
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 40. prisma
- 토픽: `2026-06-20-roun-prisma`
- 출처: [[episodic/2026-06-20-roun-learning]]
- 요약: `prisma-7-rust-free-queryCompiler.md` — Rust 엔진 제거·driverAdapters 필수·성능/번들 변화 (기
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 41. deterministic
- 토픽: `2026-06-20-snow-deterministic`
- 출처: [[episodic/2026-06-20-snow-learning]]
- 요약: deterministic-orchestration-hybrid — 결정론(기본)+동적(가변 지점 한정) 하이브리드 라우팅 패턴, Conducto
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 42. Enterprise AI Governance Gap 2026
- 토픽: `2026-06-20-snow-enterprise-ai-governance-gap-2026`
- 출처: [[episodic/2026-06-20-snow-learning]]
- 요약: Enterprise AI Governance Gap 2026 — 72% 배포/60% 거버넌스 부재 통계, 주요 보안 사고 패턴, Autobots
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 43. generator
- 토픽: `2026-06-20-snow-generator`
- 출처: [[episodic/2026-06-20-snow-learning]]
- 요약: generator-critic-quality-gate — 별도 judge 모델·per-metric 임계값 기반 산출물 검증 패턴 (기존 gene
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 44. MCP (Model Context Protocol)
- 토픽: `2026-06-20-snow-mcp-model-context-protocol`
- 출처: [[episodic/2026-06-20-snow-learning]]
- 요약: MCP (Model Context Protocol): 에이전트-툴 통신 업계 표준으로 부상, VS Code·JetBrains 등 채택 현황 정리
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 45. Microsoft Agent Framework 1.0
- 토픽: `2026-06-20-snow-microsoft-agent-framework-1-0`
- 출처: [[episodic/2026-06-20-snow-learning]]
- 요약: Microsoft Agent Framework 1.0 — AutoGen + Semantic Kernel 통합 경위, 마이그레이션 경로, .NET
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 46. 에이전트 루프 비용 패턴
- 토픽: `2026-06-20-snow-에이전트-루프-비용-패턴`
- 출처: [[episodic/2026-06-20-snow-learning]]
- 요약: 에이전트 루프 비용 패턴: 2차 증가 메커니즘, 실제 사례($47k), 컨텍스트 요약 전략 문서화
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 47. concepts/container
- 토픽: `2026-06-20-stellina-concepts-container`
- 출처: [[episodic/2026-06-20-stellina-learning]]
- 요약: `concepts/container-supply-chain-security.md` — SBOM·SLSA·Cosign 서명·Trivy 스캔 게이트
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 48. concepts/otel
- 토픽: `2026-06-20-stellina-concepts-otel`
- 출처: [[episodic/2026-06-20-stellina-learning]]
- 요약: `concepts/otel-docker-observability.md` — OTel Collector docker_stats + filelog 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 49. concepts/progressive
- 토픽: `2026-06-20-stellina-concepts-progressive`
- 출처: [[episodic/2026-06-20-stellina-learning]]
- 요약: `concepts/progressive-delivery.md` — blue-green/canary/feature flag·메트릭 게이트 롤백을 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 50. concepts/supply
- 토픽: `2026-06-20-stellina-concepts-supply`
- 출처: [[episodic/2026-06-20-stellina-learning]]
- 요약: `concepts/supply-chain-security.md` — 소프트웨어 공급망 공격 벡터(mutable action refs, 타사 패키
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 51. css
- 토픽: `2026-06-21-arthur-css`
- 출처: [[episodic/2026-06-21-arthur-learning]]
- 요약: `css-anchor-positioning-패턴` — `anchor()` / `@position-try` / popover attribute 조
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 52. shadcn
- 토픽: `2026-06-21-arthur-shadcn`
- 출처: [[episodic/2026-06-21-arthur-learning]]
- 요약: `shadcn-ui-sera-스타일` — Sera vs Rhea vs Luma 3종 compact 밀도 스펙트럼 비교 및 용도 선택 기준
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 53. zustand
- 토픽: `2026-06-21-arthur-zustand`
- 출처: [[episodic/2026-06-21-arthur-learning]]
- 요약: `zustand-tanstack-query-분리-원칙` — 서버 상태(TanStack Query)와 클라이언트 상태(Zustand) 역할 경계 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 54. atomic
- 토픽: `2026-06-21-dex-atomic`
- 출처: [[episodic/2026-06-21-dex-learning]]
- 요약: atomic-note-design — 단일 주장 노트 설계 원칙: 제목=명제, 내용=단일 아이디어, 두 아이디어=분리 기준
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 55. obsidian
- 토픽: `2026-06-21-dex-obsidian`
- 출처: [[episodic/2026-06-21-dex-learning]]
- 요약: `obsidian-bases-formula-limits` — Bases formula 한계(인라인 필드 불가, circular ref, Dura
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 56. pkm
- 토픽: `2026-06-21-dex-pkm`
- 출처: [[episodic/2026-06-21-dex-learning]]
- 요약: `pkm-decision-fatigue` — 분류 결정 인지 비용 누적 문제와 capture-first 해법
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 57. AI vs 인간 테스트 이중 컨테이너 전략
- 토픽: `2026-06-21-haeri-ai-vs-인간-테스트-이중-컨테이너-전략`
- 출처: [[episodic/2026-06-21-haeri-learning]]
- 요약: AI vs 인간 테스트 이중 컨테이너 전략: 신뢰 수준별 분리 운영·크로스 검증 절차를 E2E 테스트 아키텍처 노트로 정리
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 58. Data Contract 패턴
- 토픽: `2026-06-21-haeri-data-contract-패턴`
- 출처: [[episodic/2026-06-21-haeri-learning]]
- 요약: Data Contract 패턴 — 파이프라인 프로듀서-컨슈머 계약 명문화 + PR 게이트 통합 방법론
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 59. golden
- 토픽: `2026-06-21-haeri-golden`
- 출처: [[episodic/2026-06-21-haeri-learning]]
- 요약: `golden-dataset-synthesis` — Synthesizer 기반 goldens 자동 생성, 전문가 검증 보완재 원칙, 100+ 예
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 60. llm
- 토픽: `2026-06-21-haeri-llm`
- 출처: [[episodic/2026-06-21-haeri-learning]]
- 요약: `llm-red-teaming` — Garak/Promptfoo/PyRIT/DeepTeam 4종 도구, 공격 벡터(roleplay·logic t
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 61. pass@k vs pass^k
- 토픽: `2026-06-21-haeri-pass-k-vs-pass-k`
- 출처: [[episodic/2026-06-21-haeri-learning]]
- 요약: pass@k vs pass^k — 에이전트 신뢰성 측정 두 지표 차이 및 배포 임계값 설정 기준 (기존 agent-evaluation-metri
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 62. TestART 패턴
- 토픽: `2026-06-21-haeri-testart-패턴`
- 출처: [[episodic/2026-06-21-haeri-learning]]
- 요약: TestART 패턴: LLM 테스트 생성 + 스택 트레이스 기반 자동 수리 루프 — 실패 피드백을 생성 루프에 내장하는 구체적 구현 패턴으로 문
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 63. Kiro Ambiguity Detection 패턴
- 토픽: `2026-06-21-kiel-kiro-ambiguity-detection-패턴`
- 출처: [[episodic/2026-06-21-kiel-learning]]
- 요약: Kiro Ambiguity Detection 패턴: 요구사항 모호성을 AI가 다중 해석 샘플링으로 감지·2-option 질문 표면화하는 기법. 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 64. MCP for PM 전략
- 토픽: `2026-06-21-kiel-mcp-for-pm-전략`
- 출처: [[episodic/2026-06-21-kiel-learning]]
- 요약: MCP for PM 전략: AI가 Jira·Notion 등을 직접 연동하는 워크플로우. SaaS PRD에 "agent-ready" 요구사항 항목
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 65. mcp
- 토픽: `2026-06-21-kiel-mcp`
- 출처: [[episodic/2026-06-21-kiel-learning]]
- 요약: mcp-for-pm-tools — PM 도구별 MCP 지원 현황 (Quire first-party, Linear/Jira 커뮤니티 서버) 및 A
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 66. Parano.ai
- 토픽: `2026-06-21-kiel-parano-ai`
- 출처: [[episodic/2026-06-21-kiel-learning]]
- 요약: Parano.ai: Slack-native 경량 경쟁 인텔리전스 — Klue/Crayon 대비 진입비용 낮은 신규 카테고리, 소규모 팀 CI 도
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 67. vibe
- 토픽: `2026-06-21-kiel-vibe`
- 출처: [[episodic/2026-06-21-kiel-learning]]
- 요약: vibe-pm — PM이 직접 vibe coding으로 기능 프로토타입을 검증 후 엔지니어에 인계하는 신규 워크플로우 패턴
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 68. 트래픽 기반 OpenAPI 자동생성
- 토픽: `2026-06-21-kiel-트래픽-기반-openapi-자동생성`
- 출처: [[episodic/2026-06-21-kiel-learning]]
- 요약: 트래픽 기반 OpenAPI 자동생성: Levo.ai의 eBPF 기반 스펙 역생성 접근 — 수동 명세 보완용 새 패턴
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 69. A2A v1.0 + Agent Payments Protocol (AP2)
- 토픽: `2026-06-21-lian-a2a-v1-0-agent-payments-protocol-ap2`
- 출처: [[episodic/2026-06-21-lian-learning]]
- 요약: A2A v1.0 + Agent Payments Protocol (AP2) — 에이전트 간 결제/과금 표준 프로토콜 포함 v1.0 상세 (MCP와
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 70. ai
- 토픽: `2026-06-21-lian-ai`
- 출처: [[episodic/2026-06-21-lian-learning]]
- 요약: `ai-agent-memory-patterns` — 2026년 생산 패턴 5종·벤치마크 3종(LoCoMo/LongMemEval/BEAM) 정리,
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 71. anthropic
- 토픽: `2026-06-21-lian-anthropic`
- 출처: [[episodic/2026-06-21-lian-learning]]
- 요약: `anthropic-cowork` — Claude Code의 일반 컴퓨팅 확장 제품, 에이전트 범용화 전략 맥락 포함
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 72. Claude Fable/Mythos 모델 체계
- 토픽: `2026-06-21-lian-claude-fable-mythos-모델-체계`
- 출처: [[episodic/2026-06-21-lian-learning]]
- 요약: Claude Fable/Mythos 모델 체계 — Anthropic이 내부 연구 티어(Mythos)와 공개 티어(Fable)를 분리 운영; Fa
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 73. Gemini 3.5 Flash 스펙 노트
- 토픽: `2026-06-21-lian-gemini-3-5-flash-스펙-노트`
- 출처: [[episodic/2026-06-21-lian-learning]]
- 요약: Gemini 3.5 Flash 스펙 노트 — 벤치마크·가격·컨텍스트 창·MCP Atlas 점수 한 곳에 정리
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 74. OpenCode
- 토픽: `2026-06-21-lian-opencode`
- 출처: [[episodic/2026-06-21-lian-learning]]
- 요약: OpenCode — LSP 통합·MCP 지원 오픈소스 코딩 에이전트; Claude Code 대안으로 160K 스타, 7.5M MAU 달성
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 75. CSS Anchor Positioning 패턴
- 토픽: `2026-06-21-rina-css-anchor-positioning-패턴`
- 출처: [[episodic/2026-06-21-rina-learning]]
- 요약: CSS Anchor Positioning 패턴 — Baseline 2026 브라우저 지원 현황, 핵심 속성 3개(`anchor-name`·`po
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 76. css
- 토픽: `2026-06-21-rina-css`
- 출처: [[episodic/2026-06-21-rina-learning]]
- 요약: `css-scroll-driven-animations` — `animation-timeline: scroll()/view()` 2종 비교·디자인
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 77. shadcn/ui Luma vs Rhea 스타일 비교
- 토픽: `2026-06-21-rina-shadcn-ui-luma-vs-rhea-스타일-비교`
- 출처: [[episodic/2026-06-21-rina-learning]]
- 요약: shadcn/ui Luma vs Rhea 스타일 비교 — 용도 기준(Luma=브랜드형 소프트 UI, Rhea=밀도 높은 product UI), 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 78. tailwind
- 토픽: `2026-06-21-rina-tailwind`
- 출처: [[episodic/2026-06-21-rina-learning]]
- 요약: `tailwind-v4-3-scrollbar-utilities` — first-party `scrollbar-thin/none/auto` + 색
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 79. wcag
- 토픽: `2026-06-21-rina-wcag`
- 출처: [[episodic/2026-06-21-rina-learning]]
- 요약: `wcag-2-2-sc-2-4-11-focus-appearance` — 포커스 인디케이터 최소 면적·대비 요건 + `:focus-visible`
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 80. AsyncLocalStorage 요청 컨텍스트 패턴
- 토픽: `2026-06-21-roun-asynclocalstorage-요청-컨텍스트-패턴`
- 출처: [[episodic/2026-06-21-roun-learning]]
- 요약: AsyncLocalStorage 요청 컨텍스트 패턴 — requestId/tenantId 전파, Fastify 훅 연동, 로깅·오텔 통합 구현 
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 81. BullMQ 프로덕션 패턴
- 토픽: `2026-06-21-roun-bullmq-프로덕션-패턴`
- 출처: [[episodic/2026-06-21-roun-learning]]
- 요약: BullMQ 프로덕션 패턴 — FlowProducer DAG, removeOnComplete TTL, sandboxed worker 분리, fa
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 82. bullmq
- 토픽: `2026-06-21-roun-bullmq`
- 출처: [[episodic/2026-06-21-roun-learning]]
- 요약: `bullmq-v5-patterns.md` — BullMQ v5 Worker 분리, removeOnComplete, Flow Producer(D
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 83. DPoP (RFC 9449) 구현 패턴
- 토픽: `2026-06-21-roun-dpop-rfc-9449-구현-패턴`
- 출처: [[episodic/2026-06-21-roun-learning]]
- 요약: DPoP (RFC 9449) 구현 패턴 — proof JWT 구조(`jwk/htm/htu/jti/ath`), `jose` 라이브러리 코드 예시,
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 84. fastify
- 토픽: `2026-06-21-roun-fastify`
- 출처: [[episodic/2026-06-21-roun-learning]]
- 요약: `fastify-v5-migration-checklist.md` — v4→v5 브레이킹 변경 4종 + response schema 필수화 체크리
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 85. Prisma v7 TypeScript 엔진
- 토픽: `2026-06-21-roun-prisma-v7-typescript-엔진`
- 출처: [[episodic/2026-06-21-roun-learning]]
- 요약: Prisma v7 TypeScript 엔진 — Rust 제거, 3.4× 빠름, 번들 90% 감소, 배포 단순화 포인트 정리
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 86. claude
- 토픽: `2026-06-21-snow-claude`
- 출처: [[episodic/2026-06-21-snow-learning]]
- 요약: `claude-fable5-export-control` — 미 정부 수출통제로 frontier 모델이 72시간 만에 전면 차단된 사례; AI 거
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 87. GLM
- 토픽: `2026-06-21-snow-glm`
- 출처: [[episodic/2026-06-21-snow-learning]]
- 요약: GLM-5.2 — 최초 오픈웨이트 SWE-Bench Pro SOTA, 1M 컨텍스트, 2026-06 출시
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 88. MCP + A2A 에이전트 프로토콜 스택
- 토픽: `2026-06-21-snow-mcp-a2a-에이전트-프로토콜-스택`
- 출처: [[episodic/2026-06-21-snow-learning]]
- 요약: MCP + A2A 에이전트 프로토콜 스택 — 수직(MCP: tool) + 수평(A2A: agent delegation) 2-레이어 구조, Lin
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 89. mcp
- 토픽: `2026-06-21-snow-mcp`
- 출처: [[episodic/2026-06-21-snow-learning]]
- 요약: `mcp-apps-html-ui` — MCP가 텍스트→sandboxed iframe HTML UI로 확장된 시점과 에이전트 UX 함의
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 90. τ
- 토픽: `2026-06-21-snow-note`
- 출처: [[episodic/2026-06-21-snow-learning]]
- 요약: τ-bench — 동적 유저+툴 시뮬레이션 기반 에이전트 실세계 평가 벤치마크 (Sierra/Princeton, 2026)
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 91. 오픈소스 LLM 경쟁 구도 2026
- 토픽: `2026-06-21-snow-오픈소스-llm-경쟁-구도-2026`
- 출처: [[episodic/2026-06-21-snow-learning]]
- 요약: 오픈소스 LLM 경쟁 구도 2026 — Nemotron 3 Ultra(550B 허용), MiniMax M3(1M ctx), Kimi K2.7(1
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 92. concepts/dora
- 토픽: `2026-06-21-stellina-concepts-dora`
- 출처: [[episodic/2026-06-21-stellina-learning]]
- 요약: `concepts/dora-metrics-dx-core4.md` — DORA 4지표 + DX Core 4 보완 모델, AI 도입 역설, Good
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 93. concepts/falco
- 토픽: `2026-06-21-stellina-concepts-falco`
- 출처: [[episodic/2026-06-21-stellina-learning]]
- 요약: `concepts/falco-runtime-security.md` — Falco eBPF 드라이버 기반 컨테이너 런타임 이상 탐지, Falcos
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 94. concepts/slo
- 토픽: `2026-06-21-stellina-concepts-slo`
- 출처: [[episodic/2026-06-21-stellina-learning]]
- 요약: `concepts/slo-error-budget-ci-gate.md` — SLI/SLO/에러 버짓 → 배포 게이트 3단계 정책 (Promethe
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

### 95. concepts/sops
- 토픽: `2026-06-21-stellina-concepts-sops`
- 출처: [[episodic/2026-06-21-stellina-learning]]
- 요약: `concepts/sops-age-gitops-secrets.md` — SOPS+age로 시크릿 값 암호화 후 git 커밋, CI/CD reci
- 판정: [ ] 승격  [ ] 보류  [ ] 폐기

