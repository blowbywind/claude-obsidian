---
date: 2026-06-27
bot: stellina
type: web-research
tags: [self-learning, CI/CD best practices, container security, observability]
---

# 스텔리나 자가학습 — 2026-06-27

기존 위키(concepts-container, otel, falco, supply, observability) 내용 확인 완료. WebSearch 권한이 없어 출처 URL 도메인 신뢰도 기준으로 교차검증 진행.

---

## 검증 판정

| 항목 | 출처 | 판정 |
|---|---|---|
| OTel Semantic Conventions | opentelemetry.io | ✅ 권위 소스, 기존 위키 미수록 |
| Workload Identity + ESO | medium.com (ESO=CNCF 공식 프로젝트) | ✅ 개념 CNCF로 검증 가능 |
| 포렌식 스냅샷 보존 | orca.security (concepts-container.md 기존 수록) | ✅ 신규 각도 |
| 관측성 기반 카나리 게이트 | requirementguide.com | ⚠️ 저권위 소스, 개념은 Flagger/Argo 공식 기능으로 유효 |
| Policy-as-Code Admission Controller | jeeviacademy.com | ⚠️ 저권위, 개념 유효(기존 Falco 위키 2단계와 일치) |
| "CADR" | armosec.io | ❌ 벤더 마케팅 용어, Gartner 공식 범주는 CDR — 폐기 |
| "OBI(Non-intrusive Context Propagation)" | opentelemetry.io 인용이나 표준 용어 미확인 | ❌ 리서치 합성 약어 — 폐기 |
| Golden Path | requirementguide.com 단독 | ❌ 저권위 단독 출처 — 폐기 |

---

## 오늘 배운 것

- **OTel Semantic Conventions 표준화** — `service.name`·`k8s.pod.name`·`container.id` 등 리소스 속성 명명 규칙 통일 시 logs·metrics·traces 간 cross-signal 연관 분석 가능. OTel Collector `resource` processor로 속성 주입·오버라이드. (opentelemetry.io)
- **Workload Identity + ESO Secretless GitOps** — CI에서 시크릿 직접 주입 대신 파드 OIDC 단기 토큰→Secrets Manager 런타임 수령 패턴. External Secrets Operator(CNCF)가 K8s Secret 객체 자동 동기화. 기존 GitHub Actions OIDC(2026-06-26 프로필)와 결합해 파이프라인 전 구간 시크릿리스 가능.
- **포렌식 스냅샷 자동 보존** — Falco 경보 발화 시 에페메럴 컨테이너 소멸 전 로그·프로세스 목록·네트워크 상태 즉시 저장. Falcosidekick 웹훅 파이프라인에 저장 훅 추가로 Docker Compose 환경에서도 구현 가능. (orca.security)
- **관측성 기반 배포 게이트(구체 구현)** — Argo Rollouts / Flagger 카나리 승격 기준을 시간 대신 Prometheus 에러율·레이턴시 임계값으로 설정. 기존 에러 버짓 게이트(2026-06-21)와 동일 방향, GitHub Actions 배포 스텝에서 Prometheus API 쿼리로 K8s 없이도 구현 가능.
- **Policy-as-Code (OPA/Gatekeeper · Kyverno)** — K8s Admission Controller 단에서 비규격 이미지 진입 차단. 기존 Falco 3단 방어(정적 스캔→입장 제어→런타임)의 2단계를 구체화하는 도구. 현재 Docker Compose 환경에선 선적용 불가, K8s 전환 시 체크리스트 항목.

## 출처

- [OpenTelemetry Semantic Conventions](https://opentelemetry.io/docs/specs/semconv/)
- [Orca Security — Container Security Best Practices](https://orca.security/resources/blog/container-security-best-practices/)
- [External Secrets Operator (CNCF)](https://external-secrets.io)

## 위키화 후보

- `concepts/otel-semantic-conventions` — 리소스 속성 표준화로 cross-signal 연관 분석 활성화하는 OTel 규격 (현 otel 위키에 미수록)
- `concepts/secretless-gitops` — Workload Identity + ESO 결합 패턴, 파이프라인 시크릿 완전 제거

## 프로필 반영 후보 (저위험)

- OTel Semantic Conventions(`service.name`/`k8s.pod.name`/`container.id`) — OTel Collector 설정 권고 패턴에 리소스 속성 표준화 항목 추가
- ESO + Workload Identity Secretless 패턴 — 시크릿 관리 권고 항목에 추가 (기존 GitHub OIDC 항목 확장)

## 승인 필요 (고위험)

없음

## 신규 도구 후보 (에이전트/스킬)

없음
