---
title: Ponytail Skill 부분 흡수 (전체 플러그인 도입 비채택)
type: decision
status: accepted
owner: bbw
created: 2026-06-30
updated: 2026-06-30
accepted: 2026-06-30
tags: [claude-code, harness, skill, karpathy, over-engineering, ponytail]
---

# Ponytail Skill 부분 흡수

## 결정

DietrichGebert의 Ponytail Skill을 **플러그인으로 설치하지 않고**, 핵심 가치(오버엔지니어링 방지)만 기존 하네스에 흡수한다. 봇 4종(리안·해리·로운·아서) 전원 일치 판정.

| 항목 | 결정 | 반영 위치 |
|---|---|---|
| 6단계 의사결정 사다리 | ✅ 흡수 | `~/.claude/skills/karpathy-guidelines/SKILL.md` § Simplicity First |
| 오버엔지니어링 리뷰 항목 (`/ponytail-review`) | ✅ 흡수 | `~/.claude/commands/review.md` 신규 섹션 |
| 전역 감사 (`/ponytail-audit`) | ⚠️ 보류 | 선택형 — 필요 시 별도 커맨드로 추후 판단 |
| 강도 설정 (lite/full/ultra/off) | ❌ 제외 | 자연어 지시로 충분, 운영 복잡도 증가 (아서 반대) |
| 지표화 (`/ponytail-debt`·`/ponytail-gain`) | ❌ 제외 | 현 단계 실익 없음, 전원 반대 |

## 배경

- 원본 분석: `90-agent-logs/agy-artifacts/lian/2026-06-30__ponytail_skill_analysis.md`
- 철학("가장 좋은 코드는 작성하지 않은 코드")은 기존 karpathy-guidelines의 Simplicity First와 동일 방향 → 중복 플러그인 대신 보강이 합리적.

## 제약 (필수 준수)

- **안전 코드 축소 금지** (로운 명시): 단순화는 '해결책'에만 적용. 입력 검증·보안·예외 처리·인증/권한·접근성 등 요구사항상 필요한 안전망은 줄이지 않는다 — 두 파일 모두에 caveat로 명시함.
- 새 종속성 추가는 사다리 5단계에서 걸러도 **추가 시 사전 보고 필수**(글로벌 CLAUDE.md 정합).

## 검증

- 두 파일 YAML frontmatter 유효, 6단계 항목 수 일치, 안전 caveat 양쪽 존재, 제외 항목(강도/지표/audit) 미혼입 확인.
- 동명 `review` 스킬 부재 → 커맨드만 수정(동기화 불필요).

## 전역 감사(`/ponytail-audit`) — 현재 불필요 (2026-06-30 실측 판정)

"선택형 보류"를 코드베이스 증거로 재판정한 결과 **지금은 신설하지 않는다**.

| 근거 | 측정값 | 결론 |
|---|---|---|
| 찾아낼 부채/비대화 | TODO/FIXME/HACK **0개**, backend deps 7·frontend deps 12, 62파일/13.2k LOC | 감사 대상 자체가 없음 |
| 기존 커버리지 | `simplify`·`code-review`(`ultra`=브랜치 전체)·`harness-scan`·`/review`(오버엔지니어링 섹션)·`system-audit-2026-06-28` | 온디맨드로 이미 가능, 중복 |
| 비용/리스크 | 13.2k LOC 전역 read = 토큰 다소비 | token-optimization·feedback-529-reduce-load 원칙과 충돌 |
| 자기검증 | 6단계 사다리 1단계(YAGNI) 적용 | 커맨드 신설 자체가 오버엔지니어링 |

**재검토 트리거** (하나라도 충족 시 선택형 커맨드 신설 재평가):
1. 의존성이 ~30개 이상으로 증가
2. TODO/FIXME 등 부채 마커 누적
3. 대형 기능 추가로 코드 급증

그 전까지는 전역 점검이 필요하면 신규 커맨드 대신 기존 `code-review ultra` 또는 `simplify`를 해당 범위에 실행한다.
