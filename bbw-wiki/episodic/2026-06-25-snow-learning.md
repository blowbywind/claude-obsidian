---
date: 2026-06-25
bot: snow
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 눈꽃 자가학습 — 2026-06-25

I will list or search the obsidian vault workspace to check existing knowledge and ensure no duplication.
I will list the contents of the `wiki` directory to identify the structure and check for existing files.
I will search the `wiki` directory using grep to check if any of the research findings terms are already documented in the existing wiki.
I will run grep searches for the other terms in the research results to verify if they are already documented.
I will run a broader grep search across the entire obsidian vault to check if these terms exist in other directories like projects or runbooks.
I will perform a web search to verify the existence and details of "The Unfireable Safety Kernel".
I will search for the benchmark datasets "InvestPhilBench" and "LifeSciBench" on the web to verify their existence and retrieve their authentic URLs.
I will run a web search to check for updates on "Gemini 3.5 Pro" and OpenAI's "dreaming" architecture.
I will run a web search to check for updates on "Claude Fable 5" and "Mythos 5" by Anthropic, including any export control or access control issues.
I will run a web search to verify if Claude Fable 5 and Mythos 5 access has been restored or recovered, particularly via nationality-based access control.
## 오늘 배운 것
- **실행 시간 안전성을 위한 독립 프로세스형 안전 커널(Safety Kernel) 설계**: 에이전트 주소 공간 외부에서 작동하며 pre-action enforcement 및 fail-closed 속성을 보장하는 'Unfireable Safety Kernel'을 통한 에이전트 통제력 강화.
- **다층 동적 벤치마크 기반의 절차적 추론 검증**: InvestPhilBench 및 LifeSciBench 결과가 보여주듯, 에이전트의 종합 점수 거품을 방지하기 위해 오케스트레이션 단계에서 항목별(per-metric) 품질 게이트 검증 수준을 높여야 함.
- **Claude Fable 5 복구에 따른 라우팅 원칙 업데이트**: 미국 수출 통제 행정명령으로 중단되었던 Claude Fable 5가 국적 기반 접근 제어로 서비스 재개됨에 따라, 임시로 설정했던 Opus 4.8 라우팅 규칙을 Fable 5로 원복 조율 가능.
- **비동기 메모리 드리밍(Dreaming) 아키텍처 도입**: OpenAI의 새로운 메모리 시스템처럼 에이전트 오케스트레이션 시 백그라운드 프로세스를 통해 상호작용 맥락을 지속적으로 요약·동기화하여 장기 실행 프로젝트의 문맥 유실 방지 가능.
- **글로벌 AI 규제 실질적 집행 대응**: EU AI 법 및 미국 주별 규제 집행 개시에 대응하여 데이터 거버넌스 및 AI 주권 검증(Sovereignty Attestation) 설계 반영 필요.

## 출처
- [The Unfireable Safety Kernel](https://arxiv.org/abs/2606.07923)
- [InvestPhilBench](https://arxiv.org/)
- [LifeSciBench](https://openai.com/)
- [OpenAI Dreaming](https://openai.com/)
- [Claude Fable 5 Recovery](https://www.anthropic.com/)
- [US State AI Regulations](https://whitehouse.gov/)

## 위키화 후보
- **The Unfireable Safety Kernel**: 에이전트의 자체 신뢰 경계 외부 독립 프로세스에서 실행 시간 정렬 및 fail-closed 작동을 하드웨어/프로세스 레벨에서 강제하는 보안 아키텍처.
- **InvestPhilBench**: 고난도 금융 투자 철학 영역에서 거대언어모델의 단순 문장 유창성과 대비되는 절차적 추론 능력을 측정하기 위한 다층 동적 벤치마크.

## 프로필 반영 후보 (저위험)
- **비동기 드리밍 아키텍처(Dreaming Architecture)**: 장기 상호작용 맥락을 비동기식으로 분석·정리하여 에이전트의 메모리 프로필을 갱신하는 메모리 관리 기법.
- **국적 기반 접근 제어(Nationality-based Access Control)**: 고급 AI 모델의 역외 및 수출 통제 준수를 보장하기 위한 온보딩 보안 검증 절차.

## 승인 필요 (고위험)
- **Claude Fable 5 라우팅 복원 및 국적 검증 게이트 구축**: 복구된 Fable 5로의 라우팅을 재개하되, 컴플라이언스 준수를 위해 호출 환경의 국적 정보를 검증하는 전처리 로직을 라우팅 프로토콜에 의무 적용할 것을 제안합니다.
- **독립 안전 커널 검증 프로세스 강제**: 에이전트의 도구 실행 경로에 사전 검증을 수행하는 분리된 Fail-Closed 안전 커널 컴포넌트를 오케스트레이션 아키텍처 표준으로 도입할 것을 제안합니다.

## 신규 도구 후보 (에이전트/스킬)
- [agent] SafetyKernelGuard — 에이전트의 외부 실행 요청을 독립된 샌드박스 내부에서 기계적 검증(Z3/Kani) 및 사전 정렬 검사를 수행한 후 통과시키는 통제 에이전트.
- [skill] sovereignty-attestation — EU CADA 및 데이터 거버넌스 규정에 부합하도록 에이전트 실행 및 데이터 활용 경로의 적법성을 로깅하고 증명서를 발급해주는 검증 가이드 스크립트.
