---
title: OAuth 2.1 리프레시 토큰 보안 (RFC 9700)
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-18-roun-learning]]
summary: "OAuth 2.1 리프레시 토큰 보안: 비밀번호·MFA 변경 시 자동 무효화·rotation 필수·7~30일 만료(RFC 9700)."
---

# OAuth 2.1 리프레시 토큰 보안 (RFC 9700)

Obsidian 위키 큐레이터 모드로 concept 노트 본문을 작성하겠습니다.

---

## 핵심 정의

OAuth 2.1에서 규정하는 리프레시 토큰(Refresh Token)은 access token 만료 후 새 access token을 얻기 위한 자격증명이다. RFC 9700(2025년 1월)에서는 PKCE 필수화, Implicit Grant 폐기 등과 함께 리프레시 토큰의 보안 취약점을 강조했다.

## 주요 특성

**1. 비밀번호 리셋·MFA 변경 시 자동 무효화 부재**
리프레시 토큰은 발급 후 사용자의 비밀번호나 다중 인증 설정 변경 시 자동으로 무효화되지 않는다. 이는 토큰 탈취 시 공격자가 장기간 정상 사용자처럼 접근할 수 있는 구멍을 만든다(2025년 초 Salesloft 사고: 700개 조직 피해). 따라서 이 이벤트 발생 시 해당 사용자의 모든 refresh token을 강제 revoke하는 로직이 필수다.

**2. 권장 만료 기간**
- Access token: 5~15분
- Refresh token: 7~30일

**3. Refresh Token Rotation**
토큰 탈취 감지의 어려움. 공격자가 토큰을 사용할 때 서비스는 정상 요청으로 인식해 감지 시간이 길어질 수 있다. 따라서 모니터링과 강제 무효화 기준 수립이 중요하다.

## 출처

- [OAuth Security Best Practices 2025 | InboxAgents](https://inboxagents.ai/blog/oauth-security-best-practices)
- [Refresh Token Security Best Practices | Obsidian Security](https://www.obsidiansecurity.com/blog/refresh-token-security-best-practices)
- [Refresh Token Rotation Explained | LoginRadius](https://www.loginradius.com/blog/identity/secure-refresh-token-rotation)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-18-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
