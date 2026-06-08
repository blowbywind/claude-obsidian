---
title: Generator-Evaluator 패턴
type: concept
tags: [multi-agent, evaluation, harness, anthropic, planner]
created: 2026-06-07
updated: 2026-06-08
sources: [2026-06-07-harness-engineering-guide, 2026-06-08-claude-code-harness-castlestudio]
---

## 정의

코드·콘텐츠를 생성하는 에이전트(Generator)와 결과물을 검증하는 에이전트(Evaluator)를 분리하는 멀티 에이전트 설계 패턴. Anthropic이 GAN(Generative Adversarial Network)에서 영감을 받아 제안했다.

## 상세

### 두 가지 근본 문제 (Anthropic 연구팀 발견)

**1. 컨텍스트 불안 (Context Anxiety)**
대화가 길어질수록 AI가 지쳐 대충 마무리하려는 경향. 야근이 길어지면 직원이 퇴근 직전 보고서를 슬쩍 넘기는 것과 동일.

**2. 자기 평가 편향 (Self-Evaluation Bias)**
AI가 자신이 만든 결과물을 평가하면 항상 잘했다고 판단. 실제로 게임플레이가 안 되는 결과물에도 "완성됐습니다"라고 보고.

### 기본 구조 (2에이전트)

```
[Generator Agent] → 생성(코드, 디자인, 콘텐츠)
        ↓
[Evaluator Agent] → 독립적 평가 기준으로 검증 + 실제 도구 사용
        ↓
피드백 → Generator가 수정 → 반복
```

Evaluator는 Generator와 완전히 분리된 별도 에이전트로, **더 엄격하게 튜닝**하는 것이 가능하다.

### 확장 구조: Planner 추가 (3에이전트)

복잡한 앱 개발에는 Planner가 추가된다:

```
[Planner] → 1줄 요청을 전체 스펙으로 전개 (WHAT, HOW는 위임)
     ↓
[Generator] → 스프린트 단위로 기능 하나씩 개발
     ↓
[Evaluator] → 스프린트 전 성공 기준 합의 → 실제 앱 테스트 → 버그 보고
     ↓
피드백 루프
```

**Planner 원칙**: 무엇을 만들지만 결정하고, 어떻게 만들지는 Generator에게 위임. 기획 단계의 기술 오류가 전체로 전파되는 것 방지.

**Evaluator의 실제 로그 예시**:
> "사각형 채우기 도구가 드래그 영역으로 채워야 한다. 실패. 시작점·끝점에서만 타일이 찍히고 가운데가 안 채워진다."

### Anthropic 실험 결과: $9 vs $200

동일한 Claude 모델, 동일한 태스크("레트로 게임 만들어줘"):

| | 단일 에이전트 ($9) | 3에이전트 구조 ($200) |
|--|----------|-----------|
| 결과 | 그럴 듯한 외관, 캐릭터 꼼짝 안 함 | 실제 플레이 가능 |
| 기능 수 | 기본 에디터 2개 (동작 안 함) | 레벨 에디터, 스프라이트, 애니메이션, 사운드, AI 스프라이트 생성, AI 레벨 디자이너 |
| 시간 | 20분 | 6시간 |

**유일한 차이: 구조.**

### 네덜란드 미술관 웹사이트 실험 (2에이전트, 15회 반복)

- 1~9회: 예상 가능한 깔끔한 디자인 (보라색 그라데이션 흰 카드 등)
- **10회차**: AI가 스스로 방향을 틀어 CSS 3D 공간으로 전환
  - 체크무늬 바닥, 갤러리 간 문 이동, "미술관 안을 걷는" 경험
  - Anthropic도 예상 못 한 결과 — AI가 "이 방향은 한계가 있다"고 판단해 완전히 다른 시도

### 모델 개선과 구조의 진화

더 좋은 모델이 나오면:
- **사라지는 것**: 컨텍스트 불안 → 스프린트 구조 제거 가능
- **유지되는 것**: Evaluator (마지막 디테일 버그는 여전히 놓침)

> "모델이 좋아져도 한계와 조합의 가능성은 줄어들지 않는다. 이동할 뿐이다." — Anthropic 연구자

음악 DAW 예시 (단순화된 구조): 1줄 프롬프트, 3h50m, $124 → 멜로디·드럼·믹싱 가능. Evaluator가 여전히 버그 2개 포착.

### 하네스 법칙 4

"생성과 평가를 분리하라" — [[bbw-wiki/wiki/concepts/harness-engineering|하네스 엔지니어링]] 7가지 법칙 중 하나로 핵심 원칙으로 자리잡음.

### bbw-wiki와의 관계

현재 bbw의 `~/.claude/CLAUDE.md`에도 품질 게이트로 `code-reviewer → evaluator-strict` 분리 구조가 반영되어 있다.

## 관련 개념

- [[bbw-wiki/wiki/concepts/harness-engineering|하네스 엔지니어링]] — 이 패턴을 법칙 4로 포함
- [[bbw-wiki/wiki/concepts/agentic-loop|에이전트 루프]] — Generator-Evaluator가 동작하는 루프
- [[bbw-wiki/wiki/concepts/context-engineering|컨텍스트 엔지니어링]] — 컨텍스트 불안 해결과 연결
- [[bbw-wiki/wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — 실전 적용 맥락

## 관련 엔티티

- [[bbw-wiki/wiki/entities/anthropic|Anthropic]] — 패턴 연구·제안
- [[bbw-wiki/wiki/entities/castlestudio|castlestudio]] — 실험 결과 해설 영상 제작

## 출처

- [[bbw-wiki/wiki/sources/2026-06-07-harness-engineering-guide|하네스 엔지니어링 기초 가이드북]]
- [[wiki/sources/2026-06-08-claude-code-harness-castlestudio|클로드코드 직접 만든 사람이 직접 공개한 사용법]]
