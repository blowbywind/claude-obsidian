---
title: 하네스 엔지니어링 (Harness Engineering)
type: concept
tags: [harness, ai-agent, context-engineering, system-design]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-harness-engineering-guide, 2026-06-07-ainow-claude-code-master-guide]
---

## 정의

AI 에이전트를 둘러싼 제약(Constraints)·툴(Tools)·피드백 루프(Feedback Loops)·관찰 시스템(Observability)의 총체를 설계하고 운영하는 기술 분야.

> "AI 에이전트가 실수를 할 때마다 그 실수를 다시는 반복하지 못하도록 해결책을 설계하는 것이다." — Mitchell Hashimoto, 2026.02.05

## 상세

### 탄생 배경

2026년 2월 HashiCorp 공동창업자 Mitchell Hashimoto의 블로그 'My AI Adoption Journey'에서 개념이 명확히 정의됐다. 며칠 후 OpenAI가 'Harness engineering: leveraging Codex in an agent-first world' 보고서를 발표하며 업계 전반에 확산됐다.

3가지 수렴 요인:
1. **모델 상품화**: 최상위 모델 간 성능 차이 감소 → 모델보다 시스템이 경쟁력 결정
2. **에이전트의 프로덕션 전환**: 2025년 데모 수준 → 2026년 실제 업무 투입
3. **신뢰성 병목**: 에이전트가 충분히 유용해졌지만 안정적으로 동작하지 않는 상태

### AI OS 비유 (Philipp Schmid)

| 컴퓨터 구성요소 | AI 시스템 대응 |
|----------------|---------------|
| CPU | AI 모델 (Claude, GPT 등) |
| RAM | 컨텍스트 윈도우 |
| 운영체제(OS) | **하네스** |
| 애플리케이션 | 에이전트 |
| 디바이스 드라이버 | MCP 서버 |

### 프롬프트 → 컨텍스트 → 하네스 3단계 진화

- **프롬프트 엔지니어링 (2022–2024)**: 한 번의 입력 최적화. Few-shot, Chain-of-Thought
- **컨텍스트 엔지니어링 (2025)**: 문맥 전체 설계. RAG, MCP, 메모리 시스템
- **하네스 엔지니어링 (2026~)**: 전체 시스템 운영 방식. 툴·제약·피드백·관찰 통합

### 5대 구성요소

1. **컨텍스트 엔지니어링** — CLAUDE.md, AGENTS.md, 아키텍처 문서
2. **건축적 제약조건** — 의존성 방향 강제, 커스텀 린터, 툴 접근 제어, CI/CD
3. **피드백 루프** — 에이전트 출력 자동 검증·수정 순환
4. **관찰 및 모니터링** — 행동 기록, 실패 패턴 분석
5. **인간 개입 지점** — 권한 모델, 고위험 결정의 인간 확인

### 7가지 법칙

1. 환경을 설계하라, 코드를 작성하지 마라
2. 실수에서 배우고 영구적으로 방지하라
3. 제약이 곧 생산성이다
4. 생성과 평가를 분리하라
5. 탈부착 가능하게 구축하라 (Rippable)
6. 성공은 조용히, 실패만 크게
7. 계획과 실행을 분리하라

### Claude Code에서의 하네스

| 하네스 구성요소 | Claude Code 구현 |
|----------------|-----------------|
| 컨텍스트 엔지니어링 | CLAUDE.md |
| 건축적 제약조건 | permissions 설정, 파일 수정 제한 |
| 피드백 루프 | Hooks (preToolUse/postToolUse/stop) |
| 관찰 | 트랜스크립트 로깅 |
| 인간 개입 | 기본 권한 모델, 승인 요구 |
| 점진적 정보 공개 | Skills |
| 병렬 처리 | Sub-agents |

## 관련 개념

- [[wiki/concepts/context-engineering|컨텍스트 엔지니어링]] — 하네스의 첫 번째 구성요소
- [[wiki/concepts/generator-evaluator-pattern|Generator-Evaluator 패턴]] — 하네스의 법칙 4 구현
- [[wiki/concepts/claude-md|CLAUDE.md]] — 하네스 컨텍스트 파일
- [[wiki/concepts/hooks|훅스]] — 하네스 피드백 루프 구현체
- [[wiki/concepts/boris-self-learning-loop|Boris 자기학습 루프]] — 실전 하네스 성장 방법론
- [[wiki/concepts/agentic-loop|에이전트 루프]] — 하네스가 제어하는 대상

## 관련 엔티티

- [[wiki/entities/mitchell-hashimoto|Mitchell Hashimoto]] — 개념 창시자
- [[wiki/entities/claude-code|Claude Code]] — 하네스 엔지니어링 내장 도구
- [[wiki/entities/anthropic|Anthropic]] — Generator-Evaluator 연구

## 출처

- [[wiki/sources/2026-06-07-harness-engineering-guide|하네스 엔지니어링 기초 가이드북]]
- [[wiki/sources/2026-06-07-ainow-claude-code-master-guide|에이나우 클로드코드 실전 마스터가이드]]
