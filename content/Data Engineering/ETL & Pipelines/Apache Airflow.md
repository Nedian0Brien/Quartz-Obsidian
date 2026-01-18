#데이터엔지니어링

## 개요

복잡한 데이터 워크플로우를 코드로 정의하고, 스케줄링하고, 모니터링하기 위한 오픈소스 워크플로우 오케스트레이션 플랫폼

- 데이터 엔지니어링, 머신러닝 파이프라인 구축, [[ETL]] 처리, 배치 작업 자동화 등 다양한 분야에서 널리 사용됨

#### Apache Airflow가 널리 사용되는 이유
- 코드 기반 파이프라인 정의(DAG as code)
- 다양한 연산자를 통한 외부 시스템 연동
- 강력한 스케줄링 기능
- 직관적인 UI
- 로그 및 모니터링 지원
- 확장성, 대규모 분산 실행


## 핵심 개념
---
### DAG (Directed Acyclic Graph)
<mark style="background: #ABF7F7A6;">방향성</mark>이 있고 <mark style="background: #FFB86CA6;">비순환</mark>적인 그래프이며, Airflow에서 워크플로우 전체를 구조적으로 표현하는 단위
- 방향성: Task A -> Task B 처럼 실행 순서를 가진다는 의미
- 비순환: 순환 구조가 없어 무한 반복이 발생하지 않음

파이썬 파일로 작성되며, 다음 요소를 포함함
- DAG 이름
- 스케줄링 주기 `schedule_interval`
- 수행할 Task들
- Task 간 의존 관계

DAG 파일은 Airflow에 의해 주기적으로 파싱되고, UI에 반영됨
### Task
DAG 안에서 개별적으로 실행되는 단위 작업
Airflow에서는 `Operator`라는 클래스를 사용해 Task를 정의함

- 예시
	- `BashOperator`
		- Bash 스크립트를 실행
	- `PythonOperator`
		- 특정 파이썬 함수르 실행
	- `S3ToRedshiftOperator`
		- S3 -> Redshift 데이터 적재
	- `KubernetesPodOperator`
		- Kubernetes Pod를 생성하여 작업 실행
	- `DummyOperator`
		- 테스트용 또는 단순 연결용 작업

각 Task에 포함되는 요소
- 실제 작업 내용
- retry 전략
- timeout
- up/downstream 관계

### 스케줄러(Scheduler)
Airflow 스케줄러는 DAG 정의를 읽고, 실행 시점이 되면 Task 실행을 트리거함
또는 의존성 조건을 체크하여 순차적으로 Task를 실행

### Executor 및 Worker
Airflow는 Executor를 통해 작업 실행 방식을 결정함

대표적인 Executor:
- `SequentialExecutor`
	- 로컬 개발용. 한 번에 하나씩 실행
- `LocalExecutor`
	- 멀티프로세스 기반. 단일 머신에서 병렬 실행
- `CeleryExecutor`
	- [[Celery]] + [[Redis]]/[[RabbitMQ]]를 이용한 분산 실행
- `KubernetesExecutor`
	- 각 Task를 [[Kubernetes]] Pod로 띄워 대규모 확장 가능

### Web UI
Airflow가 좋은 이유 중 하나는 매우 직관적인 Web UI
- DAG 그래프 시각화
- Gantt 차트로 실행 시간 확인
- Task 별 로그 확인
- 수동 재실행
- 실패 Task 재시도
- DAG 활성화 / 비활성화 제어

이러한 기능을 통해 운영 및 디버깅에 매우 유용


## Airflow의 작동 흐름
---
Airflow는 다음과 같은 전체 흐름으로 작동함
1. 사용자가 DAG 파일을 작성하여 dags 폴더에 저장
2. 스케줄러가 DAG를 파싱하여 실행 계획을 등록
3. 스케줄이 도래하면 DAG Run 생성
4. Executor가 Task를 Worker에게 전달
5. Worker가 Task를 실행
6. 실행 결과(성공/실패/재시도)를 메타스토어([[Redis]]/[[RabbitMQ]])에 기록
7. Web UI에서 실행 흐름과 로그를 확인 가능

## Airflow의 장점
---
#### 코드 기반 정의
- 파이썬 코드를 사용해 파이프라인을 정의하므로 아래와 같은 장점이 있음
	- 버전관리(Git) 가능
	- 테스트 용이
	- 파이썬 생태계 활용 가능
#### 강력한 스케줄링
cron 표현식뿐 아니라 timedelta 또는 다양한 schedule 옵션 지원
#### 탄탄한 확장성
CeleryExecutor, KubernetesExecutor 등을 통해 수십~수천 개의 Task도 안정적으로 처리
#### 다양한 연동성
AWS, GCP, [[Kubernetes]], DB, [[Hadoop]], [[Spark]] 등 거의 모든 시스템과 연동 가능한 연산자 제공
#### 운영 친화적 UI
실행, 실패, 지연 등의 상태를 직관적으로 확인 가능

## Airflow의 단점 및 고려사항
---
#### 실시간 처리에는 부적합
Airflow는 배치 처리 중심이며, 이벤트 기반 실시간 처리에는 어울리지 않음
#### 의존성 관리의 복잡성
DAG 파일의 파이썬 환경 관리가 필요하며, 패키지 충돌 등을 주의해야 함
#### DAG 배포 자동화 필요
프로덕션 환경에서는 DAG 파일을 git + CI/CD로 배포하는 구조 필요
#### 설정이 복잡함
Executor, DB, Celery, Redis, Worker 등 구성 요소가 많아 처음 설정이 어려움





