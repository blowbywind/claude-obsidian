---
title: 자유령 에이전트 (Free-Roaming Agent)
type: concept
tags: [ai-agent, autonomous, free-roaming, personal-agent]
created: 2026-06-10
updated: 2026-06-10
sources: [2026-06-10-free-roaming-agents-comparison]
---

## 정의
개인이 소유·운영하는 자율 AI 에이전트 카테고리. 단순 챗봇(질문→답변)과 달리 스스로 작업을 계획·실행하고, 채널(Telegram·Slack 등)을 통해 사용자 지시를 받아 로컬 PC 또는 클라우드 환경에서 자유롭게 작업을 처리한다. 헤르메스 에이전트·OpenClaw·Gemini Spark가 같은 동족(동일 카테고리)이다.

## 핵심 특성
- **자율 실행**: 사용자가 지켜보지 않아도 정해진 시간에 자동 작업 처리
- **채널 연동**: 메시징 채널(Telegram·Slack·Discord 등)을 인터페이스로 사용
- **모델 교체 가능**: LLM(두뇌)을 Codex·Claude·Gemini 등으로 교체 가능 (Gemini Spark 제외)
- **기억 및 성장**: 작업 히스토리를 기록해 시간이 지날수록 성장 (특히 헤르메스)

## 현재 대표 3종 (2026.06 기준)

| 에이전트 | 제작 | 출시 | 환경 | 특장점 |
|---|---|---|---|---|
| OpenClaw | Peter Steinberger → OpenAI 인수 | 2026.01 | 로컬 PC | 다수 병렬 에이전트, 22채널 |
| 헤르메스 에이전트 | Nous Research | 2026.02 | 로컬 PC | 자기 진화형, 장기 육성 최적 |
| Gemini Spark | Google | 2026.06 (미국 부분) | 클라우드 | Google 생태계 완전 통합 |

## 로컬 vs 클라우드 차이

| 항목 | 로컬 (헤르메스·OpenClaw) | 클라우드 (Gemini Spark) |
|---|---|---|
| 필요 조건 | 여분 PC 필수 | PC 불필요 |
| 데이터 위치 | 내 기기 | 구글 서버 |
| 모델 유연성 | 자유 선택 | Gemini 전용 |
| 생태계 통합 | 직접 설정 필요 | Google 서비스 즉시 연동 |
| 진입 장벽 | 터미널 설치 필요 | 채팅창만으로 시작 |

## 에이전트 선택 기준
- **독립 에이전트 장기 육성** → 헤르메스 에이전트
- **다수 에이전트 병렬 처리** → OpenClaw
- **구글 생태계 활용 극대화** → Gemini Spark (한국 출시 대기)
- **ChatGPT 구독 중 → Codex 무료 연동** → 헤르메스 에이전트

## AI 직원 메타포
자유령 에이전트는 "AI 직원"으로 비유된다. 사람을 채용하듯 에이전트를 세팅하고, 행동 기준 규칙(≒CLAUDE.md)을 작성해 역할을 부여하며, LM 위키(옵시디언)로 업무 인수인계 자료를 준비해 줘야 성과가 난다.

## 관련 개념
- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]] — 자유령 에이전트를 팀원으로 구성하는 방법
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]] — 자유령 에이전트의 야간 자율 성장 메커니즘
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 에이전트에게 맥락을 제공하는 세컨드 브레인

## 관련 엔티티
- [[wiki/entities/hermes-agent|헤르메스 에이전트]]
- [[wiki/entities/openclaw|OpenClaw]]
- [[wiki/entities/gemini-spark|Gemini Spark]]

## 출처
- [[wiki/sources/2026-06-10-free-roaming-agents-comparison]]
