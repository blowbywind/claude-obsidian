---
title: Graphify
type: entity
tags: [product, tool, open-source, knowledge-graph]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-claude-code-obsidian-lmwiki-graphify]
---

## 개요

Obsidian 마크다운 위키를 지식 그래프(JSON)로 변환해 LLM이 그래프 탐색 기반 쿼리를 수행할 수 있게 해주는 오픈소스 Python 라이브러리. Andrej Karpathy의 LM Wiki 트윗 이후 48시간 만에 커뮤니티 개발자가 제작했다. "Knowledge Graphs for AI Coding Assistants"를 표방한다.

## 설치 및 사용

```bash
pip install graphify
graphify <폴더명>          # 그래프 생성
graphify query "질문"      # 그래프 기반 쿼리
graphify <폴더명> --update  # 변경분만 재추출
```

## 출력물

- `graphify_out/graph.json` — Claude Code 등 LLM이 참조하는 그래프 데이터
- `graphify_out/graph.html` — 시각화 (노드, 엣지, 클러스터)
- `graphify_out/report.md` — 마크다운 분석 리포트

## 주요 연결

- [[wiki/concepts/graphify|Graphify (개념)]]
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]]
- [[wiki/entities/obsidian|Obsidian]]

## 출처

- [[wiki/sources/2026-06-05-claude-code-obsidian-lmwiki-graphify]]
