---
title: RFC 9700 OAuth 보안 체크리스트
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-28
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-28-roun-learning]]
---

# RFC 9700 OAuth 보안 체크리스트

다음 본문을 Obsidian 위키 concept 노트로 작성합니다.

---

## RFC 9700 OAuth 보안 체크리스트

**핵심 정의**  
RFC 9700은 IETF가 발행한 OAuth 2.0 보안 모범 사례(Security Best Current Practice)입니다. 기존 OAuth 2.0 스펙의 취약점을 보완하고, 인가 서버·클라이언트 양쪽의 구현 기준을 정의합니다.

**주요 요점**

1. **금지된 플로우 — Implicit·ROPC**
   - 퍼블릭 클라이언트(브라우저, 모바일 앱)는 Implicit Grant, Resource Owner Password Credentials(ROPC) 플로우 사용 금지
   - 대신 Authorization Code with PKCE 사용 필수

2. **토큰 보호 — DPoP 또는 Rotation**
   - 액세스 토큰은 탈취 대비로 Sender-Constrained Token(DPoP) 또는 Refresh Token Rotation 중 하나 이상 필수 적용
   - 토큰 라이프타임 단축(15분 이하 권장)

3. **리다이렉션 URI 완전 일치**
   - 인가 서버는 와일드카드·정규식 패턴 허용 금지
   - 사전 등록된 값과 **정확히 일치**하는 URI만 검증 허용
   - 오픈 리다이렉터 취약점 차단

4. **상태 매개변수(state) 검증**
   - 클라이언트는 모든 인가 요청에 암호화 강한 난수 state 포함 필수
   - 응답 후 state 값 검증으로 CSRF 공격 방지

**출처**  
- [RFC 9700 — OAuth 2.0 Security Best Current Practice](https://datatracker.ietf.org/doc/html/rfc9700)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-28-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
