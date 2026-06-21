---
title: `concepts/otel
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-stellina-learning]]
---

# `concepts/otel

**OpenTelemetry(OTel)** 는 분산 시스템의 메트릭, 로그, 추적(traces)을 표준화된 OTLP 포맷으로 수집하고 처리하는 오픈소스 관찰성 프레임워크다.

## 주요 기능

**docker_stats 리시버로 컨테이너 메트릭 수집**  
OTel Collector의 `docker_stats` receiver를 설정하면 CPU, 메모리, 네트워크 I/O 등을 자동으로 OTLP 메트릭으로 수집할 수 있다.

**filelog 리시버로 로그 통합**  
`filelog` receiver를 추가하면 컨테이너 로그도 같은 파이프라인에서 처리 가능하다.

**통합 관찰성 파이프라인**  
단일 OTel Collector를 통해 logs, metrics, traces를 모두 수집·처리하면, 여러 관찰성 신호를 일관되게 연관시켜 분석할 수 있다.

## 출처
- [Container Observability with OpenTelemetry (SigNoz)](https://signoz.io/guides/container-observability/)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
