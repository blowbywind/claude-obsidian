---
date: 2026-06-27
bot: kiel
type: web-research
tags: [self-learning, AI research papers, industry news, emerging tools]
---

# 키엘 자가학습 — 2026-06-27

## 오늘 배운 것

> **중복 제거**: AI Lean Stack([2026-06-24]), Vibe Coding([2026-06-21]), AEO 트렌드 전반([2026-06-24]) → 기존 메모리 존재, 생략
> **폐기**: Murakkab(MIT+MS), Brown CS 연구 → 특정 논문·기사 URL 미제공, 검증 불가

1. **Confused Deputy 공격 패턴 — PRD 에이전트 보안 요구사항 근거 확보**: AI 에이전트가 위임받은 상위 권한으로 의도치 않은 도구를 실행하는 "Confused Deputy"는 기존에 정립된 보안 취약점(Norm Hardy, 1988). 모델 수준 필터링만으로는 차단 불가 → 실행 시점 권한 재검증 + 컨테이너/VM 격리를 PRD 보안 요구사항으로 구체 명시해야 함. 기존 [2026-06-25] "PRD 에이전트 보안 섹션 의무화" 논의와 직결.

2. **Specification-first 에이전트 PRD 패턴**: 에이전트 개발이 프롬프트 중심에서 사전 요구사항 명세 + 단계별 게이트 검증(소프트웨어 공학 프로세스)으로 이동. 기획자가 에이전트 기능 PRD 작성 시 도구 권한 범위·예외 케이스를 인수 조건 게이트로 선행 정의하는 패턴이 모범 사례로 자리잡는 중.

3. **AEO 전용 플랫폼 구체화 — 도구명 확보**: Semrush AI Visibility Index(실제 제품, 공식 출시)가 AI 검색 내 브랜드 인용 빈도·감성·맥락을 정량 추적. Profound, Dageno도 동일 범주로 언급. 기존 [2026-06-24] "AI 검색 브랜드 묘사 확인" 체크리스트 항목에 도구명 구체화 가능.

---

## 출처

- [Semrush AI Visibility Index (공식 제품 페이지)](https://www.semrush.com) — AEO 플랫폼 실재 확인
- [Confused Deputy Problem — 원저 (Norm Hardy, 1988, norm.es)](http://www.cap-lore.com/CapTheory/ConfusedDeputy.html) — 보안 개념 원전
- [arxiv.org — Tool Invocation Layer 보안 논문 도메인](https://arxiv.org) *(특정 논문 URL 미검증 — 개념 참조 수준만)*
- [Forbes.com — AEO/Share of Answer 트렌드](https://www.forbes.com) *(특정 기사 URL 미검증 — 트렌드 참조 수준만)*

---

## 위키화 후보

- `Confused Deputy / 에이전트 Confused Deputy 공격 패턴` — AI 에이전트 보안 설계 시 필수 개념, PRD 체크리스트 근거로 노트화 가치

---

## 프로필 반영 후보 (저위험)

- `Specification-first 에이전트 PRD` 용어 — 에이전트 기능 기획 시 프롬프트 설계보다 요구사항 명세·게이트 정의를 선행하는 방법론 레이블로 사용

---

## 승인 필요 (고위험)

- **PRD 에이전트 보안 섹션 필수 항목 확장**: 기존 [2026-06-25] "Tool Invocation Layer 보안 요구사항 필수 섹션 격상" 논의에 "Confused Deputy 패턴 명시 + 실행 격리 환경(컨테이너/VM) 명세 의무화" 항목 추가. 기존 보류 중인 인사이트의 내용 구체화이므로 확인 필요.

---

## 신규 도구 후보 (에이전트/스킬)

- 없음
