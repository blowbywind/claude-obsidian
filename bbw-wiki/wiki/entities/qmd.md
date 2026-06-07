---
title: qmd
type: entity
tags: [product, software, search, cli]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-llm-wiki-pattern]
---

## 개요

마크다운 파일을 위한 로컬 하이브리드 검색 엔진. BM25 + 벡터 검색 + LLM 리랭킹을 온디바이스로 실행한다.

## 인터페이스

- **CLI**: LLM 에이전트가 셸 명령으로 검색 실행
- **MCP 서버**: LLM이 네이티브 툴로 검색 사용

## 언제 도입할까

위키 소스가 ~100개, 페이지가 수백 개를 넘어서면 index.md 기반 탐색의 한계가 온다. 그 시점에 qmd를 도입하면 된다. 그 전까지는 index.md로 충분하다.

## 주요 연결

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 대규모 위키의 검색 인프라

## 출처

- [[wiki/sources/2026-06-05-llm-wiki-pattern]]
