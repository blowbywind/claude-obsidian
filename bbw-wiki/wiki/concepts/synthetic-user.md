---
title: 합성 사용자 (Synthetic User)
type: concept
tags: [ux-research, ai-native, persona, data-modeling]
created: 2026-06-10
updated: 2026-06-10
sources: [2026-05-28-ai-native-ux-lm-wiki-60th-seminar]
summary: "실제 사용자 인터뷰 데이터를 LLM으로 모델링해 만든 가상 사용자로, 실시간 대화를 통해 새 기획에 대한 인사이트를 도출할 수 있다."
---

## 정의
실제 사용자 인터뷰·서베이 데이터를 LLM으로 모델링해 만든 가상의 AI 사용자. 실제 데이터를 기반으로 생성되므로, 단순한 페르소나보다 구체적이며 LLM API를 통해 실시간 대화가 가능하다. 유훈식 교수(AI4UX)가 LM 위키 기반 AI 네이티브 UX 리서치의 핵심 응용으로 소개.

## 작동 방식

```
1. 실제 사용자 인터뷰 데이터 → 마크다운으로 저장
2. LLM으로 페르소나 모델링 (Primary/Secondary 페르소나)
3. LLM API(Gemini 등) 연결 → 페르소나와 실시간 대화
4. 새 기획/아이디어에 대한 의견 수렴 가능
```

## 기존 페르소나와의 차이

| 항목 | 기존 페르소나 | 합성 사용자 |
|---|---|---|
| 기반 | 조사 결과를 문서화 | 실제 데이터 기반 LLM 모델 |
| 상호작용 | 문서 읽기만 가능 | 실시간 채팅 대화 |
| 활용 | 디자인 방향 참고 | 새 기획 인사이트 도출 |
| 갱신 | 수동 업데이트 | 데이터 누적 시 자동 반영 |

## 가치와 한계

### 가치
- 사용자 조사 없이 빠른 인사이트 도출 가능 (데이터 누적 후)
- 특정 도메인(금융·헬스케어 등)에서 데이터 축적 시 강력한 자산
- "10년치 데이터가 쌓이면 어마어마한 데이터 자산이 된다"

### 한계
- 실제 사용자 데이터 없이는 허구의 페르소나와 다름없음
- 초기에는 반드시 실제 인터뷰/서베이 데이터 구축 선행 필요
- 도메인별 편향 주의

## LM 위키 내 위치

```
raw/
  └── user-interviews/      ← 실제 인터뷰 데이터 마크다운 저장
wiki/
  └── personas/             ← LLM으로 모델링된 페르소나
synthetic-user/             ← API 연결 가상 사용자 (Gemini/Claude 등)
```

## 관련 개념
- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]] — 데이터 누적 기반
- [[wiki/concepts/ai-native-team|AI 네이티브 팀 구성]] — AI 네이티브 UX 시스템의 일부

## 관련 엔티티
- [[wiki/entities/yu-hunsik|유훈식 교수]] — 실무 시연자

## 출처
- [[wiki/sources/2026-05-28-ai-native-ux-lm-wiki-60th-seminar]]
