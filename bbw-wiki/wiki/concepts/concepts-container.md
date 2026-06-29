---
title: `concepts/container
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-stellina-learning]]
summary: "컨테이너 워크로드는 Distroless 이미지·Cosign 서명·Trivy 스캔·Blue-Green 배포·OpenTelemetry 관찰성을 빌드부터 배포까지 일관되게 검증하는 파이프라인이 2026년 운영의 핵심입니다"
---

# `concepts/container

마크다운 본문을 작성하겠습니다.

---

**컨테이너**(Container)는 애플리케이션과 의존성을 격리된 가상 환경에서 실행하는 경량 패키징 기술입니다. 2026년 기준 컨테이너 워크로드 보안과 운영의 핵심은 빌드부터 배포까지 일관된 검증 파이프라인 구축입니다.

## 요점

**1. 이미지 보안 강화**  
Distroless 이미지로 셸·패키지매니저 제거하여 공격 표면 최소화. 빌드 후 Cosign으로 이미지 서명 → 배포 전 Cosign verify로 검증. Docker Engine 25+ 기준 `--sbom=true` 빌드 옵션으로 SBOM(Software Bill of Materials)을 Attestation으로 생성하며, SBOM/SLSA 준수가 엔터프라이즈 표준화 진행 중입니다.

**2. 취약점 스캔 게이트**  
Trivy/Grype를 CI 파이프라인에 배치하여 푸시 전·이미지 프로모션 시 스캔. OS 패키지·언어 의존성·IaC·K8s 리소스를 포괄하며, 알려진 CVE의 80% 이상을 배포 전 차단합니다.

**3. 배포 전략**  
Blue-Green(즉시 롤백, 비용 2배) 또는 Canary(단계적 트래픽 이동, 위험 최소화) 선택. Docker Compose 환경에선 서비스 이름 전환으로 Blue-Green 구현이 간단합니다.

**4. 관찰성 통합**  
OpenTelemetry Collector의 docker_stats 리시버로 CPU·메모리·네트워크 I/O 메트릭, filelog 리시버로 로그를 단일 OTLP 파이프라인으로 수집합니다.

## 출처
- https://orca.security/resources/blog/container-security-best-practices/
- https://signoz.io/guides/container-observability/
- https://calmops.com/software-engineering/continuous-deployment-strategies-blue-green-canary/
- https://www.aikido.dev/blog/container-security-best-practices
- https://vucense.com/dev-corner/container-vulnerability-scanning-2026/

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
