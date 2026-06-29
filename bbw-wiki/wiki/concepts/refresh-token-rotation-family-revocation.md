---
title: `Refresh Token Rotation & Family Revocation`
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-26
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-26-roun-learning]]
summary: "Refresh Token 재사용을 탈취 신호로 감지하여 해당 패밀리의 모든 활성 토큰을 즉시 무효화하는 RFC 9700 기반 자동 방어 메커니즘."
---

# `Refresh Token Rotation & Family Revocation`

제공된 자가학습 원문을 기반으로 `Refresh Token Rotation & Family Revocation` 노트를 작성합니다. 원문의 항목 7과 학습 내용 2번을 근거로 합니다.

---

## 핵심 정의

Refresh Token Family Revocation은 RFC 9700에서 정의한 토큰 탈취 감지 및 차단 메커니즘입니다. 이미 소비된 Refresh Token이 재사용되면 토큰 탈취로 간주하여, 해당 lineage(패밀리) 전체의 토큰을 즉시 만료시킵니다.

## 요점

1. **재사용 감지 메커니즘**: 같은 Refresh Token이 두 번 사용되는 것은 탈취의 신호입니다. 정상 흐름에서는 Token Rotation에 따라 새로운 토큰만 사용되므로, 이미 소비된 토큰의 재사용은 공격자의 개입을 의미합니다.

2. **패밀리 전체 만료**: Refresh Token은 발급→회전→폐기의 패밀리(lineage)로 추적됩니다. 재사용 감지 시 현재 토큰뿐만 아니라 해당 패밀리에 속한 모든 활성 토큰을 즉시 무효화하여 공격자의 추가 악용을 방지합니다.

3. **기존 Revoke 메커니즘과의 구분**: 비밀번호 리셋이나 MFA 변경 시 수동으로 전체 토큰을 revoke하는 것과 달리, Family Revocation은 자동으로 감지되어 능동적 방어가 가능합니다.

## 출처

- [RFC 9700 — OAuth 2.1 Security Best Current Practice](https://datatracker.ietf.org/doc/html/rfc9700)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-26-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
