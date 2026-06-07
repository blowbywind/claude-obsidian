---
title: Cowork
type: entity
tags: [product, ai, tool]
created: 2026-06-05
updated: 2026-06-07
sources: [2026-06-05-claude-code-7steps-mastery, 2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]
---

## 개요

Claude 데스크탑 앱의 세 가지 모드 중 하나(중간 모드). 로컬 폴더를 Claude에 연결하여 파일 읽기·수정·생성을 가능하게 한다.

Nick Milo는 Cowork를 AI OS의 Layer 3(외부 AI 도구)로 사용한다. Claude가 사라지면 언제든 다른 AI로 교체 가능한 레이어.

## 주요 기능

- 로컬 폴더 선택 → 허용(Allow) → Claude가 폴더 전체 접근
- 파일 읽기, 수정, 이동, 이름 변경, 새 파일 생성 가능
- 매 세션마다 문서 재업로드·컨텍스트 재설명 불필요

## 모델 선택 가이드 (Nick Milo)

| 모델 | 용도 |
|------|------|
| Sonnet | 대부분의 작업 (기본값, 토큰 효율적) |
| Opus | 복잡한 합성, 심층 리서치, 품질 우선 작업 |
| Haiku | Web Clipper 요약 등 초경량 작업만 |

## 데이터 정책 (Claude 선택 이유)

- 학습 데이터로 미사용 (비공개 노트·일기 연결 시 비협상 조건)
- 서버 보존: 롤링 30일 창

## Claude Code와의 관계

한국어 채널 콘텐츠 저자는 Claude Code 도입 후 Cowork 불사용 언급. 하지만 Nick Milo처럼 PKM 중심 워크플로우에서는 Cowork가 Obsidian 통합에 최적화된 선택이 될 수 있음.

## 주요 연결

- [[wiki/entities/claude-code|Claude Code]] — 기능적으로 대체 관계 (개발자 워크플로우)
- [[wiki/concepts/ai-os|AI OS]] — Cowork가 Layer 3 역할
- [[wiki/entities/nick-milo|Nick Milo]] — Cowork를 Obsidian PKM에 활용

## 출처

- [[wiki/sources/2026-06-05-claude-code-7steps-mastery]]
- [[wiki/sources/2026-06-07-obsidian-claude-cowork-ai-os-nick-milo]]
