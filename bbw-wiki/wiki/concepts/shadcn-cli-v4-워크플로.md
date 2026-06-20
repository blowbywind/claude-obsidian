---
title: shadcn CLI v4 워크플로
type: concept
status: ai-curated
learned_by: arthur
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-arthur-learning]]
---

# shadcn CLI v4 워크플로

## 핵심 정의

shadcn CLI v4(2026-03)는 컴포넌트 추가 시 변경 사항을 사전에 검증하고, 디자인 시스템 설정을 단일 문자열로 관리하는 워크플로를 제공한다.

## 핵심 요점

1. **검수 플래그**: `--dry-run`(변경 사항 시뮬레이션), `--diff`(레지스트리 변경 비교), `--view`(페이로드 검사) 플래그로 컴포넌트 추가 전 무분별한 덮어쓰기 방지.

2. **Presets**: 색상·테마·아이콘·폰트·radius 등 디자인 시스템 전체 설정을 단일 문자열로 패키징해 재사용 가능하게 구성.

3. **권장 워크플로**: 컴포넌트 추가 시 `--dry-run`/`--diff`로 변경 사항 사전 검수 후 적용하여 팀 내 디자인 시스템 일관성 유지.

## 출처

- https://medium.com/@nakranirakesh/shadcn-ui-march-2026-update-cli-v4-ai-agent-skills-and-design-system-presets-d30cf200b0e9
- https://ui.shadcn.com/docs/changelog/2026-03-cli-v4

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-arthur-learning]]. 사람 검증 후 status를 verified로 변경하세요.
