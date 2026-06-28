---
title: Claude Code ↔ Wiki 관계 전략
type: query
tags: [claude-code, wiki, cost-saving, workflow]
created: 2026-06-06
updated: 2026-06-06
sources: [2026-06-05-llm-wiki-pattern, 2026-06-05-how-claude-code-works]
summary: "Claude Code가 위키를 운영할 때 index.md를 유일한 진입점으로 삼고 queries/ 캐시를 활용해 토큰 절약·정보 유실 방지·반복 질문 제거를 달성하는 양방향 축적 구조 설계 기록."
---

## 질문

Claude Code가 이 위키를 어떻게 운영해야 코인 절약, 정보 유실 방지, 반복 질문 제거를 달성할 수 있는가?

---

## 1. Claude Code ↔ Wiki 진화 방향

현재 구조는 **단방향** (클리핑 → 인제스트 → wiki/) 흐름이다.
목표는 **양방향 축적**: 개발 작업 중 발견한 결정·이슈가 wiki로 역류하는 구조.

```
사용자 질문 → Claude가 index.md 탐색 → 해당 페이지 선택 로드 → 답변
                                                                   ↓
                                               가치 있으면 wiki/queries/ 에 저장 ← 누적
```

---

## 2. 코인 절약 원칙

**index.md가 유일한 진입점**이다. index.md만 읽고 필요한 페이지를 선택 로드한다.

| 비용 원인 | 개선 |
|---|---|
| 세션마다 raw/ 재탐색 | 인제스트 완료 파일 재읽기 금지 |
| 무관한 페이지 전체 로드 | index.md → 관련 페이지만 최대 3개 로드 |
| 이미 답한 질문 재분석 | wiki/queries/ 캐시 활용 |
| 200줄 초과 wiki 페이지 | 분할 신호로 처리 |

---

## 3. 개발 이슈 해결책

### 반복 질문 / 중복 내용

`wiki/queries/`를 적극 활용한다:
- 복잡한 질문에 답한 후 → 자동으로 queries/ 저장
- 다음 세션에서 같은 질문 → index.md에서 발견 → 재분석 없이 재사용

### 정보 유실 방지

두 시스템의 역할을 명확히 분리한다:

| 시스템 | 저장 대상 |
|---|---|
| `~/.claude/memory/` | Claude 행동 방식, 피드백, 사용자 선호 |
| `bbw-wiki/wiki/` | 도메인 지식, 개념, 소스 분석, 결정 이유 |
| `bbw-wiki/log.md` | 작업 이력 (append-only) |

개발 중 유실되기 쉬운 정보:
- "왜 이 라이브러리를 선택했나" → `wiki/concepts/`에 결정 이유 기록
- "이 버그는 왜 발생했나" → `wiki/queries/`에 분석 저장

### 메모리 / 속도

세션 시작 시 비용 상한을 지킨다 (CLAUDE.md에 명시):
```
1. index.md 읽기 (항상, ~50토큰)
2. log.md 마지막 5개 확인 (항상)
3. 태스크 관련 페이지만 선택 로드 (최대 3개)
4. raw/ 재읽기 금지 (인제스트 완료 파일)
```

---

## 결론

위키는 **점진적으로 누적되는 캐시**다. 질의마다 재발견하지 않고, 이전에 한 분석을 queries/에서 꺼내 쓰는 구조가 목표다. index.md의 품질이 전체 효율의 핵심이다.

---

## 관련 개념

- [[wiki/concepts/llm-wiki-pattern|LLM Wiki 패턴]]
- [[wiki/concepts/context-window|컨텍스트 윈도우]]
- [[wiki/concepts/second-brain|세컨드 브레인]]
