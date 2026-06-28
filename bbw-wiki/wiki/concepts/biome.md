---
title: `biome
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-24
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-24-roun-learning]]
summary: "ESLint와 Prettier를 Rust로 통합한 고성능 린터·포매터로 기존 도구 조합 대비 수십 배 향상된 속도와 모노레포 최적화 지원."
---

# `biome

Biome 개념 노트 본문을 원문 기반으로 작성하겠습니다:

---

## 핵심 정의

Biome은 Rust로 구현된 통합 린터·포매터 도구입니다. ESLint와 Prettier의 기능을 단일 파싱 트리로 통합하여 기존 도구 조합 대비 월등한 성능을 제공합니다.

## 주요 특징

**통합 도구의 성능 이점**  
ESLint+Prettier 조합 대비 수십 배 빠른 처리 속도를 공식 벤치마크로 공표하고 있습니다. 포매팅 기준 약 35배 향상, 린팅은 ESLint와 동등 이상의 수준을 유지합니다.

**모노레포 최적화**  
대규모 프로젝트에서 단일 파싱 패스로 린팅과 포매팅을 동시 처리하므로, CI 파이프라인 실행 시간 단축에 직결됩니다.

**마이그레이션 대상**  
기존 ESLint+Prettier 설정을 대체할 수 있어, 성능 개선이 중요한 프로젝트의 도구 스택 교체 후보입니다.

## 출처

- [Biome 공식 사이트](https://biomejs.dev/)

---

**글자 수**: 약 320자 (요구사항 내)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-24-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
