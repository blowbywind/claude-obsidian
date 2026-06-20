---
title: REST API Naming & Versioning Standards
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-18-dex-learning]]
---

# REST API Naming & Versioning Standards

## 핵심 정의

REST API의 명명 규칙과 버전 관리 전략은 API 사용성, 캐싱 효율, 후위 호환성을 결정하는 설계 기본이다. 명확한 명칭(명사 기반 리소스 표현)과 체계적 버전 관리는 클라이언트 개발 효율을 높이고, LLM/MCP 통합 시 도구 선택 정확도를 향상시킨다.

## 명명 규칙(Naming)의 4가지 표준

- **동사 제거 + 명사 기반**: `/createCustomer` (❌) → `/customers` (✓), 메서드는 HTTP 동사로만 표현
- **복수형 고정 + 소문자-하이픈**: `/order-items` (일관성), 리소스명 하이픈 구분, `/OrderItems` (❌)
- **중첩 1단계 제한**: `/customers/{id}/orders` (✓), `/customers/{id}/orders/{orderId}/items` (❌) — 가독성·캐싱 저하

## 버전 관리의 4가지 전략과 실무 선택

| 전략 | 방식 | 특징 |
|------|------|------|
| **URL 경로** | `/v1`, `/v2` | 가장 보편적, 엣지 캐싱 효율 최고 |
| **헤더** | `Accept-Version: 2.0` | 코드 변경 없이 유연한 전환 |
| **쿼리 파라미터** | `?version=2` | 명시적이나 캐싱 복잡도 증가 |
| **날짜 기반** | `YYYY-MM-DD` (GitHub 사용) | API 진화 추적 용이, 24개월 지원 정책 |

## 후위 호환성 우선 원칙

버전 전략 선택보다 **기존 클라이언트 호환성 엄격 유지**가 핵심. Netflix 사례: 버전 관련 배포 오류 42% 감소, OpenAPI 문서 정확도 유지 필수.

## 출처

- [REST API URI Naming Conventions and Best Practices](https://restfulapi.net/resource-naming/)
- [Web API Design Best Practices - Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design)
- [API Versioning Strategies: 2026 Engineering Matrix](https://www.digitalapplied.com/blog/api-versioning-strategies-2026-engineering-decision-matrix)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-18-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
