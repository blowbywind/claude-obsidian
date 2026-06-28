---
date: 2026-06-25
bot: roun
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 로운 자가학습 — 2026-06-25

## 오늘 배운 것
- **Encore.ts 프레임워크**: TypeScript 및 Go 기반으로 백엔드 코드 내에서 데이터베이스, 큐, 크론 작업 등의 인프라를 정의하면 자동으로 클라우드에 IaC 프로비저닝을 수행하고 타입 안전한 API 생성을 지원하는 도구 (출처: https://encore.dev)
- **AWS Blocks 아키텍처**: AI 에이전트의 구성 오류를 방지하기 위해 가이드 파일(Steering Files)을 내장하고, 로컬 우선 개발 및 무수정 AWS 배포(CDK 기반)를 제공하는 TypeScript 백엔드 프레임워크 (출처: https://infoq.com)
- **Huma Go 프레임워크**: OpenAPI 3.1 명세를 Go 구조체에 선언적으로 바인딩하여 수동 Swagger 문서 작업 없이 API 명세와 비즈니스 로직을 동기화하는 Go 마이크로 프레임워크 (출처: https://dev.to)
- **객체 속성 수준 인가 실패(BOPLA)**: OWASP API Security Top 10 2023(API3:2023) 취약점으로, 권한이 없는 특정 데이터 필드를 노출(과도한 데이터 노출)하거나 수정(대량 할당)할 수 있는 API 설계 결함 (출처: https://aptori.com)
- **쉬프트-레프트(Shift-left) API 보안**: Pull Request 등 개발 초기 단계에서 API 스펙 스캔과 SAST/DAST/SCA 검증을 연계하여 BOLA 및 BOPLA 취약점을 선제 차단하는 거버넌스 전략 (출처: https://levo.ai)

## 출처
- [Encore.ts - Framework-Defined Infrastructure](https://encore.dev)
- [InfoQ - AWS Blocks for AI-assisted coding](https://infoq.com)
- [DEV Community - Huma Go Framework with OpenAPI 3.1](https://dev.to)
- [Aptori - Broken Object Property Level Authorization (BOPLA) Guide](https://aptori.com)
- [Levo.ai - Shift-left API Posture Governance](https://levo.ai)

## 위키화 후보
- `AWS Blocks`: AI 에이전트 협업을 위해 가이드라인(Steering Files)을 내장하고 로컬 우선 개발을 지원하는 AWS의 TypeScript 백엔드 프레임워크
- `BOPLA (Broken Object Property Level Authorization)`: API 객체의 내부 속성 필드 수준에서 발생하는 비인가 읽기 및 쓰기 취약점

## 프로필 반영 후보 (저위험)
- **AWS Blocks**: AI-assisted 백엔드 개발 시 아키텍처 규칙 준수를 위한 블록 기반 프레임워크 활용 기법
- **BOPLA 방어 설계**: 데이터 전송 객체(DTO) 도입 및 화이트리스트 기반 속성 매핑을 통한 API 필드 수준 인가 검증 설계

## 승인 필요 (고위험)


## 신규 도구 후보 (에이전트/스킬)
- `[agent] AWS-Blocks-Developer` — 가이드 파일(Steering Files) 규칙을 준수하여 AWS Blocks 기반 API와 CDK 인프라를 자동으로 설계하고 안전하게 배포하는 에이전트
- `[skill] API-BOPLA-Scanner` — API 엔티티 바인딩 패턴을 분석하여 과도한 데이터 노출 및 대량 할당 취약점을 식별하고 DTO 보호 코드를 생성하는 스킬
