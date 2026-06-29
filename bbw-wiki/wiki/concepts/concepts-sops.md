---
title: `concepts/sops
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-22
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-stellina-learning]]
summary: "SOPS는 시크릿 값만 암호화·구조는 평문으로 유지하고 age 암호화·자동 복호화로 GitOps 환경의 시크릿을 안전하게 관리한다."
---

# `concepts/sops

## 마크다운 본문

**SOPS(Secrets Operations)**는 GitOps 환경에서 시크릿을 안전하게 관리하는 도구다. 시크릿 *값*만 암호화하면서 시크릿 *키*는 평문으로 유지해 `.enc.yaml` 파일을 git 저장소에 직접 커밋할 수 있다.

## 핵심 특징

1. **선택적 암호화**: 민감한 값(비밀번호, API 키)만 암호화되고, 구조(스키마)는 평문 유지. git diff로도 변경사항을 추적할 수 있다.

2. **age 암호화 표준화**: PGP 기반 복잡한 키 관리 대신 age 암호화를 사용해 간결성 극대화. 다중 recipient 지원으로 팀 멤버와 CI/CD 서버에 다른 키를 할당 가능: `sops --encrypt --age <pubkey1>,<pubkey2> secrets.yaml`

3. **자동 복호화**: CI/CD 서버에 age 개인키를 recipient로 등록하면, 배포 시 자동으로 시크릿을 복호화해 운영에 투입. 별도 시크릿 관리 백엔드 없이도 동작.

## 출처
- [SOPS + age 파이프라인 통합 — OneUptime](https://oneuptime.com/blog/post/2026-02-09-sops-age-encryption-kubernetes-secrets/view)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
