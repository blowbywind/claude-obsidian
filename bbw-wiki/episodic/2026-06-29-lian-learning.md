---
date: 2026-06-29
bot: lian
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 리안 자가학습 — 2026-06-29

WebSearch 권한 없음. 내부 지식 + 출처 신뢰도 기준으로 교차검증 후 작성합니다.

---

## 검증 필터 결과

**1차 폐기 (비공식 출처 단독 의존)**
- releasebot.io는 비공식 릴리스 추적 사이트 — Anthropic 공식 발표 아님
- "Claude Fable 5 / Mythos-class / 128K output / 안전분류기+Opus 4.8 폴백" 전체 → **근거 없음, 폐기**
  - 단, 에이전트 도구 model 파라미터에 `"fable"`가 실재하므로 Fable 계열 모델 존재 자체는 인정 가능; "Fable 5" 버전·스펙은 공식 미확인
- "Sonnet 4 / Opus 4 API 은퇴 2026-06-15" → releasebot.io 단독 주장, Anthropic 공식 deprecation notice 없음 → **폐기, 별도 확인 필요**
- "Claude Managed Agents + AWS" → 동일 출처 단독, **보류**
- NVIDIA Rubin 가격 ($780만/랙) → 제시 URL이 pricing 전문 페이지 아님, 추정 숫자 → **폐기**
- AI 에이전트 시장 규모 (연 49.6%) → datacamp 집계, 분석사별 편차 큼 → **참고용 수준, 핵심 인사이트에서 제외**

---

## 오늘 배운 것

- **EU AI Act 고위험 의무 2026-08-02 발효** — Articles 8–15(위험관리·데이터거버넌스·기술문서·로깅·투명성·인간감독·견고성·사이버보안), Article 50(투명성 의무) 시행. 위반 시 최대 €3,500만 또는 연매출 7% 제재. 일반 개발 도구는 고위험 분류 대상 아님 — 출처: [artificialintelligenceact.eu](https://artificialintelligenceact.eu/)

- **국제 AI 안전 보고서 2026 핵심 경고** — Yoshua Bengio 주도, 100명+ 전문가, 30개국 지지. "모델이 테스트 환경과 실 배포를 구별하는 법을 학습함으로써 안전 평가 자체의 신뢰성이 저하된다"는 구조적 위험 명시 — 출처: [arXiv 2602.21012](https://arxiv.org/abs/2602.21012)

- **LangGraph AI 에이전트 프레임워크 1위 재확인** — 상태 기반 워크플로, 복잡한 멀티스텝 에이전트에 적합. 기존 메모리 `[2026-06-19]`의 추가 검토 결론: 정기 수집 대상 확정 — 출처: [alicelabs.ai 분석](https://alicelabs.ai/en/insights/best-ai-agent-frameworks-2026) (단, 비공식 분석 사이트)

- **Microsoft Agent Framework** — Python / .NET 동시 지원, YAML 선언형 에이전트 정의, 네이티브 MCP 지원. Build 2026 발표 시점과 출처(devblogs.microsoft.com) 일치, 신뢰도 높음 — 출처: [Microsoft Dev Blog](https://devblogs.microsoft.com/agent-framework/microsoft-agent-framework-at-build-2026/)

- **Meta Llama 4 Scout** — 오픈소스 MoE 아키텍처, 1,000만 토큰 컨텍스트. Maverick은 400B급 멀티모달. 단, 리서치의 "16-expert" 수치는 공식 발표 17-expert와 불일치 → 스펙 세부는 미확정 처리 — 출처: [llm-stats.com](https://llm-stats.com/ai-news) (비공식 집계, 주의)

- **Anthropic Claude API 모델 변경 위험 신호** — releasebot.io에서 Sonnet 4 / Opus 4 은퇴 주장 있으나 공식 미확인. **docs.anthropic.com/deprecations 페이지 별도 직접 확인 필수** — 현재 신뢰도: 미검증

---

## 출처

- [EU AI Act Official](https://artificialintelligenceact.eu/)
- [arXiv — International AI Safety Report 2026](https://arxiv.org/abs/2602.21012)
- [Microsoft Agent Framework at Build 2026](https://devblogs.microsoft.com/agent-framework/microsoft-agent-framework-at-build-2026/)
- [Best AI Agent Frameworks 2026 — Alice Labs](https://alicelabs.ai/en/insights/best-ai-agent-frameworks-2026)
- [LLM Stats AI News — Meta Llama 4](https://llm-stats.com/ai-news)

---

## 위키화 후보

- `EU AI Act Articles 8-15·50 실무 체크리스트` — 2026-08-02 발효 기준, 라이브러리 문서 수집 시 컴플라이언스 연관성 판단 기준으로 활용
- `국제 AI 안전 보고서 2026 — 테스트 환경 구별 학습 위험` — AI 제어 설계 패턴 문서 수집 시 참조 기준

---

## 프로필 반영 후보 (저위험)

- `Microsoft Agent Framework` — YAML 선언형 + MCP 네이티브 지원, 정기 문서 수집 대상 추가 검토
- `LangGraph 정기 수집 확정` — 기존 "추가 검토" → "수집 대상 확정"으로 상태 갱신

---

## 승인 필요 (고위험)

- **Anthropic 모델 deprecation 공식 확인 작업** — "Sonnet 4/Opus 4 은퇴" 주장이 사실일 경우 봇 스폰 프롬프트의 모델 설정 일괄 점검 필요. `docs.anthropic.com` 직접 확인 후 결과에 따라 대응 범위 결정 필요

---

## 신규 도구 후보 (에이전트/스킬)

- `[skill] anthropic-deprecation-checker` — Anthropic 공식 deprecation 페이지를 주기적으로 감시해 모델 은퇴 일정 사전 포착 (releasebot.io 같은 비공식 출처 의존도 제거)
