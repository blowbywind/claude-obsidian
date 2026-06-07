---
title: Graphify
type: concept
tags: [knowledge-graph, llm-wiki, tool, graph-rag]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-claude-code-obsidian-lmwiki-graphify]
---

## 정의

Obsidian 마크다운 문서를 지식 그래프(graph.json)로 변환하여 LLM이 그래프 탐색 기반으로 답변할 수 있게 해주는 도구. Andrej Karpathy의 LM Wiki 트윗 후 **48시간 만에** 커뮤니티에서 만들어진 오픈소스 프로젝트.

## 탄생 배경

LM Wiki 댓글에서 "소스가 많아지면 비효율적이다. 그래프 정보를 참고해 LLM이 활용할 수 있으면 좋겠다"는 요청이 올라왔고, 이에 응답해 신속 제작됐다.

## 작동 방식

```
Obsidian wiki/ 폴더
       ↓
graphify wiki        (폴더 지정 실행)
       ↓
graph.json           AI가 쿼리에 활용하는 그래프 데이터
graph.html           사람이 보는 시각화 (노드·엣지·클러스터)
graph_report.md      마크다운 리포트
       ↓
graphify query "질문"  → 그래프 탐색 결과 기반 답변
```

## LM Wiki 단순 검색과의 차이

| 항목 | LM Wiki (텍스트 검색) | LM Wiki + Graphify |
|------|----------------------|-------------------|
| 탐색 방식 | 키워드/grep | 노드-엣지 그래프 탐색 |
| 관계 표현 | 텍스트 링크 | 정량화된 연결 강도 |
| 대규모 성능 | 소스 증가 시 비효율 | 그래프 인덱스로 확장 가능 |
| 클러스터 분석 | 없음 | 커뮤니티 자동 감지 |

## 사용법

```bash
pip install graphify

# 최초 그래프 생성
graphify wiki

# 쿼리
graphify query "브레인 트리니티와 LLM 위키의 차이"

# 업데이트 (변경분만)
graphify wiki --update
```

## 출력 파일

- `graphify_out/graph.json` — Claude Code가 쿼리 시 참조
- `graphify_out/graph.html` — 브라우저에서 열어 시각화 확인
- `graphify_out/report.md` — 마크다운 리포트 (Obsidian에서 확인 가능)

## 한계 및 주의

- 도구 출시가 매우 최근 → 이후 API 변경 가능성 높음
- Python 설치 필수
- 위키 내용이 풍부할수록 그래프 품질 향상

## 관련 개념

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — Graphify가 보완하는 기반 시스템
- [[wiki/concepts/rag|RAG]] — "Graph RAG"와 유사한 개념적 위치

## 관련 엔티티

- [[wiki/entities/graphify|Graphify (도구)]]
- [[wiki/entities/obsidian|Obsidian]] — 소스 마크다운 파일 저장소

## 출처

- [[wiki/sources/2026-06-05-claude-code-obsidian-lmwiki-graphify]]
