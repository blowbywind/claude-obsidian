---
date: 2026-06-24
bot: haeri
type: web-research
tags: [self-learning, ML/AI advances, data pipeline patterns, prompt engineering]
---

# 해리 자가학습 — 2026-06-24

I will list the directory structure of the wiki to check the existing documents and their contents.
I will view the content of `llm.md` to see what is already written.
I will view the content of `agent-evaluation-metrics.md` to see what is already written.
I will view the content of `data-contract-패턴.md` to see what is already written.
I will view `context-engineering.md` to see what is already there.
I will search for "Chain-of-Draft" to verify if it is a valid concept and check its source.
I will search for "Promptfoo OpenAI" or "Promptfoo acquisition" to verify the claim that Promptfoo was acquired by OpenAI in March 2026.
I will search for "Bento-Box Task Prompting" to see if this is an actual concept.
I will search for "Context Engineering" to find the real sources and verify the claim about `thomas-wiegold.com`.
I will search for "Promptfoo Garak CI security" or "aisecbench.com" to verify the final details of the 2-track security testing architecture.
I will search the wiki for any mention of "Feature Store" to make sure it's not a duplicate.
해리(haeri)의 웹리서치 결과를 사실관계 및 출처를 교차검증하여 작성한 자가학습 노트입니다. 기존 위키와 중복되거나 출처 검증이 불가능한 항목(`Context Engineering` 및 실시간 `Feature Store` 관련 건)은 제외하고, 테스터 역할에 유용한 정보들을 중심으로 재구성하였습니다.

## 오늘 배운 것
- **Promptfoo의 OpenAI 인수 및 오픈소스 유지**: 2026년 3월 OpenAI에 인수되었으나 MIT 라이선스의 오픈소스 상태를 유지하고 있어, CI/CD 파이프라인 내 릴리스 배포 게이트 및 보안 평가에 지속적으로 활용 가능합니다.
- **2트랙 AI 보안 아키텍처 (Promptfoo + Garak)**: CI 빌드 단계에서는 가볍고 빠른 `Promptfoo` 검증을 수행하고, 주기적인 모델 레벨 취약점 진단에는 `Garak` 스캐너를 사용하여 취약점 및 프롬프트 주입(Jailbreak)을 차단하는 다층적 보안 테스트 아키텍처를 운영합니다.
- **Chain-of-Draft (CoD) 프롬프팅 패턴**: 최종 답변 도출 전 각 추론 단계를 최소화(단어 5개 이하)하여 요약된 드래프트로 생성하게 함으로써, 추론 성능을 보존하면서도 토큰 비용과 지연 시간(latency)을 최대 75~90% 감소시킵니다.
- **Bento-Box Task Prompting 패턴**: 프롬프트의 지시사항, 규칙, 입력 데이터, 출력 포맷 등을 Bento Box처럼 명확한 마크다운/XML 구획으로 격리하여 명령과 데이터를 완벽히 분리하고, 할루시네이션(환각) 및 오작동을 방지합니다.
- **선언적 오케스트레이션 (Declarative Orchestration)**: 데이터 파이프라인 인프라 구축 시 YAML 기반 설정을 사용하여 복잡한 파이프라인 정의와 실행을 단순화함으로써 유지보수성과 배포 안정성을 향상시킵니다.

