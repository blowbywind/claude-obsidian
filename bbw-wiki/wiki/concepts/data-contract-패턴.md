---
title: Data Contract 패턴
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-haeri-learning]]
summary: "데이터 계약으로 프로듀서·컨슈머 간 스키마·SLA를 명시하고 파이프라인 검증으로 데이터 품질을 보장하는 패턴."
---

# Data Contract 패턴

데이터 컨트랙트 패턴의 Obsidian 위키 컨셉 노트 본문입니다:

---

## 핵심 정의

데이터 컨트랙트는 데이터 프로듀서(생산자)와 컨슈머(소비자) 간에 스키마, 시맨틱, SLA(Service Level Agreement)를 명시적 계약으로 문서화하고, 이를 파이프라인 레벨에서 강제하는 패턴입니다.

## 요점

### 1. 계약 기반 설계
스키마 형태, 데이터 의미론, 품질 기준(uptime, latency, freshness)을 명시적으로 정의하여 프로듀서와 컨슈머 간 인터페이스를 명확히 함.

### 2. Shift-Left 검증
PR 파이프라인에 dbt tests, Great Expectations 같은 검증 도구를 직접 삽입하여 컨트랙트 위반을 배포 전에 탐지.

### 3. 실시간 영향도 파악
컨트랙트 위반 시 실시간 알림을 통해 다운스트림 시스템이 받을 영향 범위를 즉시 파악하고 대응.

## 출처

- https://www.acceldata.io/blog/how-data-contracts-guarantee-pipeline-reliability-data-quality-slas
- https://www.mydigicode.com/digipedia/stop-pipeline-fires-data-contracts-observability-lineage-and-testing-the-ops-playbook/

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
