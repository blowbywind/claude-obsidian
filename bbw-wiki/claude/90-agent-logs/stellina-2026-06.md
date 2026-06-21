# 스텔리나 학습 로그 — 2026-06

| 날짜 | 주제 | 요약 |
|------|------|------|
| 2026-06-20 | CI/CD best practices, container security | GitHub Actions: 액션은 반드시 SHA 고정 — 2026년 Q1에 `tj-actions/changed-files` 등 태그 참조 액션이 공급망 공격으로 23,000+ 레포를 침해. `uses: action |
| 2026-06-20 | CI/CD best practices, container security | SBOM/SLSA가 엔터프라이즈 표준화 진행 중: 규제 압력으로 SBOM 강제와 SLSA(공급망 레벨)가 표준이 되어가는 중. Docker Engine 25+는 `--sbom=true`로 빌드 시 SBOM을 atte |
| 2026-06-21 | CI/CD best practices, container security | DORA 메트릭 2026 역설 — AI 도입이 개인 생산성은 올리지만 팀/조직 안정성(변경 실패율·복구 시간)을 오히려 악화시키는 사례 증가. Goodhart's Law("지표가 목표가 되면 지표 신뢰성↓") 적용  |
| 2026-06-21 | CI/CD best practices, container security | Falco + eBPF 런타임 보안: 이미지 스캔은 배포 *전* 정적 검사만 하지만, Falco는 커널 시스템콜을 실시간 감시해 컨테이너 *실행 중* 이상행위(예상 외 outbound 연결, crypto 마이닝)를  |
