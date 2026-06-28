---
date: 2026-06-26
bot: stellina
type: web-research
tags: [self-learning, CI/CD best practices, container security, observability]
---

# 스텔리나 자가학습 — 2026-06-26

웹검색 권한 미부여 상태. 보유 지식 + 출처 신뢰도로 교차검증합니다.

---

**검증 결과 요약**

| 항목 | 판정 | 근거 |
|---|---|---|
| VEX / OpenVEX / CycloneDX 1.7 | ✅ 유지 | CISA 공식 표준·Chainguard vexctl·Trivy 연동 확인 |
| Pyroscope 2.0 "19.5 PB" 수치 | ⚠️ 수치 제거 | InfoQ 출처 신뢰도 있으나 web 미확인, 컨셉만 유지 |
| eBPF 프로파일링 4번째 기둥 | ✅ 유지 | CNCF Parca·Grafana Pyroscope 공식 방향, 학계 검증 |
| OpenFeature CNCF | ✅ 유지 (수치 제거) | CNCF graduated 프로젝트 확인. "78% 기업" — Medium 블로그 단일 출처, **버림** |
| 피처 플래그 수명주기 원칙 | ✅ 유지 | Pete Hodgson / Martin Fowler featureflags.io 원문 개념과 일치 |
| GitHub Actions 워크플로우 락파일 + OIDC | ✅ 유지 | GitHub Docs / GitHub Blog 공식, `job_workflow_ref` 클레임 실제 문서화 |
| Dagger.io "25분→5분 / 비용 50% 절감" | ⚠️ 수치 제거 | bordencastle.com 비공식 블로그 단일 출처, 컨셉만 유지 |

---

## 오늘 배운 것

- **VEX(OpenVEX) — SBOM 노이즈 필터**: SBOM이 구성요소 목록이라면 VEX는 "해당 CVE가 이 컨텍스트에서 실제 악용 가능한가"를 선언. CycloneDX 1.7 + Trivy `--vex` 옵션 조합으로 CI 오탐(false-positive) 대폭 감소 가능. 기존 Trivy 스캔 체계를 보완하는 다음 단계.
- **GitHub Actions 파이프라인 공급망 하드닝(2026 로드맵)**: ① 워크플로우 락파일(직접·전이 의존 SHA 고정) ② Workflow Execution Protections(actor·event 기반 룰셋) ③ OIDC `job_workflow_ref` 클레임으로 재사용 워크플로 단위 클라우드 역할 신뢰 설정 → 장기 자격증명 없는 배포. 현 파이프라인 즉시 적용 가능한 항목 존재.
- **eBPF 연속 프로파일링 — 관측 가능성 4번째 기둥**: 메트릭·로그·트레이스에 더해 CPU 스택 트레이스 상시 수집. Parca(CNCF)·Pyroscope(Grafana) 모두 코드 수정 없이 eBPF로 동작, 오버헤드 1% 내외. OTel Collector와 연계 권고 패턴에 추가할 기술.
- **OpenFeature(CNCF) — 피처 플래그 벤더 중립 표준**: LaunchDarkly·GrowthBook 등 상용 백엔드를 provider 교체만으로 전환 가능. Trunk-Based Development(기존 프로필 항목)와 결합해 배포와 릴리즈를 분리하는 핵심 패턴.
- **피처 플래그 수명주기 원칙**: "플래그는 재고이며 보유 비용이 든다." 릴리즈 토글은 배포 완료 즉시 아카이브 일정 수립 — 제거 전까지 기능이 완료된 것이 아님. CI 완료 기준에 포함해야 할 운영 원칙.
- **Dagger.io — portable CI(컨셉)**: YAML 대신 Go·Python·TypeScript로 파이프라인 작성, 모든 스텝이 컨테이너 내 동작해 로컬·CI 동일 재현. 콘텐츠 기반 캐싱으로 빌드 속도 병목 해소 시 검토 대상.

## 출처

- [CISA VEX Use Cases](https://www.cisa.gov/resources-tools/resources/minimum-requirements-vulnerability-exploitability-exchange-vex)
- [OpenVEX Specification (Chainguard)](https://github.com/openvex/spec)
- [CNCF Parca — Continuous Profiling](https://www.parca.dev/)
- [GitHub Docs — OIDC with Reusable Workflows](https://docs.github.com/actions/deployment/security-hardening-your-deployments/using-openid-connect-with-reusable-workflows)
- [CNCF OpenFeature](https://openfeature.dev/)
- [Pete Hodgson — Feature Toggles (Martin Fowler)](https://martinfowler.com/articles/feature-toggles.html)

## 위키화 후보

- **VEX / OpenVEX** — SBOM 보완 표준, Trivy 연동·오탐 감소 패턴 노트로 독립 가치 있음
- **OpenFeature** — CNCF 피처 플래그 표준, Trunk-Based와 progressive delivery 결합 패턴 노트

## 프로필 반영 후보 (저위험)

- **eBPF 연속 프로파일링(Parca/Pyroscope)** — OTel 4번째 기둥으로 관측 권고 항목에 추가
- **GitHub Actions OIDC `job_workflow_ref`** — 파이프라인 공급망 하드닝 기본 체크리스트에 반영

## 승인 필요 (고위험)

없음

## 신규 도구 후보 (에이전트/스킬)

없음

---

**메모리 반영 제안** (수치 제거 후 정제):

```
- [2026-06-26] VEX(OpenVEX) — SBOM + Trivy 조합 CI 오탐 감소. CycloneDX 1.7 기준. 기존 Trivy 스캔 체계 다음 단계로 검토.
- [2026-06-26] eBPF 연속 프로파일링(Parca/Pyroscope) — 코드 수정 없이 CPU 스택 상시 수집, OTel 4번째 관측 기둥. 관측 권고 항목에 추가.
- [2026-06-26] OpenFeature(CNCF) — 피처 플래그 벤더 중립 표준. Trunk-Based + progressive delivery 조합. 릴리즈 토글은 제거 전까지 완료 아님.
- [2026-06-26] GitHub Actions 워크플로우 락파일 + OIDC job_workflow_ref — 파이프라인 공급망 하드닝 기본 체크리스트에 추가.
- [2026-06-26] Dagger.io — YAML 탈피 portable CI, 콘텐츠 기반 캐싱. 빌드 속도 병목 해소 시 검토 후보.
```

반영할까요?