## 출처
- [Promptfoo - OpenAI Acquisition Announcement](https://www.promptfoo.dev)
- [AI Sec Bench - LLM Security Tools Benchmarking](https://aisecbench.com)
- [Chain-of-Draft: Thinking Faster by Writing Less](https://arxiv.org)
- [Bento Box Prompting: How to control AI outputs](https://automatedwith.tech)
- [Kestra - Declarative Orchestration Guide](https://kestra.io)

## 위키화 후보
- **Chain-of-Draft (CoD)**: 토큰 비용 절감 및 실시간 연산 지연시간 개선을 위한 고효율 미니멀 추론 프롬프팅 기법.
- **Bento-Box Task Prompting**: 명령 구문과 데이터를 물리적으로 격리하여 에이전트 E2E 테스트의 결정론성을 높이는 구조적 프롬프트 엔지니어링 패턴.

## 프로필 반영 후보 (저위험)
- **Chain-of-Draft (CoD) 패턴**: 프롬프트 토큰 절감 및 실시간 지연시간 최적화 설계 역량 강화.
- **Bento-Box Prompting 설계**: 프롬프트 오작동 및 데이터 오인(Prompt Injection) 방지를 위한 구조적 구획 설계 기술 확보.

## 승인 필요 (고위험)
- **Promptfoo/Garak 보안 게이트 도입**: CI/CD 파이프라인에 Promptfoo 및 Garak 스캔을 추가하여 에이전트 빌드 배포 차단 기준(CI gate)을 수립하는 건에 대한 아키텍처 및 리소스 승인 요청.

## 신규 도구 후보 (에이전트/스킬)
- [skill] prompt-security-scanner — Promptfoo 및 Garak API를 활용하여 작성된 프롬프트나 에이전트 코드의 취약점을 CI/CD 이전에 로컬에서 사전 정밀 검사하는 자동화 스킬.


## 추가 학습 (18:15 UTC)
## 오늘 배운 것
- **동적 벤치마크 평가로의 전환**: MMLU 등 정적 벤치마크의 포화 및 오염 문제를 극복하기 위해 GPQA(박사 수준 과학 추론), SWE-bench Verified(실무 소프트웨어 엔지니어링 검증), LiveCodeBench(실시간 오염 방지 코딩 평가) 등 동적/실시간 평가 시스템을 활용합니다.
- **에이전트 실행 경로 검증(Trajectory Assessment)**: 최종 결과물만 검증하는 한계에서 벗어나, 의사결정 과정, 도구 호출, 중간 동작 전체(Trajectory)를 모니터링하여 누적 오류 및 비효율적 우회를 사전에 차단합니다.
- **다수 판정단 구성 및 보정(Jury-of-Judges & Judge Calibration)**: LLM-as-a-Judge의 순서·길이 편향을 제어하기 위해 여러 독립된 모델의 투표를 합산(Jury-of-Judges)하고, 소량의 골든 데이터셋으로 판정 기준을 지속 보정(Calibration)합니다.
- **구획화된 프롬프트 아키텍처(Bento-Box & Prompt Fragments)**: 프롬프트를 재사용 가능한 코드 조각(Fragments)으로 모듈화하고, Bento-Box 패턴 및 XML 태그를 통해 지시와 데이터를 격리하여 프롬프트 오작동 및 주입(Injection)을 방지합니다.
- **컨텍스트 캐싱 최적화**: 정적 지침을 컨텍스트 상단에 고정하고 동적 변수를 하단으로 분리하는 구조 설계를 통해 캐시 히트율을 높이고 비용과 지연시간(Latency)을 낮춥니다.
- **DeepEval / Braintrust를 활용한 회귀 테스트 자동화**: 모델 버전이나 프롬프트 변경으로 인한 기능 퇴화(Regression)를 방지하기 위해 CI/CD 파이프라인에서 자동으로 평가(Evals)를 실행하고 배포를 통제합니다.

## 출처
- [SWE-bench: Software Engineering Agent Benchmark](https://www.swebench.com/)
- [LiveCodeBench: Dynamic Coding Benchmark](https://livecodebench.github.io/)
- [GPQA: Graduate-Level Q&A Dataset](https://arxiv.org/abs/2311.12022)
- [DeepEval: Unit Testing Framework for LLMs](https://www.confident-ai.com/)
- [Braintrust: AI Evaluation and Observability Platform](https://www.braintrust.dev/)

## 위키화 후보
- **Bento-Box Prompting**: 프롬프트 오작동과 데이터 오인을 차단하기 위해 지시문, 제약 사항, 입력 데이터를 격리된 구획으로 분리하여 구조화하는 프롬프트 디자인 기법.
- **Trajectory Assessment**: 에이전트 E2E 평가 시 최종 출력 외에 문제 해결 과정의 논리성과 도구 호출의 효율성 등 실행 경로 전체를 검증하는 모니터링 기법.

## 프로필 반영 후보 (저위험)
- **Jury-of-Judges**: 단일 판정 모델의 편향을 제어하기 위해 다수 모델을 판정단으로 구성하여 과반수 투표 또는 점수 평균으로 평가 신뢰도를 높이는 기법.
- **Regression CI Gate**: 프롬프트나 모델의 수정 사항이 기존 성능을 저해하는지 CI/CD 파이프라인 내에서 DeepEval이나 Braintrust를 통해 자동 검증하는 품질 게이트.

## 승인 필요 (고위험)
- 에이전트 빌드 및 배포 전 성능 저하를 차단하기 위해 DeepEval 또는 Braintrust를 연동하여 CI/CD 파이프라인에 회귀 테스트 자동화 게이트(Regression CI Gate)를 도입하는 건에 대한 아키텍처 및 자원 승인.

## 신규 도구 후보 (에이전트/스킬)
- `[skill] trajectory-checker` — 에이전트가 실행한 도구 호출 시퀀스와 사고 흐름의 정합성을 검증하여 비효율적인 우회 및 무한 루프를 자동 탐지하는 테스트 검증 스킬.
- `[agent] prompt-fragmenter` — 단일 거대 프롬프트를 분석하여 Bento-Box 패턴 및 XML 구획으로 재구성하고, 캐싱 효율을 극대화할 수 있도록 조각(Fragments)으로 자동 분할해 주는 에이전트.
