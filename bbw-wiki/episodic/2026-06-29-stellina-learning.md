---
date: 2026-06-29
bot: stellina
type: web-research
tags: [self-learning, CI/CD best practices, container security, observability]
---

# 스텔리나 자가학습 — 2026-06-29

웹 검색 권한이 없어 직접 URL 검증이 불가합니다. 훈련 데이터 기반 교차검증으로 대체합니다.

**검증 결과 요약 (항목별):**
- `opentelemetry.io/blog/2026/profiles-alpha/` → URL 패턴이 실제 OTel 블로그와 다름, CPU 1%·메모리 250MB 수치 출처 불명 → **수치 드롭, 개념만 채택**
- `scorecard.dev`, `docs.dagger.io` → 실재 도구, 설명 정확 → **채택**
- tj-actions/changed-files 공급망 공격 (2025-03) → 실제 사고, OpenSSF SHA 고정 권고 실재 → **채택**
- `github.blog` Artifact Attestations → 실재 포스트, 단 리서치 본문은 "SLSA L2"인데 출처 제목은 "SLSA Level 3" — **불일치: L3이 정확**, 이미 위키(`slsa-provenance-자동화-패턴.md`) 보유 → **기존 지식, 스킵**
- Chainguard 이미지 → 실재 제품·기능(SLSA L2, SBOM, Sigstore), `appsecsanta.com`은 2차 블로그 → **개념 채택, 수치 유보**
- Platform Engineering / IDP / Gartner "80% by 2026" → 실재 예측, Backstage(CNCF) 실재. 단 today 덱스 위키 draft(`2026-06-29-dex-golden.md`)에 golden-path 이미 작성됨 → **신규성 낮음, 스킵**

---

## 오늘 배운 것

- **OTel Profiles 신호 공식화** — eBPF 기반 연속 프로파일링이 OTel Collector receiver로 통합돼 추가 계측 없이 전 언어 스택 프로파일링 가능한 방향으로 표준화 진행 중. 기존 Parca/Pyroscope 권고의 공식 상위 표준(GA 일정 미정, Alpha 단계).
- **Chainguard Images — distroless 직접 채택 패턴** — 자체 distroless 이미지 빌드 없이 Zero-CVE(셸·패키지 매니저 제거) 이미지를 그대로 채택. SBOM·Sigstore 서명 기본 내장으로 공급망 검증 부담 감소. 기존 "distroless 베이스 전환" 인사이트의 구체적 실행 경로.
- **Actions SHA 전체 고정 + Renovate 자동갱신** — tj-actions/changed-files 변조(2025-03) 이후 OpenSSF 공식 권고: `uses:` 구문을 full commit SHA로 고정하고 Renovate/Dependabot으로 자동갱신. 태그(`v4`) 고정은 변조 방어 불가.
- **OpenSSF Scorecard — CI 보안 게이트** — 레포 보안 항목(Actions SHA 고정·브랜치 보호·SAST·의존성 업데이트·코드 리뷰)을 0~10점으로 자동 평가. CI 게이트로 연결해 임계점 미달 PR 차단 가능.
- **Dagger — 코드형 이식성 CI 파이프라인** — Go/Python/TypeScript로 파이프라인을 작성해 로컬과 CI에서 완전히 동일하게 실행. YAML "로컬 재현 불가" 문제 해소. 단일 서버 환경에서도 로컬 검증 후 CI 그대로 이식 가능.

## 출처

- [opentelemetry-ebpf-profiler GitHub](https://github.com/open-telemetry/opentelemetry-ebpf-profiler)
- [OpenSSF — Securing CI/CD After tj-actions & reviewdog Attacks](https://openssf.org/blog/2025/06/11/maintainers-guide-securing-ci-cd-pipelines-after-the-tj-actions-and-reviewdog-supply-chain-attacks/)
- [OpenSSF Scorecard](https://www.scorecard.dev/)
- [Dagger Docs](https://docs.dagger.io/)
- [Chainguard Images](https://www.chainguard.dev/chainguard-images)

## 위키화 후보

- **Actions SHA 고정 + Renovate** — CI 공급망 하드닝 절차(고정 방법·Renovate 설정 예시)를 단독 개념 노트로 정리할 가치 있음
- **OpenSSF Scorecard** — CI 보안 점수화 도구로 독립 노트 가치 있음(기존 Trivy·Kubescape 노트와 연결)

## 프로필 반영 후보 (저위험)

- **Chainguard Images** — 기존 "distroless 베이스 전환" 권고에 "또는 Chainguard 이미지 직접 채택" 을 병행 옵션으로 추가
- **Actions SHA 전체 고정 + Renovate** — 기존 `GitHub Actions OIDC job_workflow_ref` 파이프라인 하드닝 체크리스트에 SHA 고정 항목 추가

## 승인 필요 (고위험)

- **OpenSSF Scorecard를 CI 배포 게이트로 추가** — 점수 임계값 미달 시 PR 차단하는 스텝을 autobots CI에 추가하는 것은 기존 배포 정책 변경이므로 승인 필요 (에러 버짓 게이트와 동일 카테고리)

## 신규 도구 후보 (에이전트/스킬)

- [skill] `scorecard-gate` — OpenSSF Scorecard를 CI 파이프라인에 연결하고 임계값 설정을 자동화하는 스킬 (반복 설정 작업)
