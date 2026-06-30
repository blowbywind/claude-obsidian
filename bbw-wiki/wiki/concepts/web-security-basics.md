---
title: 웹 보안 기초
type: concept
tags: [security, owasp, web-security, csp, https, injection, xss, authentication]
created: 2026-06-13
updated: 2026-06-13
sources: [2026-06-13-vibe-coding-security-gisulnote]
summary: "웹 서비스의 네트워크·서버·DB·소스코드 4구간 보안 대책과 OWASP Top 10 취약점 기준, 실무 점검 워크플로우를 다룬 가이드."
---

## 정의

웹 서비스를 외부 공격으로부터 보호하기 위한 기술·관행의 집합. 네트워크·서버·DB·소스 코드 4개 구간으로 나눠 점검한다.

## 보안 구간 4가지

| 구간 | 핵심 위협 | 주요 대책 |
|------|----------|---------|
| **네트워크** | 데이터 스누핑(도청) | HTTPS(TLS) 적용 |
| **서버** | 취약점 악용, 무단 접근 | 보안 패치, 방화벽, 포트 제한 |
| **DB** | 평문 데이터 탈취 | 패스워드 해싱(bcrypt 등), 개인정보 암호화 |
| **소스 코드** | XSS, 인젝션, 인증 우회 | OWASP Top 10 기준 점검 |

> PaaS 배포(Vercel·Cloudflare 등)는 네트워크·서버 보안을 플랫폼이 담당.
> **소스 코드 취약점은 개발자 책임** — 바이브코딩 시 특히 주의.

## OWASP Top 10

[OWASP](https://owasp.org) (Open Web Application Security Project)가 매년 발표하는 웹 보안 10대 취약점.

| # | 취약점 | 실례 |
|---|--------|------|
| 1 | **접근 제어 실패** | 타인의 계정 데이터 조회 가능한 API |
| 2 | **암호화 실패** | 패스워드 평문 저장, MD5 사용 |
| 3 | **인젝션** | SQL 인젝션, 명령어 인젝션 |
| 4 | **인시큐어 디자인** | 인증 없는 관리자 기능 |
| 5 | **보안 설정 오류** | 기본 비밀번호 유지, 디버그 모드 노출 |
| 6 | **취약한 컴포넌트** | 구버전 라이브러리, 백도어 패키지 |
| 7 | **인증 실패** | 세션 고정 공격, 토큰 탈취 |
| 8 | **무결성 오류** | CI/CD 파이프라인 주입 |
| 9 | **보안 로깅 부족** | 침해 탐지 불가 |
| 10 | **정보 노출** | 에러 메시지에 스택 트레이스, 설정 파일 노출 |

## 자주 놓치는 항목

**CSP(Content Security Policy) 헤더**:
- XSS 공격 방어의 핵심 HTTP 헤더
- 누락 시 악성 스크립트 삽입 허용
- Nginx/Caddy 설정에서 추가 가능:
  ```
  Content-Security-Policy: default-src 'self'
  ```

**패스워드 평문 저장**:
- AI가 생성한 코드에서 가장 흔히 발생하는 DB 보안 문제
- 반드시 bcrypt / argon2 등으로 해싱 후 저장

## 바이브코더 보안 점검 워크플로우

```
1. URL 보안 스캔 도구로 배포된 서비스 점검
       ↓
2. 위험·경고 항목 목록 확인
       ↓
3. AI에 "OWASP [항목명] 취약점을 내 코드에서 찾아 보완해줘" 요청
       ↓
4. 수정 후 재배포 → 재스캔으로 확인
```

**핵심**: 막연히 "보안 점검해줘"보다 **OWASP 항목명을 명시**해야 AI가 정확히 수정한다.

## 관련 개념

- [[wiki/concepts/network-infra|네트워크 & 인프라 구성]] — 네트워크 보안(HTTPS·방화벽) 기반
- [[wiki/concepts/service-dev-lifecycle|서비스 개발 라이프사이클]] — 테스트 단계에 보안 점검 포함
- [[wiki/concepts/jwt-rs256|JWT RS256 인증 패턴]] — 인증 실패(#7) 방어 구현 예시

## 관련 엔티티

- [[wiki/entities/gisulnote-alex|기술노트with 알렉]] — 이 개념을 소개한 채널

## 출처

- [[wiki/sources/2026-06-13-vibe-coding-security-gisulnote]]
