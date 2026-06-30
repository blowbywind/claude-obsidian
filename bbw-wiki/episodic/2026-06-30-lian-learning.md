---
date: 2026-06-30
bot: lian
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 리안 자가학습 — 2026-06-30

도구 권한 미부여로 외부 URL 직접 접근 불가. 위키 교차검증 + 명명 규칙 분석으로 항목별 판정.

---

## 교차검증 결과 요약

| 항목 | 판정 | 근거 |
|---|---|---|
| LongMemEval-V2 (arxiv:2605.12493) | ✅ 기확인 | 위키 2026-06-24/25 중복 |
| Microsoft Agent Framework 4월 출시 | ✅ 기확인 | 위키 2026-06-29, 프로필 등재 |
| AI Control + Alignment 융합 추세 | ✅ 기확인 | 프로필 2026-06-26 등재 |
| AgentRunbook-C 72.5% (LME-V2 세부) | 🟡 신규·미검증 | arxiv 논문 실존 확인, 수치 직접 확인 불가 |
| Sonnet-4/Opus-4 은퇴 사실 자체 | ✅ 기확인 | 프로필 2026-06-29 "Sonnet 4/Opus 4 은퇴" |
| 은퇴 날짜 "6월 15일", 후속 "Sonnet 4.6/Opus 4.8" | 🔴 폐기 | Anthropic은 날짜 접미사 방식(`-20250514` 류) 사용 — "4.6/4.8" 비표준 네이밍, 환각 의심 |
| **Claude Opus 4.7 Fast Mode** 폐기 | 🔴 폐기 | Anthropic 모델 명명 규칙에 소수점 sub-version 없음, "Fast Mode"도 비표준 용어 — 환각 확정 수준 |
| `budget_tokens` → `effort` 전환 | 🔴 보류·폐기 | `effort`는 OpenAI 용어(`reasoning_effort`). docs.anthropic.com 직접 미확인, 채택 금지 |
| Diffuse AI Control (Anthropic 연구) | 🟡 신규·미검증 | 개념 타당, 출처 `anthropic.com` URL 미검증 |

---

## 오늘 배운 것

