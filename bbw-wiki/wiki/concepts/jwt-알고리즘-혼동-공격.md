---
title: JWT 알고리즘 혼동 공격
type: concept
status: ai-curated
learned_by: roun
curated_at: 2026-06-20
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-20-roun-learning]]
summary: "공개키를 HS256 시크릿으로 위장하여 RS256 검증을 우회하는 JWT 알고리즘 혼동 공격"
---

# JWT 알고리즘 혼동 공격

## 핵심 정의

JWT 알고리즘 혼동 공격은 공격자가 JWKS(JSON Web Key Set)의 공개키를 탈취한 후, 이를 HMAC 시크릿으로 취급하도록 속여 토큰을 위조하는 취약점이다. RS256(비대칭) 검증을 기대하는 서버가 HS256(대칭) 알고리즘으로 서명된 토큰을 수락하게 되어 인증을 우회할 수 있다.

## 요점

- **공격 메커니즘**: 공격자가 토큰의 `alg` 헤더를 RS256에서 HS256으로 변조하고, JWKS에서 추출한 공개키(공개정보)를 HS256 시크릿으로 사용해 토큰을 재서명. 서버가 알고리즘 검증 없이 이를 수락함.

- **보안 영향**: CVE-2026-22817(Hono, CVSS 8.2) 등 활성 취약점으로, 인증 우회를 통한 권한 상승, 민감 데이터 접근 가능.

- **방어 방법**: `verify()` 호출 시 `algorithms: ['RS256']` 등 허용 알고리즘을 명시적으로 화이트리스팅하고, 토큰의 `alg` 헤더 값을 신뢰하지 않을 것.

- **근본 원인**: 라이브러리가 기본값으로 "alg 헤더 따르기"를 사용하면 공격에 취약. 서버가 사전에 결정한 알고리즘만 허용해야 함.

## 출처

- [JWT Algorithm Confusion Attacks: CVE-2026-22817 Fix Guide](https://dev.to/iamdevbox/jwt-algorithm-confusion-attacks-cve-2026-22817-cve-2026-27804-and-cve-2026-23552-fix-guide-4ac4)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-20-roun-learning]]. 사람 검증 후 status를 verified로 변경하세요.
