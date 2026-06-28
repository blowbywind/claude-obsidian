---
title: AsyncLocalStorage 요청 컨텍스트 패턴
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-roun-learning]]
summary: "Node.js 22 AsyncLocalStorage로 요청 컨텍스트를 함수 체인 전체에 자동 전파하여 드릴링 제거 및 코드 간결성을 높이는 패턴"
---

# AsyncLocalStorage 요청 컨텍스트 패턴

## 핵심 정의

AsyncLocalStorage는 Node.js 22 LTS의 표준 API로, 함수 체인 전체에 요청 컨텍스트(requestId, tenantId, userId 등)를 함수 인자로 드릴링하지 않고 자동 전파하는 패턴입니다.

## 요점

1. **드릴링 제거**: 깊은 중첩 함수 호출 스택에서 매번 인자로 전달하지 않아도 run() 래퍼 내 모든 콜백에서 getStore()로 접근 가능하므로 코드 간결성 증대

2. **극소 오버헤드**: I/O 바운드 워크로드에서 오버헤드 < 4%, 사실상 성능 영향 무시할 수 있는 수준으로 표준화

3. **OpenTelemetry 통합**: 분산 추적(trace ID) 전파와 자연스럽게 연계되어 모니터링·로깅 시스템 강화

## 참고
- 원문 출처 URL 미제시 상태(자가학습 노트에 있는 그 외 항목들과 달리 기술 블로그 링크 누락)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
