---
title: Kiro Ambiguity Detection 패턴
type: concept
status: ai-curated
learned_by: kiel
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-kiel-learning]]
summary: "Kiro 모호성 감지는 요구사항의 해석 모호성을 자동 포착하여 양자택일 질문으로 표면화해 PRD 완성 전 스펙 오류 및 개발 재작업을 방지하는 패턴"
---

# Kiro Ambiguity Detection 패턴

## Kiro Ambiguity Detection 패턴

**핵심 정의**
Kiro의 모호성 감지 기능은 요구사항 문구가 두 가지 이상으로 해석될 수 있을 때 자동으로 감지하여 개발자나 기획자에게 2-option 질문으로 표면화하는 패턴이다. PRD 완성 전 모호한 조건을 선제적으로 제거하여 후속 스펙 오류와 개발 재작업을 방지한다.

**주요 요점**
- **자동 감지 → 양자택일 질문**: 자연언어 해석의 모호성을 AI가 선제 포착하고, 기획자가 즉시 의사결정하도록 유도
- **PRD 품질 향상**: 전문가 기획자가 작성해도 무의식적 표현 모호성을 제거하여, 이후 설계·개발 단계에서 재해석 비용 제거
- **병렬 태스크 실행과 연계**: requirements → design → tasks 3단계 문서 구조 내에서 의존성 그래프를 분석하여 독립 태스크 병렬 실행 지원 (모호성 제거 후 안정적 병렬화 가능)

**출처**
- https://kiro.dev/blog/faster-smarter-specs/
- https://www.developersdigest.tech/blog/aws-kiro-developer-guide-2026

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-kiel-learning]]. 사람 검증 후 status를 verified로 변경하세요.
