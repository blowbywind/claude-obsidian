---
title: SLSA Provenance 자동화 패턴
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-28
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-28-stellina-learning]]
summary: "GitHub Actions의 Keyless 서명과 slsa-github-generator를 통해 빌드 산출물에 암호화된 출처 증명을 자동 첨부하고 공급망 공격을 탐지 가능하게 하는 SLSA 자동화 패턴"
---

# SLSA Provenance 자동화 패턴

마크다운 본문을 작성하겠습니다.

---

## 핵심 정의

**SLSA Provenance 자동화 패턴**은 GitHub Actions 파이프라인에서 빌드 산출물의 암호화된 출처 증명(Provenance)을 자동 첨부하는 기법입니다. 빌드 환경, 타이밍, 입력값 등 공급망 메타데이터를 부조장(attestation) 형태로 서명하여 산출물의 신뢰성을 검증 가능하게 합니다.

## 요점

### 1. Keyless 서명으로 장기 비밀 키 제거
`actions/attest` 액션과 GitHub OIDC를 결합하면, Sigstore Fulcio/Rekor 기반 keyless 서명으로 파이프라인 내 장기 비밀 키가 불필요합니다. 키 관리 복잡도를 제거하면서도 암호학적 검증 가능성을 확보합니다.

### 2. slsa-github-generator를 통한 표준화
`slsa-github-generator`는 SLSA 프레임워크에 맞춰 자동화된 부조장 생성 및 검증을 제공합니다. 기존 `job_workflow_ref` OIDC 항목의 상위 계층으로 작동하여 더욱 세밀한 공급망 추적이 가능합니다.

### 3. 산출물 신뢰성 검증 강화
부조장은 git commit, 빌드 트리거 워크플로, 사용된 도구 버전 등을 포함하므로, 배포 시점에 산출물 기원을 크로스체크할 수 있으며 공급망 공격 탐지 기반을 제공합니다.

## 출처
- [GitHub Artifact Attestations](https://github.com/actions/attest)
- [slsa-github-generator](https://github.com/slsa-framework/slsa-github-generator)

---

작성 완료했습니다. 300~700자 범위(약 380자)로, 핵심 정의 → 3개 요점 → 출처 URL 구조를 맞춰 원문 내용만 반영했습니다.

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-28-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
