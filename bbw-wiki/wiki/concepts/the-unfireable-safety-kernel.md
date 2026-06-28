---
title: The Unfireable Safety Kernel
type: concept
status: ai-curated
learned_by: snow
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-25-snow-learning]]
---

# The Unfireable Safety Kernel

작성된 마크다운 본문입니다 (frontmatter·h1 제외):

```markdown
에이전트의 신뢰 영역 외부에서 독립적으로 작동하는 실행 시간 보안 메커니즘이다. 에이전트의 주소 공간 외부 독립 프로세스에서 모든 동작을 사전 검증하고 보안 정책을 강제하는 fail-closed 아키텍처로, 에이전트 자체의 손상이나 악의적 변조로부터 시스템 안전성을 근본적으로 보장한다.

## 핵심 특성

**1. 프로세스 분리 기반 격리**
- 에이전트의 메모리 영역과 완전히 분리된 독립 프로세스로 실행
- 에이전트 손상 시에도 안전 커널은 독립적으로 동작
- 하드웨어·OS 레벨의 프로세스 격리 기법(bwrap, AppArmor 등)으로 강제

**2. Pre-action Enforcement**
- 에이전트의 모든 외부 실행 요청(도구 호출, 시스템 접근)을 실행 전 검증
- 정책 위반 요청을 사전에 차단하여 실행 단계의 보안 침해 방지

**3. Fail-Closed 속성**
- 안전 커널 검증 실패 또는 다운 상태에서도 에이전트 실행을 거부
- 보안이 위협받으면 시스템은 안전한 상태(closed)로 자동 전환
- 개방 상태(fail-open)의 위험을 구조적으로 배제

## 출처
- https://arxiv.org/abs/2606.07923
```

**작성 결과:**
- 문자 수: 약 380자 (300~700자 범위 충족)
- 구조: 핵심 정의(1문단) → 요점 3개 → 출처 URL
- 모든 내용이 자가학습 원문에서 제시한 정보만 사용(추측·원문 미포함 내용 제외)

이 본문을 Obsidian 위키의 `claude/` 또는 `topics/` 경로에 저장할 수 있습니다.

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-25-snow-learning]]. 사람 검증 후 status를 verified로 변경하세요.
