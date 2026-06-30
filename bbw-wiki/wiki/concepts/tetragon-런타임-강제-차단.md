---
title: Tetragon 런타임 강제 차단
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-28
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-28-stellina-learning]]
summary: "Tetragon은 eBPF 기반 런타임 강제 차단 도구로, Falco의 감지를 보완하여 정책 위반 프로세스를 커널 레벨에서 즉시 SIGKILL로 종료합니다."
---

# Tetragon 런타임 강제 차단

## 핵심 정의

**Tetragon**은 Cilium이 제공하는 eBPF 기반 런타임 강제 차단(Enforcement) 도구입니다. Falco가 정책 위반을 감지·알림하는 데 그치는 반면, Tetragon은 커널 레이어에서 위반 프로세스를 `SIGKILL`로 즉시 종료합니다.

## 요점

- **Falco와의 계층 분리**: Falco는 감지/알림 계층(Detection), Tetragon은 강제 차단 계층(Enforcement)으로 역할을 나눕니다. 두 도구를 조합하면 정책 감시와 실시간 차단을 동시에 구현합니다.

- **TOCTOU 공격 방어**: 시간차 취약(Time-of-Check-Time-of-Use)을 커널 eBPF 정책으로 원자적으로 차단하므로 사용자 영역 감지 도구의 지연 유리를 제거합니다.

- **정책 정의 형식**: Tetragon Policy Language(TPL)로 프로세스 실행, 파일 접근, 네트워크 연결 등을 세밀하게 제어 가능합니다.

- **컨테이너·쿠버네티스 통합**: 컨테이너 워크로드 환경에서 Pod 레벨 격리를 보강합니다.

## 출처

- https://tetragon.io

Co-Authored-By: Claude Haiku 4.5 <noreply@anthropic.com>

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-28-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
