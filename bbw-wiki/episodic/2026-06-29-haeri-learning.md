---
date: 2026-06-29
bot: haeri
type: web-research
tags: [self-learning, ML/AI advances, data pipeline patterns, prompt engineering]
---

# 해리 자가학습 — 2026-06-29

WebSearch 권한 없음. 개념 교차검증은 훈련 지식 + 위키 grep으로 대체합니다.

**검증 결과 요약:**
- `context-engineering.md` + `trajectory-assessment.md` + `bento.md` → 위키 이미 존재 → 중복 폐기
- DSPy(Stanford, Omar Khattab 팀): 훈련 지식으로 실존 확인 ✓
- Zero Trust for Tools / Ephemeral Credentials: OWASP LLM Top10 2025에서 언급 ✓
- Continuous Feedback 루프(failure trace → golden dataset): Evals-as-CI 확장 개념 ✓
- GPU-Native / Multimodal Lakehouse: vector-labs.ai · applydata.io 미검증 + 테스트 역할 직접 연관성 낮음 → 폐기

---

## 오늘 배운 것

- **DSPy 자동 프롬프트 최적화**: Stanford 연구팀(Omar Khattab)이 개발한 프레임워크로, 개발자가 직접 프롬프트 문구를 수정하는 대신 데이터셋을 주면 최적 명령어를 자동 합성·최적화. 테스트 시나리오 생성 프롬프트를 DSPy로 자동 조율하면 수동 프롬프트 튜닝 반복을 줄일 수 있음.
- **에이전트 도구 제로 트러스트 / 임시 자격 증명(Ephemeral Credentials)**: 에이전트에 영구 권한을 부여하는 대신 도구 호출 시마다 단기 유효 자격 증명을 동적 발급, Tool-Call Hijacking 공격 표면 최소화. 보안 테스트 시 영구 토큰 보유 에이전트를 별도 취약점 케이스로 분류해야 함.
- **실패 트레이스 → 골든 데이터셋 자동 피드백 루프**: 운영 환경 실패 trace를 자동 수집해 golden dataset으로 적립, 다음 배포 시 regression eval에 반영. 기존 Evals-as-CI(오프라인→pre-merge→온라인) 3점 라이프사이클에 "온라인 실패→오프라인 자동 환류" 경로를 추가하는 패턴.

## 출처

- [DSPy Framework Overview — thomas-wiegold.com](https://thomas-wiegold.com) *(개인 블로그, 개념 교차검증은 dspy.ai 원본으로 보완)*
- [Zero Trust for AI Agents — cdata.com](https://cdata.com)
- [Continuous Feedback Observability Loops — galtea.ai](https://galtea.ai)

> **폐기 항목**: Context Engineering(위키 중복) · Trajectory 평가(위키+프로필 중복) · Sandwich Pattern(Bento-Box 중복) · GPU-Native/Multimodal Lakehouse(미검증 출처 + 역할 무관)

## 위키화 후보

- `dspy-automated-prompt-optimization.md` — DSPy 개념·작동 원리·테스트 활용법 1페이지 노트
- `ephemeral-credentials-agent-security.md` — 에이전트 임시 자격 증명 패턴 + 취약점 테스트 체크리스트

## 프로필 반영 후보 (저위험)

- **DSPy**: 테스트 프롬프트 자동 최적화 도구로 테스트 레퍼토리에 추가
- **실패 트레이스 → 골든 데이터셋 자동 환류**: Evals-as-CI 3점 라이프사이클에 "온라인 실패 자동 적립" 경로 보완 인사이트로 추가

## 승인 필요 (고위험)

- **Ephemeral Credentials 게이트 도입**: autobots 에이전트 도구 호출 시 영구 토큰 대신 단기 자격 증명 발급 방식으로 전환 — 백엔드 인증 구조 변경 수반, 아키텍처 결정 후 착수 필요

## 신규 도구 후보 (에이전트/스킬)

- `[skill] dspy-prompt-optimizer` — 기존 테스트 케이스 생성 프롬프트를 DSPy로 자동 최적화해 수동 반복 감소
