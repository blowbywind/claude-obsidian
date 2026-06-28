---
date: 2026-06-25
bot: haeri
type: web-research
tags: [self-learning, ML/AI advances, data pipeline patterns, prompt engineering]
---

# 해리 자가학습 — 2026-06-25

## 오늘 배운 것
- **실행 중심의 에이전틱 벤치마크 표준화**: 기존 정적 질의응답식 평가의 포화를 해결하기 위해, 실제 깃허브(GitHub) 이슈를 해결하는 `SWE-bench Verified` 및 운영체제를 직접 제어하는 `OSWorld` 등 실질적인 도구 사용과 행동 능력을 검증하는 벤치마크가 주류로 안착함. [agent-evaluation-metrics.md](file:///home/bbw/obsidian-vault/bbw-wiki/wiki/concepts/agent-evaluation-metrics.md) 및 [ai-vs-인간-테스트-이중-컨테이너-전략.md](file:///home/bbw/obsidian-vault/bbw-wiki/wiki/concepts/ai-vs-%EC%9D%B8%EA%B0%84-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%9D%B4%EC%A4%91-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EC%A0%84%EB%9E%B5.md)의 AI 평가 자동화 지표로 참조 가능.
- **데이터 계약(Data Contract) 기반의 CI/CD 실시간 품질 제어**: 단순 스키마 오류를 넘어 비즈니스 로직(유효 범위, 참조 무결성 등)까지 명시하고, CI/CD 단계에서 실시간으로 검증을 자동화하는 `Gable` 및 `Okyline` 같은 도구가 활성화됨. [data-contract-패턴.md](file:///home/bbw/obsidian-vault/bbw-wiki/wiki/concepts/data-contract-%ED%8C%A8%ED%84%B4.md)의 데이터 품질 보증 및 파이프라인 검증용 빌드 차단 게이트에 활용 가능.
- **오염 방지 실시간 벤치마크 및 초고난도 학술 평가 도입**: 모델의 학습 데이터 오염 문제를 우회하기 위해 지속적으로 최신 코딩 문제를 수집하는 `LiveCodeBench`와 대학원 수준의 고난도 질문을 다루는 `Humanity's Last Exam (HLE)`이 고성능 추론 모델 검증의 표준으로 대두됨. [agent-evaluation-metrics.md](file:///home/bbw/obsidian-vault/bbw-wiki/wiki/concepts/agent-evaluation-metrics.md)의 모델 성능 비교 검증 기준으로 참조 가능.
- **구조화된 XML 태그 기반 프롬프트 모듈화 검증**: 역할, 작업, 입력, 출력 제약 사항을 XML 태그로 구획함으로써 컨텍스트 윈도우를 최적화하고 에이전트의 오동작을 줄이는 프롬프트 엔지니어링 설계가 표준화됨. [context-engineering.md](file:///home/bbw/obsidian-vault/bbw-wiki/wiki/concepts/context-engineering.md)와 연계하여 프롬프트 변경 사항 검증용 테스트 체크리스트로 활용 가능.
- **Model Context Protocol (MCP) 기반 실시간 컨텍스트 데이터 공급**: Zero-ETL 인프라의 확산과 함께 에이전트가 MCP 규격을 기반으로 실시간 맥락 데이터를 연동하고 쿼리할 수 있는 환경이 조성됨. [mcp-model-context-protocol.md](file:///home/bbw/obsidian-vault/bbw-wiki/wiki/concepts/mcp-model-context-protocol.md)를 확장하여 테스트 환경에서의 에이전트 데이터 공급 상태 검증에 활용 가능.

## 출처
- [Statworx: Physical AI and Robotics](https://www.statworx.com)
- [TestingXperts: Edge Computing and On-device AI](https://www.testingxperts.com)
- [TxMinds: Data Contract and Pipeline Quality](https://www.txminds.com)
- [Dataforest: Zero-ETL and MCP Integration](https://dataforest.ai)
- [Dev.to: 7 Prompt Engineering Techniques in 2026](https://dev.to/honestai/7-prompt-engineering-techniques-that-actually-work-in-2026-with-real-examples-3aj1)
- [Braintrust: Best AI Eval Tools for CI/CD Pipelines](https://www.braintrust.dev/articles/best-ai-evals-tools-cicd-2025)
- [Humanity's Last Exam: Expert-Level Benchmark](https://humanityslastexam.org)

## 위키화 후보
- `SWE-bench Verified`: AI 에이전트의 깃허브 실무 이슈 해결 능력을 검증하기 위해 500개의 정제된 과제로 구성된 실행 기반 벤치마크 표준.
- `Okyline`: 단일 실행 계약을 기반으로 데이터 유효성 및 실시간 품질 제어를 수행하는 실행 데이터 설계 도구.

## 프로필 반영 후보 (저위험)
- `Model Context Protocol (MCP) 테스팅`: 데이터 파이프라인에서 AI 에이전트로 유입되는 실시간 컨텍스트의 규격 정합성을 검증하는 역량.
- `실행 기반 에이전틱 벤치마크`: `OSWorld` 및 `SWE-bench Verified`와 같은 도구 사용 중심의 E2E 평가 환경 구축 기법.

## 승인 필요 (고위험)
- `데이터 파이프라인 E2E 테스트 스위트에 데이터 계약(Data Contract) 검증 도구 적용`: Gable 및 Okyline 같은 도구를 기존 PR 빌드 테스트에 추가하여 배포 전에 비즈니스 로직 및 컨트랙트 규격을 강제하는 파이프라인 테스트 규정 도입.

## 신규 도구 후보 (에이전트/스킬)
- `[agent] code-agent-evaluator` — SWE-bench Verified 규격을 로컬 테스팅 환경에 맞게 커스텀하여 에이전트의 실제 깃허브 코드 수정 능력을 로컬에서 CI 이전에 사전 테스트해주는 검증 에이전트.
