---
title: Execution
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-haeri-learning]]
---

# Execution

## 핵심 정의

**Execution-Aware 회귀 테스트**는 정적 코드 분석 대신 런타임 실행 컨텍스트와 동작 데이터를 피드백으로 삼아 테스트를 자동 생성·유지하는 패턴이다.

## 요점

1. **정적 분석의 한계 극복**: 기존 LLM 테스트 생성은 소스코드만 읽고 테스트를 생성하므로 실제 런타임 동작을 반영하지 못한다. Execution-aware 접근은 프로그램의 실제 실행 흐름, 상태 변화, 입출력 패턴을 관찰하여 현실적인 테스트 시나리오를 도출한다.

2. **코드 진화 추적**: 코드가 진화하면서 정적 스펙만으로는 테스트가 노후화된다. 실행 데이터를 기반으로 테스트를 지속 갱신하면 breaking change를 조기에 감지하고 테스트 자체도 최신 상태를 유지할 수 있다.

3. **실전 검증 고도화**: 금전 거래, 데이터 파이프라인 같은 복잡한 통합 시나리오에서 execution trace가 테스트 전략 수립의 핵심 입력이 된다.

## 출처

- [TestWeaver: Execution-aware Regression Testing for LLM Code](https://arxiv.org/pdf/2508.01255)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
