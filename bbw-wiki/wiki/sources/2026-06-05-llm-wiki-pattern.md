---
title: LLM Wiki — 개인 지식 베이스 구축 패턴
type: source
tags: [knowledge-management, llm, wiki, second-brain]
created: 2026-06-05
updated: 2026-06-05
origin: 사용자 제공 텍스트 (LLM Wiki idea document)
author: 미상
date_published: 2026년경
---

## 요약

RAG가 매 질의마다 지식을 재발견하는 것과 달리, LLM이 직접 마크다운 위키를 점진적으로 구축·유지하는 패턴. 소스를 추가할 때마다 LLM이 관련 페이지를 생성·갱신하므로 지식이 누적되고 교차 참조가 유지된다. 사용자는 소싱과 탐색에 집중하고 LLM이 요약·분류·북키핑을 담당한다.

## 핵심 주장

- RAG는 매번 지식을 재발견한다 — 누적이 없다
- LLM이 유지하는 위키는 소스가 추가될수록 점점 풍부해지는 **복리 효과**를 가진다
- 유지 비용이 제로에 가까워 인간이 포기하는 이유(유지 부담)가 사라진다
- 위키는 3개 레이어로 구성: 원본 소스(불변) / 위키(LLM이 쓴다) / 스키마(에이전트 지시)
- 질의 결과도 위키에 파일로 저장하면 탐색이 지식으로 누적된다
- 인간의 역할: 소스 큐레이션 + 방향 설정 + 좋은 질문. LLM의 역할: 나머지 전부

## 주요 워크플로우

- **Ingest**: 소스 → LLM 읽기 → 사용자 논의 → 소스 페이지 + 관련 페이지 갱신 → index/log 업데이트
- **Query**: 질문 → index 참조 → 관련 페이지 합성 → 인용 포함 답변 → (가치 있으면) 페이지로 저장
- **Lint**: 모순 탐색 / 구식 내용 / 고아 페이지 / 누락 개념 / 데이터 공백 제안

## 연결된 개념

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 이 문서가 설명하는 핵심 개념
- [[wiki/concepts/rag|RAG]] — 이 패턴이 대체하거나 보완하는 방식
- [[wiki/concepts/memex|Memex]] — 정신적 선조: Bush의 연상 링크 기반 개인 지식 저장소
- [[wiki/concepts/second-brain|세컨드 브레인]] — 이 시스템의 목적

## 연결된 엔티티

- [[wiki/entities/vannevar-bush|Vannevar Bush]] — Memex 개념의 원조
- [[wiki/entities/obsidian|Obsidian]] — 권장 IDE (그래프 뷰, Web Clipper, Marp 플러그인)
- [[wiki/entities/qmd|qmd]] — 위키 규모 확장 시 사용할 로컬 검색 엔진

## 메모

- 문서는 의도적으로 추상적 — 구체적 디렉토리 구조·툴링은 도메인과 선호에 따라 다름
- 소스가 ~100개, 페이지가 수백 개 정도까지는 index.md 기반으로 충분; 그 이상은 qmd 고려
- LLM이 마크다운 내 인라인 이미지를 한 번에 읽지 못하는 한계가 있음 — 텍스트 먼저, 이미지 별도 뷰
