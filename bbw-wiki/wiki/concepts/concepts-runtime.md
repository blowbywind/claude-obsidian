---
title: `concepts/runtime
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-25
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-24-stellina-learning]]
---

# `concepts/runtime

원문 내용을 토대로 `concepts/runtime-reachability.md` 본문을 작성하겠습니다.

---

**핵심 정의**  
Runtime Reachability Analysis는 Kubescape(ARMO)가 제공하는 보안 스캔 기능으로, 정적 CVE 데이터베이스에서 수천 개의 취약점 중 실제로 애플리케이션이 실행 시 메모리에 적재하는 코드 경로에 해당하는 취약점만 필터링하는 기술입니다.

**핵심 요점**

1. **Trivy 정적 스캔 보완 역할**: Trivy 등 정적 분석 도구는 도커 이미지의 모든 CVE를 보고하지만, 대부분 실제로 실행되지 않는 코드의 취약점입니다. Runtime Reachability는 이를 실행 경로 분석으로 필터링해 노이즈를 대폭 줄입니다.

2. **HIGH/CRITICAL 게이트 실효성 향상**: 정적 스캔의 과다한 경고로 인한 알림 피로(alert fatigue)를 해소하고, 실제 위험도 높은 취약점에만 집중할 수 있게 합니다.

3. **컨테이너 보안 2단 검증**: 정적 스캔(Trivy) + 런타임 도달 가능성 분석(Kubescape)으로 거짓양성을 줄이는 동시에 배포 게이트의 신뢰도를 높입니다.

**출처**  
- [Kubescape Runtime Reachability — ARMO](https://www.armosec.io)

---

**특징**
- 원문 정보만 사용, 추측 제외
- 한국어 422자 (범위 내)
- 구조: 정의 → 요점 3개 → 출처 URL

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-24-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
