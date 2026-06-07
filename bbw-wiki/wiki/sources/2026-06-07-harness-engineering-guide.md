---
title: 하네스 엔지니어링 기초 가이드북
type: source
tags: [harness-engineering, context-engineering, ai-agent, ainow]
created: 2026-06-07
updated: 2026-06-07
origin: bbw-wiki/raw/하네스+엔지니어링+기초+가이드북.pdf
author: 에이나우(AINOW)
date_published: 2026-03-01
---

## 요약

2026년 2월 Mitchell Hashimoto가 정의하고 OpenAI가 보고서로 확산시킨 '하네스 엔지니어링' 개념을 체계화한 가이드북. 프롬프트→컨텍스트→하네스 3단계 진화 프레임으로 AI 에이전트 시스템 설계 패러다임의 전환을 설명하고, OpenAI·Anthropic·LangChain·Stripe·Cloudflare의 실제 적용 사례를 포함한다.

## 핵심 주장

- **하네스의 정의** (Hashimoto, 2026.02.05): "AI 에이전트가 실수를 할 때마다 그 실수를 다시는 반복하지 못하도록 해결책을 설계하는 것"
- **AI OS 비유** (Philipp Schmid): AI 모델=CPU, 컨텍스트 윈도우=RAM, 하네스=OS, 에이전트=애플리케이션
- **경쟁력은 모델이 아닌 시스템에서**: LangChain 실험 — 모델은 그대로, 하네스만 바꿔 15개 LLM 모두 최상위권으로 향상
- **생성과 평가 분리** (Anthropic): 에이전트는 자신의 작업을 객관적으로 평가할 수 없어 Generator-Evaluator를 반드시 분리해야 함
- **탈부착 가능 설계 (Rippable)**: Vercel은 에이전트 툴 80% 제거 후 오히려 성능 향상 — 하네스는 가볍고 쉽게 교체 가능해야 함

## 3단계 진화

| 구분 | 시기 | 초점 | 한계 |
|------|------|------|------|
| 프롬프트 엔지니어링 | 2022–2024 | 입력 최적화 (Few-shot, CoT) | 복잡한 작업 불가 |
| 컨텍스트 엔지니어링 | 2025 | 문맥 전체 설계 (RAG, MCP, 메모리) | 장기 안정성 부족 |
| 하네스 엔지니어링 | 2026~ | 전체 시스템 운영 방식 설계 | 연구 진행 중 |

## 하네스 5대 구성요소

1. **컨텍스트 엔지니어링** — CLAUDE.md·AGENTS.md, 아키텍처 문서, 실행 계획
2. **건축적 제약조건** — 의존성 방향 규칙, 커스텀 린터, 툴 접근 제어, CI/CD
3. **피드백 루프** — 에이전트 출력 자동 검증, 오류 시 자동 수정 순환
4. **관찰 및 모니터링** — 행동 기록, 실패 패턴 분석, 인간 개입 시점 파악
5. **인간 개입 지점** — 권한 모델, 고위험 결정의 인간 확인 구조

## 하네스 엔지니어링 7가지 법칙

1. 환경을 설계하라, 코드를 작성하지 마라 (OpenAI)
2. 실수에서 배우고 영구적으로 방지하라 (Hashimoto)
3. 제약이 곧 생산성이다 (LangChain)
4. 생성과 평가를 분리하라 (Anthropic)
5. 탈부착 가능하게 구축하라, Rippable (Vercel)
6. 성공은 조용히, 실패만 크게 (HumanLayer)
7. 계획과 실행을 분리하라 (Cloudflare, Boris Tane)

## 실전 사례 요약

- **OpenAI Codex**: 5개월, 인간 코드 0줄, 100만 줄 생성, 수동 대비 10배 속도
- **Anthropic**: Initializer Agent + Coding Agent 2단계 구조, context anxiety 해결
- **LangChain**: 모델 고정 + 하네스만 변경 → 15개 LLM 성능 전부 향상
- **Stripe**: 400개 내부 도구 MCP 연결, devbox 격리 샌드박스
- **Cloudflare**: 계획→검토→실행 3단계 분리 (계획 승인 전 코드 작성 불가)

## 연결된 개념

- [[bbw-wiki/wiki/concepts/harness-engineering|하네스 엔지니어링]]
- [[bbw-wiki/wiki/concepts/context-engineering|컨텍스트 엔지니어링]]
- [[bbw-wiki/wiki/concepts/generator-evaluator-pattern|Generator-Evaluator 패턴]]
- [[bbw-wiki/wiki/concepts/claude-md|CLAUDE.md]]
- [[bbw-wiki/wiki/concepts/hooks|훅스]]
- [[bbw-wiki/wiki/concepts/mcp|MCP]]
- [[bbw-wiki/wiki/concepts/context-window|컨텍스트 윈도우]]

## 연결된 엔티티

- [[bbw-wiki/wiki/entities/mitchell-hashimoto|Mitchell Hashimoto]]
- [[bbw-wiki/wiki/entities/ainow|에이나우]]
- [[bbw-wiki/wiki/entities/claude-code|Claude Code]]
- [[bbw-wiki/wiki/entities/anthropic|Anthropic]]

## 메모

- Karpathy의 '컨텍스트 엔지니어링' 언급이 이 흐름의 중간 가교 역할
- MCP보다 CLI가 효과적인 경우 多 — 모델이 이미 CLI를 학습 데이터로 잘 알고 있기 때문 (HumanLayer)
- 비개발자에게도 동일 원리 적용 가능: 콘텐츠 제작·마케팅·교육 등 모든 AI 활용 작업
