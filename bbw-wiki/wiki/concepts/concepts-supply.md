---
title: `concepts/supply
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-stellina-learning]]
summary: "소프트웨어 공급망의 4대 공격 벡터(액션변조·자격증명노출·산출물검증부재·의존성불투명)와 SHA고정·OIDC·SBOM·distroless 등 대응 기법을 설명한 보안 큐레이션 노트이다."
---

# `concepts/supply

## 핵심 정의

**소프트웨어 공급망(Supply Chain)**은 소스 코드 작성부터 배포까지 관여하는 모든 도구·의존성·서비스의 집합이다. GitHub Actions 액션, 패키지 매니저의 타사 라이브러리, 컨테이너 레지스트리 등이 여기 해당하며, 이들 중 하나라도 침해되면 최종 산출물까지 영향을 미친다.

## 주요 공격 벡터 및 대응

**1. Mutable Action References**
— `uses: actions/checkout@v4` 처럼 태그로 액션을 참조하면 중간에 변조될 위험. 2026년 초 `tj-actions/changed-files` 등 공인된 액션들이 공급망 공격으로 23,000+ 레포 침해. 대응: `uses: actions/checkout@<full-sha>`로 고정.

**2. 정적 Credentials 노출**
— AWS/GCP 인증 시 long-lived credentials을 워크플로 시크릿으로 저장하면 유출 위험. 대응: `permissions: id-token: write`로 OIDC 단기 토큰 사용.

**3. 배포 산출물 검증 부재**
— SBOM(Software Bill of Materials)과 이미지 서명 없으면 배포 후 공격자가 쉽게 변조. 대응: Docker 빌드 시 `--sbom=true`로 자동 생성, `cosign sign`으로 서명, Trivy/Grype로 배포 전 CVE 스캔(80%+ 차단율).

**4. 불투명한 의존성**
— distroless 이미지 미적용 시 공격 표면 증대. 대응: 셸·패키지매니저 제거된 distroless 기본 사용.

## 출처

- [Wiz Blog — GitHub Actions Security Guide](https://www.wiz.io/blog/github-actions-security-guide)
- [GitHub Blog — 2026 Security Roadmap](https://github.blog/news-insights/product-news/whats-coming-to-our-github-actions-2026-security-roadmap/)
- [Orca Security — Container Security Best Practices](https://orca.security/resources/blog/container-security-best-practices/)
- [DEV Community — 7 Essential 2026 CI/CD Practices](https://dev.to/dev_narratives_023afd008e/secure-cicd-pipelines-7-essential-2026-best-practices-55mk)
- [Aikido — Container Security 2026](https://www.aikido.dev/blog/container-security-best-practices)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
