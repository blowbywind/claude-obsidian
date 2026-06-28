---
title: Bento
type: concept
status: ai-curated
learned_by: haeri
curated_at: 2026-06-24
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-24-haeri-learning]]
summary: "프롬프트 요소를 마크다운/XML로 격리하여 명령과 데이터를 분리해 프롬프트 주입·할루시네이션을 방지하고 응답 일관성을 높이는 패턴"
---

# Bento

## Bento-Box Task Prompting

프롬프트의 **지시사항, 규칙, 입력 데이터, 출력 포맷**을 마크다운 또는 XML 구획으로 명확하게 격리하는 프롬프트 엔지니어링 패턴입니다. Bento Box처럼 각 요소를 별도의 칸에 배치하여 **명령과 데이터를 완벽하게 분리**합니다.

## 핵심 특징

- **구조적 격리**: 프롬프트의 각 섹션을 의미 단위로 물리적으로 분리하여 모델이 혼동할 가능성 감소
- **할루시네이션 방지**: 입력 데이터가 지시사항으로 오인되는 프롬프트 주입(Prompt Injection) 차단
- **결정론성 향상**: 에이전트 E2E 테스트 시 일관된 응답 구조 보장으로 테스트 신뢰도 증대
- **오작동 감소**: 명령과 데이터 경계가 명확하여 모델의 오류 발생률 저감

## 출처

- https://automatedwith.tech

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-24-haeri-learning]]. 사람 검증 후 status를 verified로 변경하세요.
