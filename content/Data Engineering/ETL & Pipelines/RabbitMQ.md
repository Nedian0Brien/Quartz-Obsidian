

## 개요
RabbitMQ는 오픈소스 메시지 브로커 소프트웨어로, AMQP(Advanced Message Queuing Protocol)를 구현한 대표적인 메시지 큐 시스템입니다. Erlang으로 작성되었으며, 비동기 메시징 패턴을 지원하여 분산 시스템 간의 통신을 중개합니다.

## 주요 특징

### 1. 메시지 브로커 패턴
- **Producer**: 메시지를 생성하여 Exchange로 전송
- **Exchange**: 라우팅 규칙에 따라 메시지를 적절한 Queue로 전달
- **Queue**: 메시지를 저장하고 Consumer에게 전달
- **Consumer**: Queue에서 메시지를 수신하여 처리

### 2. Exchange 타입
RabbitMQ의 핵심 개념으로, 메시지 라우팅 방식을 결정합니다:

- **Direct Exchange**
  - Routing Key가 정확히 일치하는 Queue로 메시지 전달
  - 일대일 메시징에 적합
  - 예: `routing_key="error"` → `queue_error`

- **Fanout Exchange**
  - 연결된 모든 Queue에 메시지를 브로드캐스트
  - Routing Key 무시
  - 예: 로그를 여러 시스템에 동시 전송

- **Topic Exchange**
  - 패턴 매칭을 통한 라우팅 (와일드카드 지원)
  - `*`: 단어 하나 대체
  - `#`: 0개 이상의 단어 대체
  - 예: `logs.*.critical` → `logs.app.critical`, `logs.db.critical`

- **Headers Exchange**
  - 메시지 헤더 속성을 기반으로 라우팅
  - Routing Key 대신 header의 key-value 매칭 사용

### 3. 메시지 영속성 (Durability)
- **Durable Queue**: 서버 재시작 후에도 Queue 유지
- **Persistent Message**: 메시지를 디스크에 저장하여 손실 방지
- **Transient**: 메모리에만 저장 (빠르지만 휘발성)

### 4. 메시지 확인 (Acknowledgment)
- **Auto Ack**: 메시지 전달 즉시 Queue에서 삭제
- **Manual Ack**: Consumer가 처리 완료 후 명시적으로 확인
- **Negative Ack (Nack)**: 처리 실패 시 재전송 요청

## 주요 사용 사례

### 1. 작업 큐 (Task Queue)
```python
# Producer
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()
channel.queue_declare(queue='task_queue', durable=True)

message = "Heavy computation task"
channel.basic_publish(
    exchange='',
    routing_key='task_queue',
    body=message,
    properties=pika.BasicProperties(delivery_mode=2)  # persistent
)
```

### 2. Pub/Sub 패턴
```python
# Publisher (Fanout Exchange)
channel.exchange_declare(exchange='logs', exchange_type='fanout')
channel.basic_publish(exchange='logs', routing_key='', body='Log message')

# Subscriber
result = channel.queue_declare(queue='', exclusive=True)
queue_name = result.method.queue
channel.queue_bind(exchange='logs', queue=queue_name)
```

### 3. 라우팅 (Topic Exchange)
```python
# 특정 로그 레벨만 수신
channel.queue_bind(exchange='topic_logs', queue=queue_name, routing_key='*.error')
```

## RabbitMQ vs Kafka

| 특성 | RabbitMQ | Kafka |
|------|----------|-------|
| **패러다임** | 메시지 브로커 (전통적인 큐) | 분산 이벤트 스트리밍 플랫폼 |
| **메시지 보관** | Consumer가 읽으면 삭제 | 설정된 기간 동안 보관 (재읽기 가능) |
| **처리량** | 중간 수준 (초당 수만 건) | 매우 높음 (초당 수백만 건) |
| **지연 시간** | 낮음 (밀리초) | 중간 (수 밀리초) |
| **라우팅** | 복잡한 라우팅 지원 (Exchange) | 단순 (Topic 기반) |
| **사용 사례** | 작업 큐, RPC, 복잡한 라우팅 | 로그 수집, 이벤트 소싱, 스트림 처리 |
| **메시지 순서** | Queue 단위 보장 | Partition 단위 보장 |

## 설치 및 기본 설정

### Docker를 이용한 설치
```bash
# Management UI 포함 버전
docker run -d --name rabbitmq \
  -p 5672:5672 \
  -p 15672:15672 \
  rabbitmq:3-management

# 접속: http://localhost:15672
# 기본 계정: guest/guest
```

### Python 클라이언트 (pika)
```bash
pip install pika
```

## 고급 기능

### 1. Dead Letter Exchange (DLX)
처리 실패하거나 만료된 메시지를 다른 Exchange로 라우팅
```python
channel.queue_declare(
    queue='main_queue',
    arguments={
        'x-dead-letter-exchange': 'dlx_exchange',
        'x-message-ttl': 60000  # 60초 후 만료
    }
)
```

### 2. Priority Queue
메시지에 우선순위를 부여하여 처리 순서 제어
```python
channel.queue_declare(queue='priority_queue', arguments={'x-max-priority': 10})
channel.basic_publish(
    exchange='',
    routing_key='priority_queue',
    body='Urgent task',
    properties=pika.BasicProperties(priority=9)
)
```

### 3. 클러스터링 및 HA
- **Mirroring**: Queue를 여러 노드에 복제하여 고가용성 확보
- **Federation**: 서로 다른 브로커 간 메시지 전달
- **Shovel**: 특정 Queue 간 메시지 이동

## 모니터링 및 관리

### Management UI
- Queue 상태, 메시지 수, 처리율 확인
- Exchange와 Queue 바인딩 시각화
- 메시지 수동 발행/조회
- 리소스 사용량 모니터링

### 주요 메트릭
- **메시지 비율**: 발행/전달/확인 속도
- **Queue 깊이**: 대기 중인 메시지 수
- **Consumer 수**: 활성 Consumer 연결
- **메모리 사용량**: High water mark 설정 중요

## 성능 최적화

### 1. Prefetch Count 설정
Consumer가 한 번에 받을 메시지 수 제한
```python
channel.basic_qos(prefetch_count=10)
```

### 2. 배치 처리
여러 메시지를 한 번에 확인하여 네트워크 오버헤드 감소

### 3. Lazy Queue
메시지를 메모리가 아닌 디스크에 우선 저장 (메모리 사용량 감소)
```python
channel.queue_declare(
    queue='lazy_queue',
    arguments={'x-queue-mode': 'lazy'}
)
```

## 관련 기술
- [[Kafka]] - 대규모 스트림 처리에 특화된 대안
- [[Apache Airflow]] - CeleryExecutor에서 RabbitMQ를 백엔드로 사용
- [[Redis]] - 간단한 메시지 큐가 필요한 경우 대안
- [[Celery]] - Python 분산 작업 큐 프레임워크 (RabbitMQ와 함께 자주 사용)

## 참고 자료
- [RabbitMQ 공식 문서](https://www.rabbitmq.com/documentation.html)
- [RabbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html)
- [AMQP 0-9-1 Model](https://www.rabbitmq.com/tutorials/amqp-concepts.html)

## 태그
#message-queue #rabbitmq #amqp #distributed-systems #etl #async-messaging