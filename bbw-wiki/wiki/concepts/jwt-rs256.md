---
title: JWT RS256 인증 패턴
type: concept
tags: [auth, jwt, security, rs256, asymmetric]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-hnedu-auth-project]
summary: "인증 서버만 개인키를 보유하고 각 서비스는 공개키로 JWT 서명을 검증하는 RSA 2048 비대칭키 기반 인증 방식"
---

## 정의

비대칭키(RSA 2048)로 JWT를 서명하는 방식. 인증 서버만 개인키를 보유하고, 각 서비스는 공개키로 서명을 검증하기만 한다.

## HS256 vs RS256

```
HS256 (대칭키): 모든 서비스가 비밀키 공유
               → 키 유출 시 전체 시스템 위험
               → 서비스 수가 늘수록 키 관리 복잡

RS256 (비대칭키): auth 서버만 개인키 보유
                  ERP·CRM은 공개키로 서명 검증만 수행
                  → 공개키가 유출돼도 토큰 발급 불가
                  → 서비스 추가 시 공개키 배포 1회로 끝남
```

## hnedu-auth 적용 구조

```
hnedu-auth (개인키 보유)
    ↓ JWT 발급 (RS256 서명)
    ↓ GET /auth/public-key — 공개키 1회 배포
    ↓
ERP Web API (.NET)   ← 공개키로 서명 검증만
CRM FastAPI (Python) ← 공개키로 서명 검증만
```

## 보안 규칙

- `keys/private.pem` — `.gitignore` 필수, 절대 커밋 금지
- `keys/public.pem` — 각 서비스에 1회 배포 후 로컬 캐시
- Refresh Token — DB에 SHA-256 해시만 저장 (평문 저장 금지)
- 역할·상태 변경 시 해당 직원의 refresh_tokens 전체 revoke (재로그인 강제)

## 키 생성 명령어

```bash
openssl genrsa -out keys/private.pem 2048
openssl rsa -in keys/private.pem -pubout -out keys/public.pem
```

## 관련 개념

- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]]

## 관련 엔티티

- [[wiki/entities/hnedu-auth|hnedu-auth]] — 이 패턴의 구현체

## 출처

- [[wiki/sources/2026-06-05-hnedu-auth-project]]
