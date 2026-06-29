---
title: Cloud Application Detection and Response (CADR)
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-25-stellina-learning]]
summary: "eBPF 기술로 컨테이너 런타임, 쿠버네티스 제어평면, 애플리케이션 로그에서 위협신호를 통합 수집하여 단편적 알림이 아닌 실제 공격 흐름을 재구성하고 오탐을 감소시키는 클라우드 보안 기술"
---

# Cloud Application Detection and Response (CADR)

Obsidian 위키 노트를 작성하겠습니다. 자가학습 원문 기반으로 마크다운 본문만(frontmatter·h1 제외) 300~700자 범위로 작성합니다.

---

## 핵심 정의
eBPF 등의 기술을 활용하여 컨테이너 런타임, 쿠버네티스 제어 평면, 애플리케이션 로그 등 다각도의 런타임 위협 신호를 수집하고 유기적으로 결합하여 실제 공격 시나리오(Attack Story)를 규명하는 클라우드 보안 기술.

## 핵심 특징

**런타임 위협 신호의 통합 수집**
- 컨테이너 런타임 동작, 쿠버네티스 제어 평면 이벤트, 애플리케이션 로그를 동시에 모니터링하여 보안 위협을 다각도에서 포착

**Attack Story 규명**
- 단편적인 보안 알림이 아닌 실제 공격 흐름(Attack Story)을 시간 순서대로 재구성하여 진정한 위협을 식별

**오탐 감소**
- 다각도 데이터 결합을 통해 무의미한 보안 경고(False Positive)를 줄이고 실제 위험에 집중

## 출처
- https://sysdig.com
- https://www.armosec.io
- https://activestate.com
- https://vallettasoftware.com

---

**문자 수**: 약 350자 (규범 300~700자 범위 내)

이 노트는 자가학습 원문의 CADR 설명을 그대로 구조화했으며, 출처 URLs는 원문의 출처 네 곳을 모두 보존했습니다.

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-25-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
