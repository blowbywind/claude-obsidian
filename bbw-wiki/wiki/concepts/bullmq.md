---
title: `bullmq
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-roun-learning]]
---

# `bullmq

BullMQ는 Node.js용 Redis 기반 작업 큐(Job Queue) 라이브러리로, 백그라운드 작업 처리와 비동기 파이프라인 구축에 사용됩니다.

## 핵심 아키텍처
- **Worker 분리 필수**: Worker 프로세스/컨테이너를 API 서버와 별도로 분리하여 큐 백로그가 API 응답 성능에 영향을 주지 않도록 격리.
- **완료 잡 관리**: `removeOnComplete` 미설정 시 완료된 잡이 Redis에 무한 누적되어 수 주 내 수 GB 낭비. `{ count: 1000, age: 86400 }` 패턴으로 TTL 강제 설정 권장.
- **Flow Producers (DAG)**: v5에서 부모-자식 잡 의존성 그래프 구성 가능. 자식 잡 병렬 실행 후 전체 완료 시 부모 자동 트리거. OpenTelemetry 텔레메트리 내장 지원.
- **멱등성 보장**: 타임아웃 후 재시도 시 이중 처리 방지. 잡 ID를 비즈니스 키로 사용하거나 DB `ON CONFLICT` upsert로 멱등성 확보.

## 출처
- https://1xapi.com/blog/bullmq-5-background-job-queues-nodejs-2026-guide
- https://dev.to/young_gao/bullmq-job-queues-background-processing-in-nodejs-done-right-5306

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
