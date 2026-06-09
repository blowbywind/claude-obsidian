---
title: OpenDesign
type: entity
tags: [product]
created: 2026-06-09
updated: 2026-06-10
sources: [2026-06-09-ai-native-hermes-report]
---

## 개요
Claude Design을 로컬화한 오픈소스 도구. CLI로 에이전트와 연결하면 디자인 레퍼런스를 받아 UI를 직접 생성·실습할 수 있다. 야간 자율 학습 루프에서 디자인 에이전트(효리)의 실습 도구로 사용된다. (공식 URL 불명확 — 미확인)

## 사용 방법 (김요일 사례)

### 야간 학습 루프에서의 역할
1. 취침 전 디자인 레퍼런스 또는 디자인 시스템을 효리에게 전달
2. OpenDesign을 CLI로 연결 → 효리가 직접 디자인 생성·수정 반복
3. **"95% 이상 똑같이 만들 때까지 무한 루프"** 지시 → 취침
4. 기상 시 목표 유사도에 도달한 결과물 확인

### 조합 학습 전략
OpenDesign 실습 전에 다음 레퍼런스를 먼저 학습:
- Dribbble, Awwwards, Mobbin, Godly 등 UI 레퍼런스 사이트 탐색
- 감각적인 기업·브랜드의 공개 디자인 시스템 학습

→ **이론(레퍼런스 학습) + 실습(OpenDesign 무한 루프)** 조합으로 디자인 능력 향상

## 주요 연결
- [[wiki/concepts/autonomous-learning-loop|야간 자율 학습 루프]] — 핵심 실습 도구로 사용
- [[wiki/entities/hermes-agent|헤르메스 에이전트]] — 효리(효2) 에이전트가 CLI로 연결

## 출처
- [[wiki/sources/2026-06-09-ai-native-hermes-report]]
