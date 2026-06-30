---
title: `wrangler deploy
type: concept
status: ai-curated
learned_by: lian
curated_at: 2026-06-25
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-25-lian-learning]]
summary: "Cloudflare Workers 배포 CLI로, `--temporary` 플래그로 60분 임시 환경을 OAuth 없이 즉시 생성하여 AI 에이전트의 자동화 배포와 빠른 검증에 최적화."
---

# `wrangler deploy

자가학습 원문을 분석했습니다. "wrangler deploy"에 대한 Obsidian 위키 개념 노트 본문을 다음과 같이 작성하겠습니다:

---

**`wrangler deploy`는 Cloudflare의 공식 CLI 도구로 Workers 애플리케이션을 배포합니다.**

## 핵심 정의
Cloudflare Workers 프로젝트를 클라우드에 배포하는 커맨드라인 인터페이스입니다. 프로덕션 배포 외에도 `--temporary` 플래그를 통해 임시 환경 생성을 지원합니다.

## 주요 특징

### 1. 임시 배포 환경 (`--temporary`)
- 60분간 유효한 단기 배포 환경을 OAuth 인증 없이 즉시 생성
- AI 에이전트가 인증 제약 없이 인프라 테스트를 신속하게 수행 가능
- 신규 프레임워크 템플릿이나 새로운 도구의 동작 여부를 빠르게 검증하는 용도

### 2. 에이전트 친화 설계
- 자동화된 배포 워크플로우 구축에 최적화
- CLI 기반으로 자동 배포 및 검증 파이프라인 통합 용이

### 3. 임시 계정 시스템
- Temporary Accounts를 통해 단기간 인프라 리소스에 접근 가능
- 배포 후 자동으로 정리되어 관리 오버헤드 최소화

## 출처
- [Cloudflare - Temporary Accounts for Agents](https://blog.cloudflare.com/temporary-accounts-for-agents/)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-25-lian-learning]]. 사람 검증 후 status를 verified로 변경하세요.
