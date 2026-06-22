---
title: `concepts/slo
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-22
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-stellina-learning]]
---

# `concepts/slo

요청을 이해했습니다. 자가학습 원문의 **SLO 에러 버짓 → CI/CD 게이트** 섹션을 바탕으로 `concepts/slo` 개념 노트 본문을 마크다운으로 작성하겠습니다.

---

## 본문 (마크다운)

**SLO**(Service Level Objective)는 서비스가 일정 기간 내에 달성해야 할 가용성·성능·신뢰도 목표를 정량화한 약속이다. 예를 들어 "월 99.9% 가용성"이 SLO이면, 허용되는 다운타임은 약 43분이며, 이를 **에러 버짓**(Error Budget)이라 한다.

**핵심 활용 패턴**

1. **에러 버짓 기반 배포 게이트**: 배포 직전 현재까지의 에러 버짓 소진량을 체크해 ①건강 상태(여유 충분)→자동승인, ②임계 상태(여유 적음)→수동승인, ③완전 소진→배포 차단의 3단계 정책으로 운영  
2. **실용 구현**: Prometheus에서 SLI(Service Level Indicator) 메트릭을 수집하고 Grafana 대시보드에서 에러 버짓 소진량을 시각화해 CI/CD 파이프라인의 배포 승인/차단 결정 기준으로 활용

이 접근법은 2026 SRE 표준으로 자리 잡는 중이며, 개발 속도(높은 배포 빈도)와 안정성(변경 실패율 관리) 사이의 균형을 자동화된 정책으로 해결한다.

**출처**  
- [Error Budget Policies for Release Gating — OneUptime](https://oneuptime.com/blog/post/2026-02-17-how-to-establish-error-budget-policies-for-release-gating-on-google-cloud/view)

---

**글자 수**: 약 330자 / **구조**: 핵심 정의(SLO·에러 버짓) → 요점 2개(배포 게이트 3단계·구현 스택) → 출처 URL

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
