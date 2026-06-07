---
title: RAG (Retrieval-Augmented Generation)
type: concept
tags: [llm, retrieval, architecture]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-llm-wiki-pattern]
---

## 정의

질의 시마다 문서 컬렉션에서 관련 청크를 임베딩 검색으로 가져와 LLM 컨텍스트에 주입하고 답변을 생성하는 방식. NotebookLM, ChatGPT 파일 업로드, 대부분의 기업 AI 솔루션이 이 방식을 사용한다.

## 한계

- 매 질의마다 지식을 재발견 — **누적이 없다**
- 여러 문서를 합성해야 하는 미묘한 질문에 약하다
- 교차 참조가 없으므로 연결 관계를 파악하기 어렵다
- 벡터 DB, 임베딩 파이프라인 등 인프라가 필요하다

## 비교

[[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] 참고.

## 관련 개념

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — RAG의 대안/보완

## 출처

- [[wiki/sources/2026-06-05-llm-wiki-pattern]]
