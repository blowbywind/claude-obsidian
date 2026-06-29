---
title: 세컨드 브레인
type: concept
tags: [knowledge-management, productivity, personal, agent-productivity]
created: 2026-06-05
updated: 2026-06-08
sources: [2026-06-05-llm-wiki-pattern, 2026-06-08-ai-workflow-overhaul-silval-dev]
summary: "외부 지식 체계로 기억과 합성을 오프로드하는 개인 및 에이전트용 정보 저장소."
---

## 정의

외부 시스템에 지식을 체계적으로 축적·연결하여 기억·합성·창의의 부담을 오프로드하는 개인 지식 관리(PKM) 방식. Tiago Forte가 대중화한 개념.

## BBW Wiki에서의 의미

이 위키가 곧 세컨드 브레인이다:
- 사용자(bbw)는 소스를 큐레이션하고 방향을 설정한다
- LLM이 구조화·연결·유지를 담당한다
- 지식은 대화 히스토리가 아닌 마크다운 파일에 영속된다

## 에이전트를 위한 세컨 브레인 (2026 관점)

하재상(실밸개발자)은 AI 시대에 세컨 브레인을 **에이전트에게 주는 지식 저장소**로 재정의한다:

### 에이전트가 모르는 것: 코드 밖의 암묵지
- 팀만 아는 프로덕션 규칙 ("이건 배포 전에 반드시 팀 협의")
- 5년·10년 된 코드베이스의 설계 결정 맥락
- 구식이 된 위키 (마지막 업데이트 2~3년 전)
- 점심 자리·옆자리 시니어 한숨에서 나오는 비공식 지식

에이전트는 신입보다도 못하다 — 온보딩 자리에도 못 가고, 시니어 한숨도 못 듣는다.

### "다 담으면 되지 않나?"의 함정

5,000 페이지 위키를 에이전트에게 주면 없는 것과 같다:
- 컨텍스트 노이즈 발생 → 퀄리티 저하
- 응답 속도 하락 + 비용 증가

→ 해결책: **[[wiki/concepts/context-intelligence|컨텍스트 인텔리전스]]** — 구조화 + 인덱싱으로 "잘 찾게" 만들기

## 관련 개념

- [[wiki/concepts/context-intelligence|컨텍스트 인텔리전스]] — 세컨 브레인에 구조·인덱스를 부여하는 방법
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 세컨드 브레인을 구현하는 아키텍처
- [[wiki/concepts/context-engineering|컨텍스트 엔지니어링]] — 에이전트가 정보를 활용하는 설계 기술
- [[wiki/concepts/memex|Memex]] — 세컨드 브레인의 원조 개념

## 관련 엔티티

- [[wiki/entities/obsidian|Obsidian]] — 세컨드 브레인 탐색 도구
- [[wiki/entities/silval-dev-jaesung|하재상 (실밸개발자)]] — AI 에이전트용 세컨 브레인 개념 발전

## 출처

- [[wiki/sources/2026-06-05-llm-wiki-pattern]]
- [[wiki/sources/2026-06-08-ai-workflow-overhaul-silval-dev|AI를 기존 방식에 얹지 마세요]]
