---
title: Microsoft Agent Framework 1.0
type: concept
status: ai-curated
learned_by: snow
curated_at: 2026-06-21
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-snow-learning]]
summary: "AutoGen과 Semantic Kernel을 통합한 엔터프라이즈급 멀티에이전트 오케스트레이션 프레임워크, 2026년 4월 출시, .NET과 Python에서 동일 API와 이중 오케스트레이션 지원."
---

# Microsoft Agent Framework 1.0

## 핵심 정의

Microsoft Agent Framework 1.0(2026년 4월 정식 출시)은 **AutoGen과 Semantic Kernel을 통합한 엔터프라이즈급 멀티에이전트 오케스트레이션 프레임워크**이다. .NET과 Python에서 동일한 API를 제공하며, 두 선행 프레임워크는 유지보수 모드로 전환됐다.

## 핵심 특성

**1. 이중 오케스트레이션 지원**
LLM 기반 동적 라우팅과 결정론적 워크플로 오케스트레이션을 하나의 시스템에서 모두 지원한다. 실무 모범 사례는 결정론적 흐름을 기본으로 하고, 진정으로 가변적인 결정 지점에만 동적 라우팅을 한정하는 하이브리드 접근이다.

**2. 언어 호환성**
.NET(C#) 및 Python 개발자가 동일한 API 및 패러다임으로 에이전트 설계를 할 수 있다. 이는 기존 AutoGen이나 Semantic Kernel 기반 코드의 마이그레이션 경로를 단순화한다.

**3. 프로덕션 준비 상태**
AutoGen의 오케스트레이션 설계와 참조 구현을 직접 참고해야 했던 과거와 달리, MAF 문서와 API가 엔터프라이즈 표준이 된다.

## 출처

- [Visual Studio Magazine: Microsoft Agent Framework 1.0](https://visualstudiomagazine.com/articles/2026/04/06/microsoft-ships-production-ready-agent-framework-1-0-for-net-and-python.aspx)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-snow-learning]]. 사람 검증 후 status를 verified로 변경하세요.
