---
title: 빅데이터 분석 파이프라인
type: concept
tags: [bigdata, data-engineering, ETL, pipeline, elasticsearch, python]
created: 2026-06-13
updated: 2026-06-13
sources: [2026-06-13-bigdata-pipeline-gisulnote]
summary: "데이터 수집·정제·저장·분석 후 API 제공까지의 ETL 파이프라인 아키텍처, 분석 기법(상관관계·군집·연관규칙), 소규모 구축 예시(ELK+Python)."
---

## 정의

데이터 소스에서 원시 데이터를 수집하여 분석 모델로 가공하고, 그 결과를 서비스 API로 제공하기까지의 전체 흐름. 서비스 규모에 따라 대형(데이터 레이크 + 웨어하우스 분리) 또는 소규모(ELK + Python + FastAPI) 형태로 구축한다.

## 5단계 흐름

```
데이터 소스 → 수집·정제 → 저장 → 분석 → API 제공
```

| 단계 | 역할 | 소규모 도구 |
|------|------|------------|
| 데이터 소스 | 시스템 로그, DB, IoT, 결제 데이터 | 자체 서비스 로그 |
| 수집·정제 | 불필요·누락 데이터 제거 (전처리) | Filebeat + Logstash |
| 저장 | 원시: 데이터 레이크 / 변환: 웨어하우스 | Elasticsearch |
| 분석 | 알고리즘 선택 → 모델 학습 → 반복 검증 | Python |
| API 제공 | 모델을 REST API로 서비스 연동 | FastAPI / Flask |

## ETL

**Extract(추출) → Transform(변환) → Load(적재)**의 약자. 데이터를 원본에서 꺼내 목적에 맞게 변환한 뒤 저장소에 쌓는 과정 전체.

## 주요 분석 기법

**상관관계 분석**: 두 변수의 관계 강도 측정.
예) 기온↑ → 아이스 아메리카노 판매↑, 기저귀 + 맥주 동시 구매 패턴

**군집 분석**: 유사 데이터를 그룹화해 정상/이상 패턴 구분.
예) 시스템 로그에서 새로운 패턴 등장 시 알람

**연관 규칙 분석(Market Basket Analysis)**: 함께 발생하는 항목 발견.
예) 장바구니 분석 → 진열 배치·번들 상품 기획

## 피처(Feature) 선택

알고리즘에 입력할 변수(특징)를 결정하는 과정. 피처 선택과 알고리즘 선택이 분석 품질을 결정하는 두 핵심 변수. 반복 테스트로 최적 조합을 찾는다.

## 주요 활용처

- **수요 예측**: 재고·물류 최적화 (소규모: 편의점 요일별 발주량)
- **개인화 추천**: 체류 시간·전환율 향상 (YouTube 오른쪽 추천 영상)
- **장애 예측**: 이상 패턴 감지 → 선제 대응

## 데이터 소스 품질

결제 데이터 > 체류 시간 > 클릭 로그 순으로 신뢰도 높음. "가장 확실한 증거는 결제한 것"

## 소규모 구축 예시 (ELK + Python)

```
서비스 로그 파일
  → Filebeat (수집)
  → Logstash (정제)
  → Elasticsearch (저장·검색)
  → Python 분석 스크립트
  → FastAPI (API 서빙)
  → 서비스에서 API 호출
```

단일 Elasticsearch로 데이터 레이크 + 검색을 모두 처리 가능. 대형 서비스가 아니면 별도 데이터 레이크/웨어하우스 분리 불필요.

## 관련 개념

- [[wiki/concepts/context-intelligence|컨텍스트 인텔리전스]] — 에이전트가 데이터를 활용하는 상위 개념
- [[wiki/concepts/agentic-loop|에이전트 루프]] — 분석 결과를 에이전트가 반복 활용하는 패턴

## 관련 엔티티

- [[wiki/entities/gisulnote-alex|기술노트with 알렉]] — 이 개념을 소개한 채널

## 출처

- [[wiki/sources/2026-06-13-bigdata-pipeline-gisulnote]]
