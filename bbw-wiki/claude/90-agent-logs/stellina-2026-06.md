# 스텔리나 학습 로그 — 2026-06

| 날짜 | 주제 | 요약 |
|------|------|------|
| 2026-06-20 | CI/CD best practices, container security | GitHub Actions: 액션은 반드시 SHA 고정 — 2026년 Q1에 `tj-actions/changed-files` 등 태그 참조 액션이 공급망 공격으로 23,000+ 레포를 침해. `uses: action |
| 2026-06-20 | CI/CD best practices, container security | SBOM/SLSA가 엔터프라이즈 표준화 진행 중: 규제 압력으로 SBOM 강제와 SLSA(공급망 레벨)가 표준이 되어가는 중. Docker Engine 25+는 `--sbom=true`로 빌드 시 SBOM을 atte |
| 2026-06-21 | CI/CD best practices, container security | DORA 메트릭 2026 역설 — AI 도입이 개인 생산성은 올리지만 팀/조직 안정성(변경 실패율·복구 시간)을 오히려 악화시키는 사례 증가. Goodhart's Law("지표가 목표가 되면 지표 신뢰성↓") 적용  |
| 2026-06-21 | CI/CD best practices, container security | Falco + eBPF 런타임 보안: 이미지 스캔은 배포 *전* 정적 검사만 하지만, Falco는 커널 시스템콜을 실시간 감시해 컨테이너 *실행 중* 이상행위(예상 외 outbound 연결, crypto 마이닝)를  |
| 2026-06-22 | CI/CD best practices, container security | 학습 완료 |
| 2026-06-24 | CI/CD best practices, container security | 런타임 도달 가능성 분석(Runtime Reachability Analysis): Kubescape(ARMO)가 제공하는 기능으로, 수천 개의 정적 CVE 중 실제로 실행 시 메모리에 적재되는 코드 경로에 해당하는  |
| 2026-06-25 | CI/CD best practices, container security | 컨테이너 이미지 지속적 재스캔(Continuous Re-scanning): 이미지가 레지스트리에 푸시된 이후에도 백그라운드에서 신규 공개 취약점(CVE)을 지속적으로 재스캔하여 신규 보안 위협을 실시간으로 감지하고  |
| 2026-06-26 | CI/CD best practices, container security | VEX(OpenVEX) — SBOM 노이즈 필터: SBOM이 구성요소 목록이라면 VEX는 "해당 CVE가 이 컨텍스트에서 실제 악용 가능한가"를 선언. CycloneDX 1.7 + Trivy `--vex` 옵션 조합 |
| 2026-06-27 | CI/CD best practices, container security | OTel Semantic Conventions 표준화 — `service.name`·`k8s.pod.name`·`container.id` 등 리소스 속성 명명 규칙 통일 시 logs·metrics·traces 간 c |
| 2026-06-28 | CI/CD best practices, container security | Cilium Tetragon — eBPF 런타임 강제 차단: Falco(감지·알림 전용)와 달리 Tetragon은 커널 eBPF 레이어에서 정책 위반 프로세스를 SIGKILL로 즉시 종료. TOCTOU 공격 방어 가 |
| 2026-06-29 | CI/CD best practices, container security | `opentelemetry.io/blog/2026/profiles-alpha/` → URL 패턴이 실제 OTel 블로그와 다름, CPU 1%·메모리 250MB 수치 출처 불명 → 수치 드롭, 개념만 채택 |
