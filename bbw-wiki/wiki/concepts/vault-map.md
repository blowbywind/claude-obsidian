---
title: Vault Map & Skill Map
type: concept
tags: [ai, obsidian, pkm, context, navigation]
created: 2026-06-07
updated: 2026-06-07
sources: [2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]
---

## 정의

AI OS 번역층(Layer 2)의 두 번째·세 번째 핵심 파일. AI가 Obsidian 볼트를 정확하게 탐색하고 올바른 스킬을 선택하도록 안내한다.

## Vault Map

**"AI는 내 볼트를 어떻게 탐색해야 하는가?"** 에 답하는 파일.

볼트 전체의 목차(TOC) + 매뉴얼. AI가:
- 관련 노트 또는 폴더를 빠르게 찾도록 안내
- 관련 없는 노트를 건너뛰어 컨텍스트 낭비 방지
- 노트를 대신 생성할 때 올바른 위치에 저장

**지도 없는 AI의 문제**: 17,000개 노트에 지도 없이 접근한 AI는 체리피킹·샘플링만 하고 전체를 검토한 척한다 → 부정확한 결과. 지도를 주면 관련 파일만 로드해 정밀하게 응답.

## Skill Map

**"어떤 스킬이 있고 언제 써야 하는가?"** 에 답하는 파일.

- 스킬 목록과 각 스킬의 역할, 트리거 조건 정의
- 스킬은 시스템 단위로 그룹화 (Daily Trident, Sherpa, Rock Tumbler 등)

### 핵심 원칙: 스킬은 로컬에 보관
- AI 도구(Claude Projects 등) 내부에 스킬을 저장하면 → AI 종속 발생
- Obsidian 안 `AIOS/skills/` 폴더에 저장 → 어떤 AI로 교체해도 스킬 유지
- AI는 스킬 *생성·검토* 에 써도 되지만, *보관* 은 반드시 로컬

## 실전 스킬 시스템 예시 (Nick Milo)

| 시스템 | 스킬 | 설명 |
|--------|------|------|
| Daily Trident | Daily Brief | 매일 06:00 자동 생성, Gmail+Calendar+ClickUp+Ideaverse 통합 |
| Daily Trident | Daily Log | 하루 중 인터스티셜 저널, 다음날 브리핑에 반영 |
| Sherpa | 주제 맵핑 | 새 주제 학습 가속 |
| Weekly Review | 주간 리뷰 | 누락 사항 점검 보조 렌즈 |
| Rock Tumbler | IDI 피드백 | Imagine·Discern·Integrate 오픈 질문으로 작업 피드백 |
| Chronicler | 대화 저장 | "save this verbatim" 명령으로 AI 대화 보존 |
| Janitor | 시스템 유지 | AI OS 자가 정비 |
| Courier | 팀 공유 | 개인 노트를 sanitize 후 팀 공간에 전달 |

## 관련 개념

- [[wiki/concepts/ai-os|AI OS]] — Vault Map과 Skill Map이 속한 Layer 2
- [[wiki/concepts/me-md|ME.MD]] — Layer 2의 첫 번째 파일
- [[wiki/concepts/claude-code-commands-skills|커맨드 & 스킬스]] — Claude Code에서의 스킬 개념과 유사

## 출처

- [[wiki/sources/2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]]