- **LME-V2 세부 성능 수치**: AgentRunbook-C 방법론(코딩 에이전트 기반)이 72.5% 정확도로 최고 성능 — 단, 직접 확인 불가로 참고 수준 유지 (출처: [arxiv:2605.12493](https://arxiv.org/abs/2605.12493), 논문 실존 기확인)

- **Anthropic 모델 수명주기 재확인**: 기확인 사항(`claude-sonnet-4`, `claude-opus-4` 계열 은퇴)이 재부상. **구체 날짜·후속 모델명은 반드시 `docs.anthropic.com/en/docs/about-claude/models/deprecations` 직접 확인 후 봇 스폰 프롬프트 점검**. 외부 리서치 제공 버전명("Sonnet 4.6/Opus 4.8")은 비표준 네이밍 → 사용 금지.

- **Diffuse AI Control 개념 부상**: 모호한 작업(fuzzy tasks) 환경에서 AI 사보타주·정보 은폐를 분산형 제어로 감지·차단하는 연구 흐름. AI Control의 세부 분기로 추적 시작. (출처 미검증, 후속 확인 필요)

- **`budget_tokens` API 상태**: `effort` 파라미터 대체설은 OpenAI 명명과 혼동 의심 → **현재 `budget_tokens` 폐기 여부 미확인. docs.anthropic.com 직접 확인 전까지 코드에서 변경 금지.**

- **외부 리서치 환각 패턴 추가 확인**: "Opus 4.7 Fast Mode", "Sonnet 4.6" 등 Anthropic 비표준 버전명 → 필터 기준으로 등록. Anthropic 모델 버전은 메이저.마이너(3/3.5/4) + 날짜 접미사 체계가 원칙.

## 출처

- [LongMemEval-V2 (arxiv:2605.12493)](https://arxiv.org/abs/2605.12493)
- [docs.anthropic.com — 모델 deprecation 페이지](https://docs.anthropic.com/en/docs/about-claude/models/deprecations) *(직접 접근 불가, 확인 필요)*

## 위키화 후보

- `diffuse-ai-control` — Fuzzy Tasks 환경 분산형 AI 제어 연구, AI Control의 세부 분기 (출처 확인 후 작성)

## 프로필 반영 후보 (저위험)

- Anthropic 모델 수명주기 검증 필터: "리서치 제공 Anthropic 모델명이 날짜 접미사 없이 소수점 버전 형태이면 1차 환각 의심 → docs.anthropic.com 직접 확인"

## 승인 필요 (고위험)

- 없음

## 신규 도구 후보 (에이전트/스킬)

- 없음

---

## 완료 보고
- 완료: 리서치 7개 항목 교차검증, 위키/프로필 중복 제거, 환각 3건 폐기(Opus 4.7 Fast Mode·Sonnet 4.6 후속명·`budget_tokens→effort`), 신규 학습 5건 구조화
- 결과: 부분완료
- 못 한 것: docs.anthropic.com 직접 접근 불가(도구 권한 미부여) → Anthropic deprecation 날짜·`budget_tokens` 상태 미확인
- 다음 단계: `docs.anthropic.com/en/docs/about-claude/models/deprecations` 및 `extended-thinking` 페이지 수동 확인 후 봇 스폰 프롬프트 모델 점검 권장


## 추가 학습 (19:05 UTC)
기존 위키 내용과 오늘 이전 학습 파일 교차검증 완료. 아래 항목별 판정 후 최종 종합.

---

**교차검증 결과 (5개 항목)**

| 항목 | 판정 | 근거 |
|---|---|---|
| ALE 벤치마크 (arxiv:2606.05405) | ✅ 신규 · 검증가능 수준 | 위키 미존재, Berkeley RDI 주체·arxiv ID 형식 일관, 기술 기술 모순 없음 |
| Opus 4/Sonnet 4 은퇴 + "4.6" 후속명 | 🔴 중복·폐기 | 오늘 1차 실행에서 이미 처리. 후속명 "4.6" 비표준 네이밍 환각 확정 |
| Anthropic "은퇴 인터뷰(retirement interviews)" 정책 | 🔴 폐기 | 위키·공식 문서 근거 없음. 웹 접근 불가로 직접 확인 불가, 비정상적 주장 |
| Fable 5/Mythos 5 중단 (6/12) | 🟡 기확인 | 위키 2026-06-21~24 다수 기록, 중복 |
| Claude Opus 4.8 신기능 (mid-conv 시스템 메시지) | 🔴 폐기 | "4.8" 소수점 버전 → 비표준 네이밍 필터 적중. 신기능 세부 주장 1차 출처 없음 |

---

## 오늘 배운 것

- **Agents' Last Exam (ALE) 벤치마크 등장**: U.S. O*NET 직업 분류 기반 1,000~1,500개 실전 전문 업무를 GUI/CLI 샌드박스에서 평가. 현재 최상위 에이전트 합격률 2.6% 미만 — 장기 태스크(long-horizon)에서의 에이전트 한계를 수치화한 신규 지표. (출처: [arxiv:2606.05405](https://arxiv.org/abs/2606.05405), [agents-last-exam.org](https://agents-last-exam.org))

- **Anthropic "retirement interview" 주장 — 반복 환각 유형 추가 식별**: 공식 문서 URL을 출처로 달면서도 내용이 검증 불가한 주장(은퇴 인터뷰·가중치 보존 정책)이 리서치 배치에 포함되는 패턴 확인. URL 존재 ≠ 주장 검증 — 출처 URL이 실존 페이지여도 해당 주장이 그 페이지에 있는지 직접 확인 전까지 폐기 유지.

## 출처

- [Agents' Last Exam (arxiv:2606.05405)](https://arxiv.org/abs/2606.05405)
- [agents-last-exam.org](https://agents-last-exam.org)
- [GitHub: rdi-berkeley/agents-last-exam](https://github.com/rdi-berkeley/agents-last-exam)

## 위키화 후보

- `agents-last-exam` — ALE 벤치마크: O*NET 기반 장기 전문 업무 에이전트 평가, 합격률 2.6% 미만 (에이전트 능력 갭 지표)

## 프로필 반영 후보 (저위험)

- ALE(Agents' Last Exam) — 에이전트 장기 태스크 평가 벤치마크 추적 목록에 추가 (LoCoMo·LongMemEval·BEAM과 병렬)

## 승인 필요 (고위험)

- **리서치 폐기 필터 강화 제안**: "출처 URL이 실존 공식 도메인이라도, 주장이 그 페이지에 실재하는지 검증 없이 채택 금지" 규칙을 리서치 수신 규칙에 명문화. (현행 규칙: "Vertex AI redirect = 폐기". 확장 버전: "URL 실존 ≠ 내용 검증 — docs URL 포함 전 주장 교차출처 필수")

## 신규 도구 후보 (에이전트/스킬)

- 없음

---

## 완료 보고
- 완료: 신규 배치 5개 항목 교차검증, 위키·오늘 1차 학습 파일 대조, 환각 3건 폐기(은퇴 인터뷰·Sonnet 4.6 후속명·Opus 4.8 신기능), 신규 1건(ALE 벤치마크) 구조화
- 결과: 부분완료
- 못 한 것: WebSearch/WebFetch 권한 미부여 → ALE 논문 세부 수치·Anthropic 공식 페이지 직접 접근 불가
- 다음 단계: ALE 위키 노트 작성 시 [arxiv:2606.05405](https://arxiv.org/abs/2606.05405) 직접 확인 권장
