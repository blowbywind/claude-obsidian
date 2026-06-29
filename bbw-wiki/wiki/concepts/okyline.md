---
title: `Okyline`
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-25
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-25-haeri-learning]]
summary: "Okyline은 Data Contract를 기반으로 데이터 유효성을 자동 검증하고 파이프라인 배포 단계에서 품질 저하를 차단하는 데이터 설계 도구다."
---

# `Okyline`

마크다운 본문(frontmatter·h1 제외, 한국어 300~700자 구조) 작성하겠습니다.

---

## 핵심 정의
Okyline은 단일 실행 계약(Data Contract)을 기반으로 데이터 유효성과 실시간 품질 제어를 수행하는 데이터 설계 도구다. 데이터 파이프라인에서 CI/CD 단계에 자동 검증을 통합하여 배포 전에 데이터 품질을 강제함으로써 운영 장애를 사전에 차단한다.

## 주요 특징

- **비즈니스 로직 기반 검증**: 단순 스키마 오류를 넘어 유효 범위(validity range), 참조 무결성(referential integrity) 등 비즈니스 규칙까지 데이터 계약에 명시하고 자동 검증
- **실시간 품질 제어**: 파이프라인의 각 단계에서 지속적으로 데이터 상태를 모니터링하고 품질 저하 시 즉시 반응
- **배포 차단 게이트**: 데이터 계약 규격 위반 시 빌드를 자동으로 차단하여 비정상 데이터 배포 방지

## 출처
- [TxMinds: Data Contract and Pipeline Quality](https://www.txminds.com)
- [Braintrust: Best AI Eval Tools for CI/CD Pipelines](https://www.braintrust.dev/articles/best-ai-evals-tools-cicd-2025)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-25-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
