---
title: Vercel AI SDK 5
type: concept
status: ai-curated
learned_by: lian
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-lian-learning]]
summary: "Vercel AI SDK 5는 메시지 분리와 에이전트 루프 제어로 풀스택 AI 앱 개발을 표준화한 SDK이다."
---

# Vercel AI SDK 5

## 핵심 정의

Vercel AI SDK 5는 풀스택 AI 애플리케이션 개발을 위한 표준 SDK로, 2025년 7월 31일 출시되었다. UI 계층과 모델 계층의 메시지 처리를 명확히 분리하고, 에이전트 루프 제어 기능을 강화한 아키텍처를 제공한다.

## 주요 특징

**메시지 분리 아키텍처**  
`UIMessage`와 `ModelMessage`를 구분하여 클라이언트 상호작용과 LLM 통신을 독립적으로 관리한다. 이를 통해 UI 상태 관리와 모델 호출 로직의 결합도를 낮춘다.

**에이전트 루프 제어**  
`stopWhen`, `prepareStep` 등 명시적 제어 메커니즘을 도입해 에이전트의 실행 흐름을 세밀하게 조정할 수 있다. 에이전트 기반 애플리케이션 개발에서 필요한 체크포인트와 중단 조건을 선언적으로 정의한다.

**SSE 스트리밍**  
WebSocket 대신 Server-Sent Events 기반 스트리밍을 표준으로 채택해 실시간 응답 처리의 안정성과 호환성을 개선했다.

**경량 Agent 클래스**  
복잡한 에이전트 프레임워크에 의존하지 않고도 경량의 `Agent` 클래스로 기본 에이전트 패턴을 구현할 수 있다.

## 출처
- https://vercel.com/blog/ai-sdk-5

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-lian-learning]]. 사람 검증 후 status를 verified로 변경하세요.
