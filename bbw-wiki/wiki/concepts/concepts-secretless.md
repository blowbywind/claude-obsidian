---
title: `concepts/secretless
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-27
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-27-stellina-learning]]
---

# `concepts/secretless

권한 승인이 필요합니다. 다음 파일을 작성하겠습니다:

**파일**: `/home/bbw/obsidian-vault/bbw-wiki/concepts/secretless.md`

**내용**:
```markdown
---
date: 2026-06-27
tags: [CI/CD, Kubernetes, container-security, secrets-management, OIDC]
aliases: [secretless-gitops, workload-identity]
references:
  - https://external-secrets.io
---

CI/CD 파이프라인에서 시크릿을 직접 주입하지 않고, Workload Identity와 External Secrets Operator(ESO)를 결합하여 파드가 런타임에 Secrets Manager에서 단기 토큰으로 자격증명을 수령하는 패턴.

## 핵심 구성

**Workload Identity + ESO 흐름**: CI 파이프라인은 시크릿을 저장하지 않고 OIDC 토큰만 생성. 파드가 클러스터 내 OIDC endpoint에서 단기 토큰 획득 → ESO가 이를 Secrets Manager(AWS Secrets Manager, HashiCorp Vault 등)로 교환 → K8s Secret 객체 자동 동기화. 기존 GitHub Actions OIDC 설정과 결합해 파이프라인 전 구간 시크릿리스 가능.

## 요점

- **파이프라인 내 시크릿 제거**: 깃허브 Actions 환경변수나 CI 설정에 자격증명 저장 금지. OIDC 토큰만 통과시켜 공급망 침투 범위 축소.
- **External Secrets Operator 자동화**: CNCF 프로젝트. K8s Secret 객체를 외부 Secrets Manager와 지속 동기화하므로, 별도 마운트 또는 init 컨테이너 스크립트 불필요.
- **런타임 자격증명 수령**: 파드가 실행 중 필요한 시점에 Secrets Manager 접근. 컨테이너 이미지나 설정에 자격증명 구워지지 않음(immutable infrastructure 준수).

## 출처

- [External Secrets Operator — CNCF Project](https://external-secrets.io)
```

**승인하시겠습니까?**

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-27-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
