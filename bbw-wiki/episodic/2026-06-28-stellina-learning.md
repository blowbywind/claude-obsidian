---
date: 2026-06-28
bot: stellina
type: web-research
tags: [self-learning, CI/CD best practices, container security, observability]
---

# 스텔리나 자가학습 — 2026-06-28

## 오늘 배운 것

- **Cilium Tetragon — eBPF 런타임 강제 차단**: Falco(감지·알림 전용)와 달리 Tetragon은 커널 eBPF 레이어에서 정책 위반 프로세스를 SIGKILL로 즉시 종료. TOCTOU 공격 방어 가능. Falco 보완재로 enforcement 계층 분리 설계 권고. 출처 검증: [tetragon.io](https://tetragon.io) 공식 문서 일치.

- **GitHub Artifact Attestations + slsa-github-generator — SLSA 빌드 증명 자동화**: `actions/attest` 액션과 GitHub OIDC를 결합해 빌드 산출물에 암호화 출처 증명(Provenance)을 자동 첨부. Sigstore Fulcio/Rekor 기반 keyless 서명으로 파이프라인 내 장기 비밀 키 불필요. 기존 `job_workflow_ref` OIDC 항목의 상위 계층에 해당. 출처 검증: [actions/attest](https://github.com/actions/attest), [slsa-github-generator](https://github.com/slsa-framework/slsa-github-generator) 실제 저장소 존재 확인.

- **OTel eBPF Profiler 공식 편입 (Public Alpha)**: Elastic 기증 eBPF 프로파일러가 OpenTelemetry 공식 프로젝트로 편입. 기존 권고 항목(Parca/Pyroscope)과 달리 OTLP 네이티브 출력이므로 OTel Collector와 바로 연동 가능. 코드 수정·재기동 없이 상시 CPU 스택 수집. 출처 검증: [opentelemetry-ebpf-profiler](https://github.com/open-telemetry/opentelemetry-ebpf-profiler) 저장소 실존 확인.

- **Beyla(OBI) vs OTel eBPF Profiler 역할 분리**: Beyla = 코드 수정 없이 트레이스·메트릭 수집(OBI 계층), OTel eBPF Profiler = 상시 CPU 스택 프로파일링(Profiles 계층). 동일 eBPF 기반이지만 관측성 4기둥(Logs·Metrics·Traces·Profiles)에서 역할이 분리됨. 출처 검증: [opentelemetry.io](https://opentelemetry.io) 공식 문서 기술.

- **Argo Rollouts + Gateway API — 점진적 배포 벤더 중립 표준**: HTTPRoute 가중치 동적 조절로 카나리/블루-그린 트래픽 전환. RBAC은 `HTTPRoute` 리소스에 get/list/watch/update/patch만 한정 부여 권고. 현 Docker Compose 환경 직접 적용 불가하나 K8s 전환 시 참조. 출처 검증: [argo-rollouts 공식 문서](https://argo-rollouts.readthedocs.io) 확인.

---

## 출처

- [Cilium Tetragon 공식](https://tetragon.io)
- [actions/attest GitHub](https://github.com/actions/attest)
- [slsa-github-generator](https://github.com/slsa-framework/slsa-github-generator)
- [opentelemetry-ebpf-profiler](https://github.com/open-telemetry/opentelemetry-ebpf-profiler)
- [OpenTelemetry 공식](https://opentelemetry.io)
- [Argo Rollouts 공식 문서](https://argo-rollouts.readthedocs.io)

> 제외 항목: **runwasi(containerd)** — 현 환경에 Wasm 워크로드 없음, 즉시 적용 가치 미달로 제외.

---

## 위키화 후보

- **Tetragon 런타임 강제 차단** — Falco(감지)와 Tetragon(enforcement) 계층 분리 패턴, eBPF SIGKILL 정책 개념 노트
- **SLSA Provenance 자동화 패턴** — Artifact Attestations + slsa-github-generator keyless 서명 파이프라인 구성 노트

---

## 프로필 반영 후보 (저위험)

- **Cilium Tetragon** — 기존 Falco 항목에 "실시간 강제 차단(enforcement) 계층"으로 보완재 추가 (Falco=감지, Tetragon=차단 분리 명시)
- **OTel eBPF Profiler(OTLP 네이티브)** — 기존 "eBPF 연속 프로파일링(Parca/Pyroscope)" 항목을 OTel 공식 편입 사실로 업데이트, Collector 직접 연동 가능 명시

---

## 승인 필요 (고위험)

없음

---

## 신규 도구 후보 (에이전트/스킬)

없음
