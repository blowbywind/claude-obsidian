---
date: 2026-06-24
bot: stellina
type: web-research
tags: [self-learning, CI/CD best practices, container security, observability]
---

# 스텔리나 자가학습 — 2026-06-24

WebSearch 권한이 없어 직접 검색 불가 → 훈련 데이터 기반 교차검증으로 대체한다. 이미 확인된 위키 항목 및 소스 신뢰도를 기준으로 정리한다.

---

**교차검증 결과 (소스별)**

| 항목 | 소스 | 판정 |
|------|------|------|
| 런타임 도달 가능성 분석 | armosec.io (Kubescape 제작사 ARMO) | ✅ CNCF 프로젝트, Kubescape v3+ 실제 기능 |
| Observability as Code | ibm.com | ✅ IBM 기술 블로그 실존, GitOps 확장 개념 검증됨 |
| Observability Tax | motadata.com | ✅ 벤더 사이트지만 개념 자체는 업계 공인 |
| Progressive Delivery 배포↔출시 분리 | capgo.app | ⚠️ Capacitor OTA 도구 사이트 — 개념은 Martin Fowler/LaunchDarkly로 검증되나 출처 권위 낮음, 개념만 채택 |
| Internal Developer Platform | tblocks.com | ❌ 비권위 소스, 기존 platform engineering 재포장 수준 — 폐기 |
| Predictive CI/CD | medium.com | ❌ 비권위 소스, 내용 모호 — 폐기 |
| Agentic AI Monitoring | montecarlo.ai | ⚠️ 자사 제품 마케팅 성격, DevOps 인프라 역할 직접 관련도 낮음 — 폐기 |

**기존 위키 중복 확인**: Falco(`concepts-falco.md`) · OTel(`concepts-otel.md`) 이미 수록. Progressive delivery는 stub만 존재(`concepts-progressive.md` — 내용 미완).

---

## 오늘 배운 것

- **런타임 도달 가능성 분석(Runtime Reachability Analysis)**: Kubescape(ARMO)가 제공하는 기능으로, 수천 개의 정적 CVE 중 실제로 실행 시 메모리에 적재되는 코드 경로에 해당하는 취약점만 필터링한다. Trivy 정적 스캔 결과의 노이즈를 대폭 줄여 HIGH/CRITICAL 게이트의 실효성을 높인다.
- **Observability as Code**: Grafana 대시보드 JSON, Prometheus 알림 규칙 YAML, OTel Collector 설정을 Git으로 버전 관리하고 CI/CD 파이프라인으로 배포하는 방식. 대시보드 드리프트 방지 및 환경 간 일관성 확보에 효과적이다.
- **Observability Tax 최적화**: 분산 트레이싱·로그 전량 수집 시 스토리지·전송 비용이 급증하는 현상. 헤드 기반 샘플링(head-based sampling) 대신 꼬리 기반 샘플링(tail-based sampling)으로 오류·느린 요청만 전량 보존하고 정상 트래픽은 저율 샘플링하면 비용 절감과 장애 가시성을 동시에 확보한다.
- **Progressive Delivery — 배포↔출시 분리**: 컨테이너 배포(deploy)와 기능 활성화(release)를 피처 플래그로 분리. 코드를 먼저 프로덕션에 올리고 트래픽은 플래그 토글로 점진 전환해 롤백 비용을 최소화한다. 단일 서버 Caddy+Compose 환경에서는 Unleash(셀프호스트) 또는 환경 변수 플래그로 구현 가능.

## 출처

- [Kubescape Runtime Reachability — ARMO](https://www.armosec.io)
- [Observability as Code — IBM](https://www.ibm.com)
- [Observability Tax & Smart Sampling — Motadata](https://www.motadata.com)
- Progressive Delivery 배포↔출시 분리 — [Martin Fowler, Feature Toggles](https://martinfowler.com/articles/feature-toggles.html) (권위 출처로 대체)

## 위키화 후보

- `concepts/runtime-reachability.md` — Kubescape 런타임 도달 가능성 분석: Trivy 정적 스캔 보완, CVE 노이즈 필터링 메커니즘
- `concepts/observability-as-code.md` — 대시보드·알림·Collector 설정 GitOps화, 기존 `concepts-otel.md`와 연결

## 프로필 반영 후보 (저위험)

- Kubescape Runtime Reachability를 인프라 보안 체크리스트에 추가 — Trivy(정적) + Kubescape(런타임 필터) 2단 스캔 권고 용어로 등록
- tail-based sampling을 OTel Collector 설정 권고 패턴에 추가

## 승인 필요 (고위험)

_(없음)_

## 신규 도구 후보 (에이전트/스킬)

_(없음 — 기존 Trivy·Falco·OTel 체계 내 확장으로 충분)_
