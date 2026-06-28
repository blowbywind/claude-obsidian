---
title: 자유령 에이전트 3종 비교 — 헤르메스·OpenClaw·Gemini Spark
type: source
tags: [ai-agent, hermes, openclaw, gemini-spark, lm-wiki, obsidian, free-roaming]
created: 2026-06-10
updated: 2026-06-10
origin: https://youtu.be/nmlYSLmmRBg
author: 김요일
date_published: 2026-06-10
summary: "헤르메스·OpenClaw·Gemini Spark 세 자유령 에이전트를 비교하고, 마크다운의 토큰 효율성과 옵시디언 연동으로 AI 네이티브 워크플로우를 구성하는 방법을 카페 UX 프로젝트 실무 시연으로 보여준 김요일"
---

## 요약
김요일이 자유령 에이전트 3종(헤르메스, OpenClaw, Gemini Spark)을 "동족"으로 묶고 그 차이를 비교하며, LM 위키와 옵시디언을 활용한 AI 네이티브 UX 실무 워크플로우를 시연한 영상. 핵심은 로컬(헤르메스·OpenClaw) vs 클라우드(Gemini Spark) 구분, LLM의 두뇌(모델) 교체 가능성, 마크다운의 토큰 효율성이다.

## 핵심 주장
- 헤르메스·OpenClaw·Gemini Spark는 "자유령 에이전트" 동족 — 개인 AI 직원 개념
- 헤르메스·OpenClaw = 로컬 PC 기반, Gemini Spark = 구글 클라우드 기반
- 모든 에이전트의 "두뇌"(LLM 모델)는 교체 가능 — Codex·Claude·Gemini API 연결
- 단, Gemini Spark는 Gemini 모델 전용 (타 API 연동 불확실)
- 마크다운이 HTML 대비 토큰 소모량 **65–90% 감소** → AI 작업 효율 극대화
- 옵시디언 노드 구조로 데이터 연결 → LLM이 관련 자료만 집중 탐색 가능
- 헤르메스 = 독립 에이전트 장기 육성 최적 / OpenClaw = 다수 에이전트 병렬 처리 최적

## 에이전트 선택 기준

| 상황 | 추천 |
|---|---|
| 하나의 에이전트를 장기 육성하고 싶다 | 헤르메스 에이전트 |
| 여러 에이전트를 병렬로 많은 일 처리 | OpenClaw |
| ChatGPT 구독 중 → Codex 무료 연동 원한다 | 헤르메스 에이전트 |
| 구글 생태계(드라이브·Gmail·Docs) 통합 | Gemini Spark (출시 대기) |

## Gemini Spark 주요 정보
- 구글 IO 2026에서 공개 발표
- 현재 미국 Gemini Ultra 구독자에 한해 부분 사용 가능
- 한국 출시: 1–4개월 예상
- 기능: 채팅창으로 Gmail·Docs·Drive·이미지 생성 등 모든 구글 플랫폼 통합 조작
- 음성 대화 지원, 다중 작업 누적 처리

## 헤르메스 에이전트 특징 추가 정보
- **자기 진화형 아키텍처**: 작업 중 미스 수정 시 스스로 마크다운에 히스토리·이슈 기록 → 성장 누적
- **보안**: OpenClaw보다 보안성 높다는 평가 있음 (영상 언급)
- **설치**: 터미널 명령 2개 (`hermes install` → `hermes setup`)
- **채널 연동 사례**: 텔레그램 — 날씨·AI 뉴스(UX/Figma/Google/OpenAI 분류)·사용자 요청 처리
- **ChatGPT 구독 시**: Codex 모델 구독 플랜으로 무료 연동 가능 (OpenClaw는 API 과금만)

## LM 위키 × 옵시디언 핵심 인사이트
- 안드레 카파시가 정의: LLM(언어모델) + IDE(옵시디언) + Wiki(마크다운) 삼위일체
- 마크다운이 HTML 대비 토큰 65–90% 절감 → 동일 비용에 더 많은 컨텍스트
- 옵시디언 노드 구조로 데이터를 사전 연결 → LLM 주의(attention) 효율화
- 나만의 스킬(UX 방법론, 심리학 이론 등)을 마크다운으로 저장 → 에이전트 전문성 부여

## 실무 시연: 카페 UX UI 프로젝트 (헤르메스 + 옵시디언 스킬 35개)
1. 정성적 인터뷰 계획서 자동 생성
2. 사용자 인터뷰 데이터 분석 보고서 (5단계 프레임워크)
3. 페르소나 생성 (목표·동기·행동 패턴·페인포인트·니즈 포함)
4. PRD 문서 작성 (섹션별 콘텐츠 요구사항·기능 요건)
5. HTML 웹사이트 코드 생성
6. 사용성 평가 (휴리스틱 평가 자동화 가능)

## 인용

> "AI 에이전트가 B라는 직원이 될 수 있도록 환경을 만들어 주는게 마크다운이다."

> "나만의 고유한 철학과 아주 디테일한 결과를 만들어 낼 수 있는 것들을 하기 위해서는 얘한테 아주 정교하게 필요한 데이터를 전달해줘야 한다."

> "에이전트들은 자꾸 자유령 에이전트기 때문에 문제를 해결하는 것도 스스로 하도록 자꾸 해 나가게 되고, 기록이 쌓이면 그걸 가지고 지속적으로 성장하는 구조로 간다."

## 연결된 개념
- [[wiki/concepts/free-roaming-agent|자유령 에이전트]]
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]]
- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]]
- [[wiki/concepts/second-brain|세컨드 브레인]]
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]]

## 연결된 엔티티
- [[wiki/entities/kimyoil|김요일]]
- [[wiki/entities/hermes-agent|헤르메스 에이전트]]
- [[wiki/entities/openclaw|OpenClaw]]
- [[wiki/entities/gemini-spark|Gemini Spark]]
- [[wiki/entities/obsidian|Obsidian]]

## 메모
- 영상에서 "안드레 카파시" 언급 = Andrej Karpathy (LM Wiki 개념 제안)
- "티아고 포로테" = Tiago Forte (세컨드 브레인 개념 창시자)
- Gemini Spark 한국 출시 후 별도 특집 예정 (김요일 언급)
- AIDTQ 기술 자격증 과정 홍보 포함 (6단계 워크플로우 기반)
