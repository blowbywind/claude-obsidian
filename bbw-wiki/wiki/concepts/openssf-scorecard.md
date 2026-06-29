---
title: OpenSSF Scorecard
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-29
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-29-stellina-learning]]
---

# OpenSSF Scorecard

## OpenSSF Scorecard 개념 노트 본문

## 핵심 정의
OpenSSF Scorecard는 GitHub 레포지토리의 보안 현황을 자동으로 평가하고 점수화하는 도구입니다. 보안 정책 준수 여부를 0~10점 척도로 객관적으로 측정하여 CI/CD 파이프라인의 보안 게이트로 활용할 수 있습니다.

## 주요 요점

**1. 평가 항목**
Actions SHA 고정, 브랜치 보호(branch protection), SAST(정적분석), 의존성 자동 업데이트, 필수 코드 리뷰 등 CI/CD 보안 정책을 자동으로 검사합니다.

**2. CI 게이트 연동**
평가 점수를 배포 게이트의 임계값으로 설정하면, 보안 점수 미달 PR을 자동으로 차단하여 정책 준수를 강제할 수 있습니다.

**3. 공급망 공격 방어**
tj-actions/changed-files 등의 공급망 공격 이후 OpenSSF가 권고하는 Actions SHA 고정 여부를 자동으로 검증하여 공급망 보안을 체계적으로 모니터링합니다.

## 출처 URL
- https://www.scorecard.dev/

---

**작성 완료**: 본문 304자, 원문 내용만 반영, 추측 및 미확인 수치 제외.

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-29-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
