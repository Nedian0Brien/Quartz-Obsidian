#AI 

[[Machine Learning]]을 [[Python]]에서 쉽게 구현할 수 있게 해 주는 라이브러리. [[Tensorflow]]기반으로 작동한다.


## Keras란?

Keras는 [[Python]]으로 작성된 고수준 신경망 API로, [[Tensorflow]], Theano, CNTK 위에서 실행될 수 있습니다. 2015년 François Chollet이 개발했으며, 현재는 TensorFlow의 공식 고수준 API로 통합되어 있습니다.

## 주요 특징

### 1. 사용자 친화적
- 간결하고 일관된 API
- 최소한의 코드로 모델 구축 가능
- 직관적인 모델 정의 방식

### 2. 모듈식 구조
```python
from tensorflow import keras
from tensorflow.keras import layers

model = keras.Sequential([
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')
])
```

### 3. 확장 가능
- 사용자 정의 레이어, 손실 함수, 메트릭 추가 가능
- 복잡한 모델 아키텍처 구현 가능

### 4. 다양한 백엔드 지원
- TensorFlow (기본)
- Theano
- CNTK

## 설치

```bash
# TensorFlow와 함께 설치 (권장)
pip install tensorflow

# 또는 독립 설치
pip install keras
```

## 모델 구축 방법

### 1. Sequential API (순차 모델)
가장 간단한 방식으로 레이어를 순차적으로 쌓는 방식입니다.

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Dropout

model = Sequential([
    Dense(128, activation='relu', input_shape=(784,)),
    Dropout(0.2),
    Dense(64, activation='relu'),
    Dropout(0.2),
    Dense(10, activation='softmax')
])
```

### 2. Functional API (함수형 API)
더 복잡한 모델(다중 입출력, 공유 레이어 등)을 구축할 때 사용합니다.

```python
from tensorflow.keras.layers import Input, Dense, concatenate
from tensorflow.keras.models import Model

# 입력 레이어
input_a = Input(shape=(128,), name='input_a')
input_b = Input(shape=(64,), name='input_b')

# 각 입력에 대한 처리
x = Dense(64, activation='relu')(input_a)
y = Dense(32, activation='relu')(input_b)

# 두 경로를 결합
combined = concatenate([x, y])

# 출력 레이어
output = Dense(10, activation='softmax')(combined)

# 모델 생성
model = Model(inputs=[input_a, input_b], outputs=output)
```

### 3. Model Subclassing (서브클래싱)
가장 유연한 방식으로, 복잡한 커스텀 모델을 구현할 때 사용합니다.

```python
import tensorflow as tf

class MyModel(tf.keras.Model):
    def __init__(self):
        super(MyModel, self).__init__()
        self.dense1 = tf.keras.layers.Dense(64, activation='relu')
        self.dense2 = tf.keras.layers.Dense(10, activation='softmax')
    
    def call(self, inputs):
        x = self.dense1(inputs)
        return self.dense2(x)

model = MyModel()
```

## 모델 컴파일

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

### 주요 옵티마이저
- `adam` - 대부분의 경우 좋은 성능
- `sgd` - 기본적인 확률적 경사하강법
- `rmsprop` - RNN에 효과적
- `adamw` - Weight decay가 추가된 Adam

### 주요 손실 함수
- `binary_crossentropy` - 이진 분류
- `categorical_crossentropy` - 다중 클래스 분류 (원핫인코딩)
- `sparse_categorical_crossentropy` - 다중 클래스 분류 (정수 레이블)
- `mse` - 회귀 문제

## 모델 학습

```python
history = model.fit(
    x_train, y_train,
    batch_size=32,
    epochs=10,
    validation_split=0.2,
    callbacks=[
        keras.callbacks.EarlyStopping(patience=3),
        keras.callbacks.ModelCheckpoint('best_model.h5')
    ]
)
```

## 주요 레이어

### 핵심 레이어
```python
from tensorflow.keras.layers import Dense, Dropout, Flatten

# 완전 연결 레이어
Dense(units=64, activation='relu')

# 드롭아웃 (과적합 방지)
Dropout(rate=0.5)

# 평탄화 (다차원 → 1차원)
Flatten()
```

### 합성곱 레이어 (이미지)
```python
from tensorflow.keras.layers import Conv2D, MaxPooling2D

# 2D 합성곱
Conv2D(filters=32, kernel_size=(3, 3), activation='relu')

# 맥스 풀링
MaxPooling2D(pool_size=(2, 2))
```

### 순환 레이어 (시계열)
```python
from tensorflow.keras.layers import LSTM, GRU, SimpleRNN

# LSTM
LSTM(units=128, return_sequences=True)

# GRU
GRU(units=64)

