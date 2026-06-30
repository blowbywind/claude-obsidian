---
date: 2026-06-30
bot: stellina
type: web-research
tags: [self-learning, CI/CD best practices, container security, observability]
---

# 스텔리나 자가학습 — 2026-06-30

기존 위키 파악 완료. progressive-delivery는 draft 단계, CNAPP·AI Observability·Hadolint는 미기록. 출처 교차검증 결과:

- **버림**: gravitydevops.com(Agentic CI/CD) — 미검증 블로그, 권위 없음. railway.com(Platform-native CI/CD) — 벤더 마케팅.
- **주의**: tblocks.com("Bounded Failures" 용어) — 불명 출처. 개념 자체(blast radius)는 표준 SRE 용어로 검증, 해당 사이트 신뢰도 낮아 출처 미채택.
- **채택**: armosec.io(CNAPP — Gartner 카테고리, ARMO=Kubescape 제작사), ox.security(AI 인프라 코드 검증), ibm.com(AI 관찰성), elastic.co(OTel 비용 필터링).

---

## 오늘 배운 것

- **CNAPP(Cloud-Native Application Protection Platform) 통합 관점**: IAM·네트워크·컨테이너 런타임 보안 데이터를 단일 플랫폼에서 연계 분석하는 Gartner 정의 카테고리. 현재 Trivy(정적) + Falco(런타임) + Kubescape(reachability) 3단 체계를 CNAPP 논리 레이어로 설명할 수 있다.
- **AI 생성 인프라 코드 검증 필요성**: AI 도구가 출력한 Dockerfile·K8s 매니페스트가 전통 리뷰를 건너뛰고 적용되는 공급망 리스크 대두. CI 게이트에 Hadolint(Dockerfile 린트) + Trivy 스캔을 AI 생성 파일 전용 스텝으로 강제하는 것이 권고 방향.
- **blast radius 최소화 (점진적 배포 연계)**: 카나리·링 배포 + 실시간 메트릭 연계로 장애의 시간·공간 영향 범위를 제한하는 표준 SRE 패턴. 기존 에러 버짓 게이트 제안(2026-06-21)과 직접 결합 가능 — 버짓 소진 시 카나리 단계에서 자동 차단.
- **AI 에이전트 관찰성(AI Observability)**: 다수 AI 에이전트 협업 흐름에서 신뢰성 문제 추적을 위해 에이전트 간 호출을 OTel 스팬으로 포함시키는 계측 패턴. autobots 봇 협업 흐름(handoff·delegation 체인)에 직접 적용 가능.
- **OTel 수집 비용 필터링**: 텔레메트리 데이터 폭증에 따른 비용 제어를 위해 OTel Collector 단에서 샘플링·drop 필터를 강화하는 FinOps 지향 체계. 기존 tail-based sampling 권고(2026-06-24)를 비용 기준으로 구체화하는 후속 단계.

## 출처

- [ARMO Security — CNAPP & Kubescape](https://www.armosec.io)
- [OX Security — AI-generated code supply chain risk](https://www.ox.security)
- [IBM — Observability for AI agents](https://www.ibm.com)
- [Elastic — Observability cost & data volume control](https://www.elastic.co)

## 위키화 후보

- `concepts/cnapp.md` — Trivy·Falco·Kubescape 3단 체계를 CNAPP 관점으로 통합 정리 (기존 포인트 툴 노트 연결)
- `concepts/ai-observability.md` — AI 에이전트 간 호출을 OTel 스팬으로 계측하는 패턴 (autobots 적용 맥락)

## 프로필 반영 후보 (저위험)

- **Hadolint + Trivy AI 생성 인프라 코드 검증 스텝** — CI 보안 체크리스트에 "AI 도구 출력 Dockerfile은 Hadolint+Trivy 게이트 필수" 항목 추가
- **blast radius 최소화 + 에러 버짓 게이트 연계** — 배포 전략 권고 항목에 "카나리 + 버짓 소진 자동 차단" 패턴 추가

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보

- `[skill] ai-infra-lint` — AI 생성 Dockerfile·Compose 파일 대상 Hadolint + Trivy 자동 게이트 실행 스킬 (CI 파이프라인 연동 반복 작업)
