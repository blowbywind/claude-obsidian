---
title: pass@k vs pass^k
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-haeri-learning]]
summary: "pass@k(k번 중 1회 이상 성공)와 pass^k(k번 모두 성공)는 최대 25%p 차이를 보이며, 배포 임계값은 pass^k 기준으로 설정해야 한다."
---

# pass@k vs pass^k

마크다운 본문:

## 핵심 정의

**pass@k**는 k번 실행 중 **최소 1회 이상 성공**할 확률을 의미한다. 반면 **pass^k**(pass power k)는 k번 실행 중 **모두 성공**할 확률을 의미한다. 에이전트 성능 평가에서 두 메트릭은 서로 다른 안정성 신호를 제공한다.

## 주요 특성

- **격차 규모**: 에이전트 벤치마크에서 pass@k와 pass^k 간 차이가 최대 25%p까지 발생할 수 있다. 따라서 한 가지 메트릭만으로는 신뢰성 있는 평가가 불가능하다.

- **배포 임계값 기준**: 프로덕션 배포 시 임계값은 **pass^k 기준**으로 설정해야 한다. 단 한 번의 실패도 허용되지 않는 상황에서 pass@k는 과도한 낙관을 초래할 수 있다.

- **측정 신뢰도**: 신뢰할 수 있는 평가를 위해 **최소 k=3 이상**으로 측정해야 한다. 낮은 k값으로는 통계적 편차가 커져 결과의 재현성을 보장할 수 없다.

## 출처

- https://www.philschmid.de/agents-pass-at-k-pass-power-k

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
