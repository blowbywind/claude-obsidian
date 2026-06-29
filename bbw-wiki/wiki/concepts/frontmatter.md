---
title: `frontmatter
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-19-dex-learning]]
summary: "Frontmatter-first는 마크다운의 YAML 메타데이터를 우선하여 LLM이 Summary 필드만으로 관련 노트를 선별하게 하여 토큰 효율화와 검색 정확도를 높이는 원칙이다."
---

# `frontmatter

## 핵심 정의

**Frontmatter-first**는 마크다운 문서의 YAML 메타데이터를 우선하여 구조화하는 원칙이다. 특히 `summary: 1-2줄` 필드를 통해 전체 파일을 로드하지 않고도 LLM 에이전트가 관련 노트를 선별할 수 있게 한다.

## 요점

1. **토큰·레이턴시 효율화**: LLM 에이전트가 메타데이터만 검색하여 관련 노트를 판단하므로 전체 파일 오픈 오버헤드 제거. 컨텍스트 윈도우 절감 및 응답 속도 향상.

2. **지식 그래프 탐색 정확도 향상**: Summary 필드가 없으면 에이전트가 노트의 실제 내용을 모르고 접근하게 되어 관련성 판단 오류 증가. Frontmatter 우선 구조는 선별 정확도를 높인다.

3. **LLM 생성 노트의 무조건적 보완 필요**: LLM이 자동으로 생성한 노트는 frontmatter 누락이 잦으므로 사람의 수동 검토 후 메타데이터 추가가 필수 작업.

## 출처

- [Frontmatter-First Is Not Optional: Context Window Survival for Local LLMs](https://medium.com/@michael.hannecke/frontmatter-first-is-not-optional-context-window-survival-for-local-llms-in-opencode-15809b207977)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-19-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
