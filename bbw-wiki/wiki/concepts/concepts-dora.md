---
title: `concepts/dora
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-22
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-stellina-learning]]
---

# `concepts/dora

## 개념 노트: DORA 메트릭

**DORA(DevOps Research and Assessment)** 메트릭은 소프트웨어 팀의 배포 효율성과 안정성을 측정하는 4가지 핵심 지표다. 배포 빈도(Deployment Frequency), 리드타임(Lead Time for Changes), 변경 실패율(Change Failure Rate), 복구 시간(Mean Time to Recovery)으로 구성된다.

### 요점

1. **2026 AI 도입 역설** — AI 코딩 도구는 개인 생산성(배포 빈도·리드타임)은 개선하지만, 팀 안정성(변경 실패율·복구 시간)은 오히려 악화시키는 경향이 보고되고 있다. Goodhart's Law("지표가 목표가 되면 지표의 신뢰성이 떨어진다")가 적용되는 사례로, **변경 실패율 집중 모니터링**이 2025 DORA 보고서의 권고사항이다.

2. **DX Core 4 보완 필요** — DORA 4지표만으로는 개발자 경험(Developer Experience)을 완전히 포괄하지 못하므로, 코드 유지보수성·테스트 커버리지·배포 신뢰성 등을 추가 측정하는 DX Core 4 프레임워크와 병행이 필수다.

3. **5번째 지표: Deployment Rework Rate** — 2024년 신규 추가. 롤백이나 긴급 핫픽스가 필요한 배포의 비율을 측정하며, 변경 실패율의 한계를 보완한다.

### 출처
- https://www.gitrecap.com/blog/dora-metrics-benchmarks
- https://getdx.com/blog/dora-metrics-tools/
- https://www.faros.ai/blog/5th-dora-metric-rework-rate-track-it-now

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
