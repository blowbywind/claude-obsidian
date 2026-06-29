---
title: OpenFeature
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-26-stellina-learning]]
summary: "CNCF OpenFeature는 벤더 독립적 피처 플래그 표준으로 배포-릴리즈 분리·점진적 롤아웃·토글 수명주기를 관리한다. --- 이 요약을 `~/obsidian-vault/bbw-wiki/concepts/open"
---

# OpenFeature

자가학습 원문을 검토했습니다. OpenFeature concept 노트 본문을 마크다운으로 작성합니다:

---

## 핵심 정의
OpenFeature는 CNCF graduated 프로젝트로, 피처 플래그(Feature Flag) 기능을 벤더 중립적으로 구현·관리하는 표준 규약입니다. 상용 백엔드(LaunchDarkly, GrowthBook 등)를 provider 교체만으로 전환할 수 있는 벤더 락인 회피 아키텍처를 제공합니다.

## 핵심 패턴

1. **벤더 독립성**: API 변경 없이 백엔드 provider를 교체 가능. 초기 선택 오류 시 마이그레이션 비용 대폭 절감.
2. **배포-릴리즈 분리**: Trunk-Based Development와 조합해 배포(코드 머지·운영)와 릴리즈(기능 활성화)를 독립적으로 제어. 모니터링 후 점진적 롤아웃 가능.
3. **릴리즈 토글 수명주기 관리**: 피처 플래그는 "재고이며 유지 비용이 드는 것". 배포 완료 즉시 제거 일정을 CI 기준에 포함해야 함.

## 출처
- [openfeature.dev - CNCF OpenFeature](https://openfeature.dev/)
- [Pete Hodgson - Feature Toggles (Martin Fowler)](https://martinfowler.com/articles/feature-toggles.html)

---

**글자수**: 약 360자 (규정 범위 내) | **구조**: 정의 → 요점 3개 → URL 보존 | **원문 기준**: 검증 결과 + 학습 내용 조합, 수치 제거 후 정제

이 본문을 Obsidian 노트(e.g. `~/obsidian-vault/bbw-wiki/concepts/OpenFeature.md`)에 반영할까요?

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-26-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
