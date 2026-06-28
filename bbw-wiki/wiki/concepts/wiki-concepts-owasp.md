---
title: `wiki/concepts/owasp
type: concept
status: ai-curated
learned_by: kiel
curated_at: 2026-06-25
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-25-kiel-learning]]
---

# `wiki/concepts/owasp

요청하신 내용에 따라 **OWASP 개념 노트의 본문**을 작성했습니다. frontmatter와 h1을 제외한 순수 마크다운 본문입니다:

---

## 핵심 정의

OWASP(Open Web Application Security Project)는 웹 애플리케이션 보안을 위한 표준, 가이드라인, 도구를 제공하는 비영리 조직입니다. 전통적인 웹앱 보안부터 최근의 생성형 AI 및 에이전트 시스템 보안까지 확대되고 있습니다.

## 주요 요점

### 1. 전통적 웹 애플리케이션 보안
OWASP Top 10은 웹 애플리케이션의 가장 심각한 보안 취약점 목록으로, 업계 표준 위험 평가 기준입니다.

### 2. GenAI 에이전트 보안 (ASI Top 10)
**OWASP Agentic Application Security Initiative (ASI)**는 AI 에이전트 고유의 보안 위협에 대응합니다. 목표 하이재킹(ASI01), 도구 오용(ASI02), 메모리 오염(ASI06) 등 툴 호출 레이어의 보안 사양을 정의하며, 에이전트 기획 단계에서 이러한 취약점에 대한 설계 지침을 제시합니다.

### 3. 에이전트 권한 및 규제
에이전트의 권한 남용 방지를 위한 Zero Trust 아키텍처, 동적 증명(dynamic attestation)을 기반으로 한 보안 설계가 권고됩니다. 또한 2026년 8월 시행 예정인 EU AI Act 준수 요건에 맞춘 감사 추적(audit trails), 설명 가능성, 이상 동작 조기 감지가 필수화됩니다.

## 출처
- https://owasp.org
- https://www.nist.gov

---

**특징**:
- ✅ 한국어 본문 (~420자)
- ✅ 핵심 정의 → 요점 3개 → 출처 구조
- ✅ 자가학습 원문 내용만 활용
- ✅ OWASP 전통 보안 + ASI(에이전트) 신규 동향 포함

`wiki/concepts/owasp.md` 파일 생성 시 위 본문을 사용하면 됩니다.

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-25-kiel-learning]]. 사람 검증 후 status를 verified로 변경하세요.