# Simple RNN
SimpleRNN(units=32)
```

### 정규화 레이어
```python
from tensorflow.keras.layers import BatchNormalization, LayerNormalization

# 배치 정규화
BatchNormalization()

# 레이어 정규화
LayerNormalization()
```

## 콜백 (Callbacks)

학습 과정을 모니터링하고 제어하는 도구입니다.

```python
from tensorflow.keras.callbacks import (
    EarlyStopping,
    ModelCheckpoint,
    ReduceLROnPlateau,
    TensorBoard
)

callbacks = [
    # 조기 종료
    EarlyStopping(
        monitor='val_loss',
        patience=5,
        restore_best_weights=True
    ),
    
    # 모델 저장
    ModelCheckpoint(
        'best_model.h5',
        monitor='val_accuracy',
        save_best_only=True
    ),
    
    # 학습률 감소
    ReduceLROnPlateau(
        monitor='val_loss',
        factor=0.5,
        patience=3
    ),
    
    # TensorBoard 로깅
    TensorBoard(log_dir='./logs')
]
```

## 모델 저장 및 로드

```python
# 전체 모델 저장
model.save('my_model.h5')

# 모델 로드
from tensorflow.keras.models import load_model
model = load_model('my_model.h5')

# 가중치만 저장
model.save_weights('model_weights.h5')

# 가중치만 로드
model.load_weights('model_weights.h5')
```

## 전이 학습 (Transfer Learning)

```python
from tensorflow.keras.applications import VGG16

# 사전 훈련된 모델 로드
base_model = VGG16(
    weights='imagenet',
    include_top=False,
    input_shape=(224, 224, 3)
)

# 베이스 모델 동결
base_model.trainable = False

# 새로운 레이어 추가
model = Sequential([
    base_model,
    Flatten(),
    Dense(256, activation='relu'),
    Dropout(0.5),
    Dense(10, activation='softmax')
])
```

## 데이터 전처리

### 이미지 데이터 증강
```python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

datagen = ImageDataGenerator(
    rotation_range=20,
    width_shift_range=0.2,
    height_shift_range=0.2,
    horizontal_flip=True,
    zoom_range=0.2
)

# 학습에 적용
model.fit(
    datagen.flow(x_train, y_train, batch_size=32),
    epochs=50
)
```

### 텍스트 전처리
```python
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences

tokenizer = Tokenizer(num_words=10000)
tokenizer.fit_on_texts(texts)

sequences = tokenizer.texts_to_sequences(texts)
padded = pad_sequences(sequences, maxlen=100)
```

## Keras vs PyTorch

| 특징 | Keras | [[Pytorch]] |
|------|-------|---------|
| 학습 곡선 | 쉬움 | 중간 |
| 유연성 | 중간 | 높음 |
| 프로덕션 | TensorFlow 생태계 | PyTorch 생태계 |
| 연구 | 빠른 프로토타이핑 | 세밀한 제어 |
| 커뮤니티 | 대규모 | 성장 중 |

## 장단점

### 장점
- ✅ 매우 직관적이고 사용하기 쉬움
- ✅ 빠른 프로토타이핑 가능
- ✅ 풍부한 문서와 예제
- ✅ TensorFlow 생태계와 완벽한 통합

### 단점
- ❌ PyTorch에 비해 연구 유연성이 낮음
- ❌ 매우 커스텀한 모델 구현 시 제약
- ❌ 디버깅이 때때로 어려움

## 실전 예제: MNIST 분류

```python
import tensorflow as tf
from tensorflow import keras

# 데이터 로드
(x_train, y_train), (x_test, y_test) = keras.datasets.mnist.load_data()

# 전처리
x_train = x_train.reshape(-1, 784).astype('float32') / 255
x_test = x_test.reshape(-1, 784).astype('float32') / 255

# 모델 구축
model = keras.Sequential([
    keras.layers.Dense(128, activation='relu', input_shape=(784,)),
    keras.layers.Dropout(0.2),
    keras.layers.Dense(10, activation='softmax')
])

# 컴파일
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

# 학습
history = model.fit(
    x_train, y_train,
    batch_size=128,
    epochs=5,
    validation_split=0.1
)

# 평가
test_loss, test_acc = model.evaluate(x_test, y_test)
print(f'Test accuracy: {test_acc:.4f}')
```

## 관련 문서
- [[Tensorflow]] - Keras의 백엔드
- [[Pytorch]] - 대안 딥러닝 프레임워크
- [[Python]] - 프로그래밍 언어
- [[Machine Learning]] - 머신러닝 개념

## 참고 자료
- [Keras 공식 문서](https://keras.io/)
- [TensorFlow Keras 가이드](https://www.tensorflow.org/guide/keras)
- [Keras 예제](https://keras.io/examples/)
