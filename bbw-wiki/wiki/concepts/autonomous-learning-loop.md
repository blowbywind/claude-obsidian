---
title: 야간 자율 학습 루프
type: concept
tags: [cron, autonomous, learning, hermes]
created: 2026-06-09
updated: 2026-06-09
sources: [2026-06-09-ai-native-hermes-report]
summary: "에이전트가 크론잡으로 취침 중 자율 학습·리서치를 수행하고 옵시디언 위키화하여 기상 시 활용하는 시간 활용 루프."
---

## 정의
크론잡(예약 작업)을 이용해 에이전트가 취침 중 자율적으로 학습·리서치를 수행하고, 기상 시 결과를 제공하는 루프 구조. "자는 시간을 활용한다"는 것이 핵심 아이디어.

## 상세

### 에이전트별 학습 설계 예시

**개발 에이전트 (효율이)**
- 실리콘밸리 논문·학술 자료, AI 뉴스, Reddit, AI 블로그·커뮤니티 탐색
- 학습 깊이 1–10 숫자로 설정 가능
- 기상 시 방대한 학습 완료 상태

**디자인 에이전트 (효리)**
- Dribbble, Awwwards, Mobbin, Godly 등 UI 레퍼런스 사이트 주기적 탐색
- 감각적 기업·브랜드 공개 디자인 시스템 학습
- OpenDesign (CLI 연결) → 레퍼런스 전달 → "95% 이상 유사도 달성까지 무한 루프"

### 메모리 관리 연계
학습 결과 전부를 에이전트 메모리에 저장하면 메모리 초과 → 성능 저하. 해결책:
1. 분석·학습 완료 → 옵시디언 위키화
2. 메모리는 항상 최대 효율 유지
3. 관련 업무 시 키워드로 옵시디언 검색 후 참조

## 관련 개념
- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]] — 헤르메스 에이전트가 이 루프 담당
- [[wiki/concepts/context-intelligence|컨텍스트 인텔리전스]] — 위키화로 맥락 축적
- [[wiki/concepts/boris-self-learning-loop|Boris 자기학습 루프]] — 유사 패턴 (실수→CLAUDE.md 누적)

## 관련 엔티티
- [[wiki/entities/hermes-agent|헤르메스 에이전트]]
- [[wiki/entities/opendesign|OpenDesign]]
- [[wiki/entities/obsidian|Obsidian]]

## 출처
- [[wiki/sources/2026-06-09-ai-native-hermes-report]]
