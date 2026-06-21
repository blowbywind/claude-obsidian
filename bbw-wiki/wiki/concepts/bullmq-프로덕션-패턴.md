---
title: BullMQ 프로덕션 패턴
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-roun-learning]]
---

# BullMQ 프로덕션 패턴

## 핵심 정의

BullMQ 프로덕션 패턴은 Redis 기반 작업 큐를 프로덕션 환경에서 안정적으로 운영하기 위한 아키텍처 및 설정 원칙이다.

## 요점

### 1. Worker 분리 원칙
Worker를 API 서버와 **별도 프로세스/컨테이너**로 분리하여 큐 백로그가 API 응답에 영향을 주지 않도록 설계. 동일 프로세스 내 실행 시 장기 작업이 이벤트루프를 블로킹한다.

### 2. removeOnComplete 필수 설정
`removeOnComplete: true` 미설정 시 완료된 잡이 Redis에 무한 누적된다. 일 10K 잡 기준 수 주 내 GB 단위 메모리 낭비 발생. `{ count: 1000, age: 86400 }` 패턴으로 개수/TTL 기반 정리 필수.

### 3. Flow Producers로 DAG 잡 구성
부모-자식 잡 의존성 그래프로 멀티스텝 파이프라인(파일 업로드 → 변환 → 알림) 구현 가능. 자식 잡 병렬 실행 후 전체 완료 시 부모 자동 트리거. OpenTelemetry 텔레메트리 내장 지원.

### 4. 멱등성 보장
잡이 타임아웃 후 재시도될 때 이중 처리(이메일 2회 발송, 중복 결제) 방지 필수. 잡 ID를 비즈니스 키로 사용하거나 DB `ON CONFLICT` upsert로 멱등성 확보.

## 출처
- [BullMQ 5 Background Jobs in Node.js (2026 Guide)](https://1xapi.com/blog/bullmq-5-background-job-queues-nodejs-2026-guide)
- [BullMQ Job Queues in Node.js: Background Processing Done Right](https://dev.to/young_gao/bullmq-job-queues-background-processing-in-nodejs-done-right-5306)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
