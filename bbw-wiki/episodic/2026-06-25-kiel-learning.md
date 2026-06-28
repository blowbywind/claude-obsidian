---
date: 2026-06-25
bot: kiel
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 키엘 자가학습 — 2026-06-25

## 오늘 배운 것
- **OWASP 에이전틱 애플리케이션 보안 표준(OWASP ASI Top 10)**: 목표 하이재킹(ASI01), 도구 오용(ASI02), 메모리 오염(ASI06) 등에 대응하기 위한 툴 호출 레이어 보안 사양 기획 지침.
- **NIST AI Agent Standards Initiative 및 Zero Trust for Agents**: 권한 상승 제어와 식별 관리를 포함하여 정적 API 키 대신 동적 증명(dynamic attestation)을 적용하는 보안 아키텍처 설계법.
- **AEO(AI 답변 엔진 최적화) 경쟁 분석 및 모니터링 도구 활용**: HubSpot AEO Grader, xSeek, Profound, AthenaHQ 등을 활용하여 브랜드 인용 비율 및 AI 노출 품질을 추적하는 방법론.
- **A2A(Agent-to-Agent) 1.0 프로토콜 기반 에이전트 카드 표준화**: 서로 다른 에이전트 간 협업 시 역할과 API 사양을 명시하는 에이전트 카드 규격을 설계에 반영.
- **EU AI 법(EU AI Act) 고위험 에이전트 준수 요건**: 2026년 8월 시행 예정인 규제에 맞춰 기획 단계에서 작동 기록(audit trails), 설명 가능성, 이상 동작 조기 감지 요구사항 명시.

## 출처
- [OWASP GenAI Security Project](https://owasp.org)
- [NIST Center for AI Standards and Innovation](https://www.nist.gov)
- [Strata Identity Maverics Agentic Identity Platform](https://www.strata.io)
- [xSeek AI Visibility and Brand Monitoring Platform](https://xseek.io)
- [HubSpot AEO Grader Diagnostic Tool](https://www.hubspot.com)
- [A2A Protocol Open Standard](https://a2a-protocol.org)
- [Neuraltrust AI Safety and Compliance Framework](https://www.neuraltrust.ai)

## 위키화 후보
- `wiki/concepts/owasp-asi-top10.md` — 에이전틱 애플리케이션 고유 보안 취약점(ASI01~ASI10) 및 설계 지침 정의
- `wiki/concepts/aeo-evaluation-metrics.md` — AI 검색 엔진 내 브랜드 노출 품질, 감성, 멘션 비율을 평가하는 AEO 핵심 지표 정리

## 프로필 반영 후보 (저위험)
- `Zero Trust for Agents` — 에이전트의 권한 남용을 방지하는 dynamic least-privilege 보안 아키텍처 이해
- `Agent Cards` — A2A 1.0 프로토콜에서 에이전트의 권한 및 API 인터페이스를 명시하는 표준 데이터 모델 활용

## 승인 필요 (고위험)
- `PRD 에이전트 보안 및 규제 준수 섹션 의무화` — 에이전트 기획 시 OWASP ASI 대응 방안 및 EU AI Act 기준의 작동 기록(audit trails) 설계를 의무화하도록 PRD 템플릿 변경
- `AEO 경쟁 분석 프로세스 정규화` — 브랜드 경쟁 분석 체크리스트에 'AI 검색 결과 묘사 및 인용 빈도 확인(AEO Grader 활용)' 항목을 공식화

## 신규 도구 후보 (에이전트/스킬)
- `[skill] aeo-grader-integrator` — HubSpot AEO Grader 또는 xSeek API와 연동해 자사 제품의 AI 답변 노출 지표를 주기적으로 진단하고 비교 리포트를 작성하는 스킬
- `[agent] compliance-auditor` — 기획된 에이전트 스펙이 OWASP ASI Top 10 및 EU AI Act의 고위험군 규제 요건을 충족하는지 자동 검사하는 에이전트
