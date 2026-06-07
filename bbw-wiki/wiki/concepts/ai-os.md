---
title: AI OS (AI 운영체제)
type: concept
tags: [ai, pkm, architecture, obsidian]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]
---

## 정의

개인 지식·워크플로우를 AI와 연결하는 3레이어 아키텍처. Nick Milo가 제안한 프레임워크로, 특정 AI 도구에 종속되지 않는 **이식 가능한 AI 시스템**을 목표로 한다.

## 3레이어 구조

```
[Layer 3] 외부 AI 도구 (Claude Cowork, Codex, Gemini 등)
              ↕  번역·중개
[Layer 2] Maps & Manuals (ME.MD · Vault Map · Skill Map)
              ↕  저장·탐색
[Layer 1] Ideaverse (Obsidian 로컬 마크다운 볼트)
```

### Layer 1 — Ideaverse (내 생각)
- Obsidian 볼트 = 로컬 마크다운 파일 폴더
- ACE 구조: **Atlas**(지식·아이디어) / **Calendar**(날짜 기반 노트) / **Efforts**(프로젝트·할 일)
- AI가 생성한 콘텐츠와 내 원본 생각을 명확히 분리 → `AIOS/` 폴더에 AI 콘텐츠 격리

### Layer 2 — 번역층 (Maps & Manuals)
AI OS의 핵심. Obsidian과 외부 AI 사이의 다리. 3대 파일:

| 파일 | 역할 |
|------|------|
| `ME.MD` | 내가 누구인지, 어떻게 생각하는지, AI와 협업 방식 정의 — AI-agnostic |
| `Vault Map` | 볼트 전체 TOC+매뉴얼. AI가 지도 없이 탐색하면 정확도 급락 |
| `Skill Map` | 어떤 스킬이 있고 언제 써야 하는지 목록 |

### Layer 3 — 외부 AI 도구
- 현재: Claude Cowork (Claude 데스크탑 앱의 파일 접근 모드)
- 언제든 교체 가능: Claude → Codex → 오픈소스 로컬 모델
- 교체해도 Layer 1·2는 그대로 유지됨

## 핵심 원칙

- **파일이 여행한다**: 내 노트·스킬·AI 코어 문서는 로컬에, AI는 렌터카처럼 교체
- **스킬은 로컬에**: AI 도구 내부(Claude Projects 등)가 아닌 Obsidian에 스킬 저장
- **세션 시작 프롬프트**: AI는 기억상실이 있으므로 매 세션마다 ME.MD·Vault Map·Skill Map 읽기 명시 지시 필요

## 관련 개념

- [[wiki/concepts/me-md|ME.MD]] — Layer 2의 핵심 파일
- [[wiki/concepts/vault-map|Vault Map & Skill Map]] — Layer 2 나머지 파일들
- [[wiki/concepts/ace-folder-framework|ACE 폴더 프레임워크]] — Layer 1 구조화 방법
- [[wiki/concepts/세컨드 브레인|세컨드 브레인]] — 상위 철학적 개념
- [[wiki/concepts/claude-md|CLAUDE.md]] — Claude 전용 Layer 2 파일 (AI-agnostic 아님)

## 관련 엔티티

- [[wiki/entities/nick-milo|Nick Milo]] — 프레임워크 창시자
- [[wiki/entities/obsidian|Obsidian]] — Layer 1 호스팅 앱
- [[wiki/entities/cowork|Cowork]] — Layer 3 현재 AI 도구

## 출처

- [[wiki/sources/2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]]
