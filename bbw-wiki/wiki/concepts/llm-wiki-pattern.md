---
title: LLM Wiki 패턴
type: concept
tags: [knowledge-management, llm, wiki, architecture]
created: 2026-06-05
updated: 2026-06-10
sources: [2026-06-05-llm-wiki-pattern, 2026-06-05-claude-code-obsidian-lmwiki-graphify, 2026-06-10-free-roaming-agents-comparison]
---

## 정의

LLM이 단순 검색 인덱스가 아닌 **편집자**로서 마크다운 위키를 점진적으로 구축·유지하는 지식 관리 패턴. 소스가 추가될 때마다 LLM이 관련 페이지를 생성·갱신하므로, 지식이 세션을 넘어 누적된다.

## RAG와의 차이

| 항목 | RAG | LLM Wiki |
|------|-----|----------|
| 지식 처리 시점 | 질의마다 재발견 | 인제스트 시 한 번 컴파일 |
| 교차 참조 | 없음 | 위키 링크로 사전 구축 |
| 모순 감지 | 없음 | 인제스트·린트 시 명시 |
| 누적 | 없음 | 소스가 늘수록 복리 |
| 인프라 | 임베딩·벡터 DB 필요 | 마크다운 파일만 |

## 3개 레이어 아키텍처

1. **원본 소스 (raw/)** — 불변. LLM이 읽기만 한다. 진실의 원천.
2. **위키 (wiki/)** — LLM이 생성·유지하는 마크다운 파일. 사용자는 읽고 탐색.
3. **스키마 (CLAUDE.md)** — 에이전트 지시서. 구조, 규칙, 워크플로우 정의. 사용자와 LLM이 공동 진화.

## 핵심 인사이트

- 위키 유지의 핵심 장벽은 **지루함과 반복 작업**이다. LLM은 지루해하지 않는다.
- 좋은 질의 결과를 페이지로 저장하면 **탐색 자체가 지식으로 누적**된다.
- index.md는 LLM의 "목차" — 질의 전 먼저 읽어 관련 페이지를 파악한다.

## 적용 도메인

- 개인: 목표·건강·심리·자기계발 추적
- 연구: 논문·보고서 장기 축적
- 독서: 챕터별 인제스트 → 팬 위키 수준의 동반 위키
- 비즈니스: Slack 스레드·회의록·고객 콜 → 자동 유지 내부 위키

## 관련 개념

- [[wiki/concepts/rag|RAG]] — LLM Wiki가 대체하거나 보완하는 패턴
- [[wiki/concepts/memex|Memex]] — 정신적 선조: 연상 링크 기반 개인 지식 저장소
- [[wiki/concepts/second-brain|세컨드 브레인]] — 이 패턴이 구현하는 목표

## 세팅 프로세스 (실습 기반)

Andrej Karpathy 제안 → 브레인 트리니티가 실제 구현한 순서:

1. 핵심 맥락 3문항 작성 (나는 누구 / 왜 기록 / 어떤 아웃풋)
2. Claude Code 인터뷰로 맥락 구체화 → CLAUDE.md 생성
3. 폴더 CLAUDE.md 포함한 raw/wiki/output/ 구조 자동 생성
4. Obsidian Web Clipper 커스텀 템플릿 5종 생성 (article/youtube/podcast/book/research)
5. /ingest, /query, /lint 스킬 생성 (2~3회 직접 수행 후 스킬화 권장)
6. Graphify로 그래프 DB 보완

## 마크다운의 토큰 효율성
김요일(2026.06.10 영상)이 인용한 수치: 마크다운은 HTML 대비 **토큰 소모량 65–90% 감소**.
- HTML은 웹태그·CSS 클래스 등이 많아 LLM이 파싱할 때 무거움
- 마크다운은 필요한 데이터만 압축 → 처리 속도 빠르고, 동일 비용에 더 많은 컨텍스트
- 에이전트 직원 관점: B(마크다운 환경)가 A(HTML 환경)보다 같은 일을 더 빠르게, 더 저렴하게 처리

> "AI 에이전트가 B라는 직원이 될 수 있도록 환경을 만들어 주는게 마크다운이다." — 김요일

유훈식 교수(AI4UX) 추가 수치: 마크다운이 HTML 대비 처리 속도 **35% 향상** (김요일 영상의 65-90% 토큰 절감과 별도 연구 기반, 상이한 수치 → 출처마다 다를 수 있음).

> "AI가 이 문서를 읽을 때 85% 정도 토큰을 아낄 수 있다. 시간도 35% 더 빠르다." — 유훈식 교수

## Graphify와의 결합

소스가 많아질 경우 단순 텍스트 검색은 비효율적. Graphify가 wiki/ 폴더를 지식 그래프로 변환하여 Claude Code가 그래프 탐색 기반으로 쿼리할 수 있게 한다. → [[wiki/concepts/graphify|Graphify]] 참조

## 관련 엔티티

- [[wiki/entities/obsidian|Obsidian]] — 위키 탐색 IDE
- [[wiki/entities/qmd|qmd]] — 규모 확장 시 검색 엔진
- [[wiki/entities/graphify|Graphify]] — 그래프 DB 보완 도구
- [[wiki/entities/brain-trinity|브레인 트리니티]] — 한국어 실습 사례

## 출처

- [[wiki/sources/2026-06-05-llm-wiki-pattern]]
- [[wiki/sources/2026-06-05-claude-code-obsidian-lmwiki-graphify]]
- [[wiki/sources/2026-06-12-llm-wiki-selection-criteria]]
