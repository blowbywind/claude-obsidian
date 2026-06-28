---
title: "Claude Code + Obsidian + LM Wiki + Graphify 실습 가이드"
type: source
tags: [claude-code, obsidian, lm-wiki, graphify, knowledge-management]
created: 2026-06-05
updated: 2026-06-05
origin: https://youtu.be/cNlvrU-KcRg
author: 브레인 트리니티 (브라이언)
date_published: 2026-06-05
summary: "브레인 트리니티 채널이 Karpathy LM Wiki를 Claude Code + Obsidian + Graphify 조합으로 구현하는 볼트 세팅부터 그래프화까지 전 과정을 다룬 AI 지식관리 메타스택 실습 영상."
---

## 요약

브레인 트리니티 채널이 Andrej Karpathy의 LM Wiki 아이디어를 Claude Code + Obsidian 환경에서 직접 구현하는 실습 영상. 볼트 생성 → 핵심 맥락 인터뷰 → CLAUDE.md 생성 → 폴더 구조 세팅 → Web Clipper 템플릿 → 인제스트 스킬 → Graphify 설치까지 전 과정을 다룬다. LM Wiki의 한계(대규모 소스에서 탐색 비효율)를 Graphify로 보완하는 조합이 새로운 메타 스택으로 소개된다.

## 핵심 주장

- Claude Code + Obsidian + LM Wiki + Graphify 조합이 현재 AI 지식 관리의 "메타"로 떠오르고 있다
- LM Wiki의 성패는 **목적성 있는 수집**에 달려 있다 — 왜 수집했는지 설명 못하면 쓰레기 데이터
- Andrej Karpathy가 LM Wiki를 언급한 지 48시간 만에 Graphify가 만들어졌다
- RAG보다 LM Wiki가 세업 복잡도가 낮고, 지식이 복리로 축적된다
- 스킬은 같은 작업을 2~3회 수행한 후 만들어야 패턴을 잘 잡는다
- 각 폴더마다 CLAUDE.md를 두면 해당 폴더 맥락까지 AI가 자동으로 파악한다

## 단계별 세팅 프로세스

1. **새 Obsidian 볼트 생성** — 전용 볼트로 시작
2. **핵심 맥락 작성** — "나는 누구인가 / 왜 기록하는가 / 어떤 아웃풋을 만들고 싶은가" 3가지 질문에 STT로 답변
3. **Claude Code 인터뷰** — 맥락 파일을 바탕으로 AI가 심층 인터뷰 → 핵심 맥락 노트 업데이트
4. **CLAUDE.md 생성** — 인터뷰 내용 + LM Wiki 패턴 문서를 넣고 스키마 생성 요청
5. **폴더 구조 자동 생성** — raw/, wiki/, output/ 및 각 폴더 CLAUDE.md 자동 생성
6. **Web Clipper 템플릿 생성** — 기존 템플릿 JSON을 AI에 제공 → article/youtube/podcast/book/research 5종 템플릿 생성
7. **인제스트 스킬 생성** — `/ingest`: 새 raw 파일 읽기 → 사용자 관점 질문 → 위키 반영
8. **쿼리/린트 스킬 생성** — `/query`: 위키 기반 답변, `/lint`: 위키 전체 건강 점검
9. **Graphify 설치 및 실행** — `pip install graphify`, `graphify wiki` → graph.json + graph.html 생성
10. **Graphify 쿼리** — `graphify query "질문"` → 그래프 탐색 기반 답변

## 연결된 개념

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]]
- [[wiki/concepts/graphify|Graphify]]
- [[wiki/concepts/purposeful-collection|목적성 있는 수집]]
- [[wiki/concepts/rag|RAG]]
- [[wiki/concepts/second-brain|세컨드 브레인]]
- [[wiki/concepts/claude-code-commands-skills|커맨드 & 스킬스]]

## 연결된 엔티티

- [[wiki/entities/brain-trinity|브레인 트리니티]]
- [[wiki/entities/claude-code|Claude Code]]
- [[wiki/entities/obsidian|Obsidian]]
- [[wiki/entities/graphify|Graphify]]
- [[wiki/entities/antigravity|Antigravity]]

## 메모

- 영상에서 사용한 IDE는 Antigravity (Google의 AI 통합 개발 환경)
- Web Clipper 템플릿 JSON은 영상 설명란에 공유 예정이라고 언급
- Graphify는 매우 최근 도구라 영상 이후 업데이트가 많을 것이라 본인도 언급
- 스킬 내 질문(사용자 관점 입력) 단계는 선택사항이지만, 목적성 있는 수집을 위해 권장
