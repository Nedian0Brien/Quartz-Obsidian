---
tags: ""
---
#데이터엔지니어링 
###### **E**xtract(추출) - **T**ransform(변환) - **L**oad(적재)
---
서로 다른 데이터 소스에서 데이터를 가져와 분석·저장·활용에 적합한 형태로 가공한 뒤 목적지 시스템(주로 [[데이터 웨어하우스]] 혹은 [[데이터 레이크]])에 저장하는 전체 파이프라인을 의미함

## ETL이란?
---
#### 1. Extract
- 목적
	다양한 데이터 소스에서 원천 데이터를 최대한 손실 없이 정확하게 가져오는 것을 목표로 함
	데이터는 조직 내외부의 여러 시스템에 흩어져 있으며, 각 소스는 서로 다른 형식, 구조, 접근 방식(파일, API, 데이터베이스 등)을 가짐

##### 대표적인 데이터 소스
- 관계형 데이터베이스(MySQL, PostgreSQL)
- NoSQL 데이터베이스(MongoDB, Cassandra)
- 로그 파일, CSV, JSON, Parquet 등 정형 · 반정형 파일
- 외부 API(예: SNS API, 공공데이터 API)
- 메세징 시스템([[Kafka]])
- SaaS 서비스(Google Analytics, Salesforce)

- [b] Extract 시 고려할 점
- 데이터 양이 많을 경우 <mark style="background: #FF5582A6;">incremental extract</mark>가 필요
- CDC(Change Data Capture)를 통한 변경분 추적
- 네트워크 지연, 데이터 불일치(Consistency) 문제
- 데이터 타입 변환 필요성

Extract는 단순히 "데이터를 가져오는 과정"이 아니라, <mark style="background: #FFB86CA6;">"손실과 왜곡 없이 안정적으로 가져오기 위한 전략을 설계하는 과정"</mark>임

#### 2. Transform
- 목적
	추출된 데이터를 분석, 저장, 모델링에 적합한 구조로 재가공하는 과정
	ETL의 핵심이며, 전체 데이터 품질을 결정함

##### 대표적인 변환 과정
- 정제(Cleaning)
	- 결측치 처리
	- 중복 제거
	- 이상치 검출
	- 형식 오류 수정
- 데이터 타입 변환
	- 문자열 -> 정수, 문자열 -> 날짜 등
- 표준화(Nomalization)
	- 동일 표현을 하나로 통합(ex: "KR", "Korea", "South Korea" -> "Korea")
- 조인(Join)
	- 여러 테이블 연결
- 집계(Aggregation)
	- 일별 매출 합계, 사용자 세션당 평균 시간 등
- 파생 변수 생성
	- 도메인 로직을 이용한 새로운 feature 생성
- 비즈니스 규칙 반영
	- 회사 내 KPI 정의에 맞춘 지표 계산

Transform은 단순한 데이터 변환을 넘어 "의미를 만드는 과정"임.
추출 단계의 원시 데이터(raw data)는 대부분 분석에 적합하지 않은 형태이며, <mark style="background: #FFB86CA6;">Transform 단계에서 도메인 지식과 비즈니스 로직이 개입되면서 데이터가 비로소 조직에 유용한 형태로 재탄생</mark>

#### 3. Load
- 목적
	변환된 데이터를 최종 목적지 시스템에 저장하는 과정
	일반적으로 다음과 같은 목적지를 가짐
	- 데이터 웨어하우스(Redshift, BigQuery, Snowflake)
	- 데이터 레이크(S3, HDFS, LakeFS 등)
	- 데이터 마트(특정 팀/도메인에 최적화된 서브 웨어하우스)
	- 검색 시스템(ElasticSearch)
	- 머신러닝 파일 스토리지(Feature Store 등)

##### 적재 방식
1. Full Load
	전체 데이터를 매번 덮어쓰기
	데이터 양이 적거나 정기 리셋이 필요한 경우 적합
2. Incremental Load
	변경/추가된 데이터만 적재
	대규모 데이터 처리 시 필수적

- [b] Load 시 고려할 점
- 대상 시스템의 스키마 설계(Star Schema, Snowflake Schema)
- 파티션 설계(날짜 단위, 지역 단위 등)
- 중복 처리 전략
- 실패 시 rollback 또는 재시도 전략
- 적재 시점의 원자성 보장


## ETL과 ELT의 차이
---
현대 데이터 엔지니어링에서는 ETL과 ELT의 전략적 차이가 매우 중요

## **ETL (Extract → Transform → Load)**

- 전통적인 방식을 의미
- 변환(Transform)을 외부 시스템에서 수행
- 목적지 시스템에 ‘처리된’ 데이터 저장
- Data Warehouse가 비싸고 느렸던 시절에 유용

## **ELT (Extract → Load → Transform)**

- 현대적 방식
- Raw 데이터 그대로 저장 후 목적지 시스템에서 Transform
- BigQuery, Snowflake처럼 고성능/저비용 DW의 등장으로 급격히 확산
- 원본 데이터 보존 가능
- 변환 로직 버전 관리 용이
- 스케일아웃/컬럼 기반 엔진 덕분에 빠른 처리 가능

현재는 ELT가 더 일반적이며, ETL은 특정 상황에서만 선택됩니다.


## ETL 파이프라인을 구현하는 도구들

### 오케스트레이션 도구
- [[Apache Airflow]]
- Perfect
- Dagster

### 데이터 처리 엔진
- Spark
- Flink
- Pandas
- dbt(ELT 기반)

### 데이터 이동 도구
- Kafka
- Logstash
- AWS Glue
- Google DataFlow