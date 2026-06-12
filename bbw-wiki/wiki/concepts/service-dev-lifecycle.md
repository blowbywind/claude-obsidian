---
title: 서비스 개발 라이프사이클
type: concept
tags: [software-development, mvp, api-design, deployment, git, cloud, lifecycle]
created: 2026-06-13
updated: 2026-06-13
sources: [2026-06-13-service-dev-lifecycle-gisulnote]
---

## 정의

서비스(웹/앱) 하나가 아이디어에서 출시·운영까지 거치는 전체 단계. 기획 → 설계 → 개발 → 테스트 → 배포 → 출시 → 운영의 7단계로 구성.

## 전체 흐름

```
[기획] MVP 정의 + 타겟 유저 + 차별화 전략
  ↓
[설계] 화면 설계 + 데이터 설계(ERD) + API 설계
  ↓
[개발] 프론트엔드 + 백엔드 + DB + 연동 + Git 관리
  ↓
[테스트] 단위·통합·성능·보안 테스트
  ↓
[배포] 빌드 → 클라우드 서버 업로드 → 도메인 + HTTPS
  ↓
[출시] 웹: 도메인 공개 / 앱: 스토어 등록·심사
  ↓
[운영] 장애 대응 + 기능 추가 + 수익화
```

## 1단계 — 기획

**MVP(Minimum Viable Product)**: 생존 가능한 최소 기능 버전.
- 카카오톡 MVP = 대화, 당근마켓 MVP = 중고 거래
- 기획의 핵심은 기능 추가가 아닌 **욕심 내려놓기**

**구성 요소**:
1. 아이디어 → 핵심 기능 1~3개 도출
2. 타겟 유저(페르소나) 구체화 — 구체적일수록 성공 가능성 높음
3. 경쟁 서비스 분석 → 차별화 포인트 정의
4. 수익화 모델 — **기획 단계부터 함께 고민** (나중에 붙이면 구조 전체가 흔들림)

## 2단계 — 설계

**화면 설계**: 사용자 흐름·시나리오 시각화 (사용자 유형별: 일반/어드민/비로그인)

**데이터 설계(ERD)**: 테이블 정의 + 관계 설계
```
회원 테이블: id, pw, email, address
상품 테이블: id, name, price, seller_id
결제 테이블: id, user_id, product_id, amount
```

**API 설계**: 기능 단위로 엔드포인트 정의
- 앱·웹 → DB 직접 접속 불가 → API 서버가 중간자
- 기능과 테이블이 API로 연결되는 구조

## 3단계 — 개발

**프론트엔드**:
- 웹: HTML + CSS + JS / 반응형 웹(PC↔모바일 자동 적응)
- 앱: Android / iOS 각각의 언어·프레임워크

**백엔드**:
- API 개발 (종류별: 회원·상품·결제 등)
- **CRUD**: Create / Read / Update / Delete — 데이터 처리의 기본 단위
- DB 구축: DBMS 설치(MySQL·MongoDB 등) → 테이블 생성 → SQL

**소스 관리 — Git 브랜치 전략**:
```
main(운영) ← merge ← dev(개발) ← feature/기능명
```
- 운영 브랜치 직접 수정 금지
- 개발 완료 + 테스트 통과 후 운영에 반영

**빌드**: 소스 코드 → 실행 가능한 형태 (JAR, 번들 등)

## 4단계 — 테스트

| 종류 | 목적 |
|------|------|
| 단위 테스트 | 개별 모듈 동작 검증 |
| 통합 테스트 | 컴포넌트 간 연동 검증 |
| 성능 테스트 | 부하 대응력 확인 |
| 보안 테스트 | 취약점 점검 |

## 5단계 — 배포

**클라우드 선택 기준**:
| 규모 | 도구 |
|------|------|
| 단순 프론트엔드 | Vercel, Cloudflare Pages |
| DB·API 복잡한 서비스 | AWS / Azure / GCP |

**배포 체크리스트**:
1. 빌드 결과물 → 서버 업로드 (deploy)
2. 서버 실행 (웹 포트: 80, WAS: 8080)
3. 도메인 구매 → 서버 IP에 연결
4. SSL 인증서 설치 → HTTPS 활성화 (필수)

## 6단계 — 출시

- **웹**: 도메인 연결 완료 시 공개
- **앱**: 앱스토어(iOS) / 구글 플레이(Android) 등록 → 심사 → 스토어 노출 (수일 소요)

> "출시가 끝이 아니라 시작이다"

## 7단계 — 운영

- 장애 대응 (즉각 복구)
- 기능 추가·개선 (Git 기반 지속적 배포)
- 데이터 분석 → 개선 방향 도출 → [[wiki/concepts/bigdata-pipeline|빅데이터 분석 파이프라인]]과 연결

## 관련 개념

- [[wiki/concepts/it-knowledge-map|IT 기술 지식 맵]] — 개발에 필요한 기술 전체 지도
- [[wiki/concepts/computer-architecture-os|컴퓨터 구조 & 운영체제]] — 서버·배포 기반 지식
- [[wiki/concepts/bigdata-pipeline|빅데이터 분석 파이프라인]] — 운영 단계 데이터 활용

## 관련 엔티티

- [[wiki/entities/gisulnote-alex|기술노트with 알렉]] — 이 개념을 소개한 채널

## 출처

- [[wiki/sources/2026-06-13-service-dev-lifecycle-gisulnote]]
