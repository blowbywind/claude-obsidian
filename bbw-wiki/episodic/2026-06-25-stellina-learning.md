---
date: 2026-06-25
bot: stellina
type: web-research
tags: [self-learning, CI/CD best practices, container security, observability]
---

# 스텔리나 자가학습 — 2026-06-25

## 오늘 배운 것
- **컨테이너 이미지 지속적 재스캔(Continuous Re-scanning)**: 이미지가 레지스트리에 푸시된 이후에도 백그라운드에서 신규 공개 취약점(CVE)을 지속적으로 재스캔하여 신규 보안 위협을 실시간으로 감지하고 대응함.
- **리눅스 기능(Linux Capabilities)의 명시적 제거(Drop)**: 컨테이너 실행 시 단순히 non-root 계정을 적용하는 것을 넘어, 커널 수준에서 불필요한 리눅스 기능을 명시적으로 drop(`--cap-drop=ALL` 또는 `securityContext.capabilities.drop`)하여 컨테이너 보안을 강화함.
- **클라우드 애플리케이션 탐지 및 대응(CADR)**: eBPF 등을 통해 컨테이너 런타임, 쿠버네티스 제어 평면, 애플리케이션 로그 등 다각도의 런타임 위협 신호를 유기적으로 결합하여 실제 공격 시나리오(Attack Story)를 규명하고 오탐을 줄임.
- **트렁크 기반 개발(Trunk-Based Development)과 피처 플래그 결합**: 장기 생명주기 기능 브랜치로 인한 병목을 방지하기 위해 메인 브랜치에 코드를 자주 통합하되, 미완성 기능은 피처 플래그로 제어하여 배포와 출시를 완전히 분리함.

## 출처
- [Sysdig](https://sysdig.com)
- [ActiveState](https://activestate.com)
- [ARMO](https://www.armosec.io)
- [Valletta Software](https://vallettasoftware.com)

## 위키화 후보
- Cloud Application Detection and Response (CADR) — eBPF 기반의 런타임 행동 분석과 클라우드 자산 컨텍스트를 결합한 통합 탐지/대응 기술.

## 프로필 반영 후보 (저위험)
- Trunk-Based Development — 피처 플래그 및 자동화된 짧은 PR 검토 주기를 활용하여 지속적 통합 속도를 높이는 브랜칭 전략.

## 승인 필요 (고위험)


## 신규 도구 후보 (에이전트/스킬)
