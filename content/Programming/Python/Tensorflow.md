#AI 

[[Python]]의 [[Machine Learning]] 라이브러리
[[Google]]에서 개발한 것으로 유명하다.
요즘은 [[Pytorch]]에서 텐서플로 쪽으로 주도권이 넘어가고 있다고 한다.


## TensorFlow란?

TensorFlow는 [[Google]] Brain 팀에서 개발한 오픈소스 머신러닝 프레임워크입니다. 2015년 출시 이후 산업계에서 널리 사용되고 있으며, 프로덕션 환경에서의 배포가 강점입니다.

## 주요 특징

### 1. Static Computational Graph (정적 연산 그래프)
- TensorFlow 1.x: 그래프를 먼저 정의한 후 실행
- TensorFlow 2.x: Eager Execution으로 동적 실행 지원

### 2. 다양한 플랫폼 지원
- 서버, 모바일(TF Lite), 웹(TensorFlow.js)
- TPU 최적화
- 엣지 디바이스 배포

### 3. 프로덕션 중심
- TensorFlow Serving으로 쉬운 모델 배포
- TensorFlow Extended (TFX)로 완전한 ML 파이프라인
- 대규모 분산 학습 지원

### 4. Keras 통합
- TensorFlow 2.0부터 Keras가 공식 고수준 API로 통합
- `tf.keras`로 간편하게 사용

## 설치

```bash
# CPU 버전
pip install tensorflow

# GPU 버전 (CUDA, cuDNN 필요)
pip install tensorflow[and-cuda]

# TensorFlow 버전 확인
python -c "import tensorflow as tf; print(tf.__version__)"
```

## TensorFlow 2.x의 핵심 변화

### Eager Execution (즉시 실행)
```python
import tensorflow as tf

# TensorFlow 2.x에서는 기본적으로 즉시 실행
x = tf.constant([1, 2, 3])
y = tf.constant([4, 5, 6])
z = x + y
print(z)  # 바로 결과 출력
```

### tf.function으로 그래프 최적화
```python
@tf.function
def fast_function(x, y):
    return x + y

# 첫 호출 시 그래프로 컴파일
result = fast_function(x, y)
```

## Keras API (tf.keras)

### Sequential 모델
```python
import tensorflow as tf
from tensorflow import keras

model = keras.Sequential([
    keras.layers.Dense(128, activation='relu', input_shape=(784,)),
    keras.layers.Dropout(0.2),
    keras.layers.Dense(10, activation='softmax')
])

model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

history = model.fit(x_train, y_train, epochs=5, validation_split=0.2)
```

### Functional API
```python
inputs = keras.Input(shape=(784,))
x = keras.layers.Dense(128, activation='relu')(inputs)
x = keras.layers.Dropout(0.2)(x)
outputs = keras.layers.Dense(10, activation='softmax')(x)

model = keras.Model(inputs=inputs, outputs=outputs)
```

### Model Subclassing
```python
class MyModel(keras.Model):
    def __init__(self):
        super(MyModel, self).__init__()
        self.dense1 = keras.layers.Dense(128, activation='relu')
        self.dropout = keras.layers.Dropout(0.2)
        self.dense2 = keras.layers.Dense(10, activation='softmax')
    
    def call(self, inputs, training=None):
        x = self.dense1(inputs)
        if training:
            x = self.dropout(x)
        return self.dense2(x)
```

## 텐서 연산

### 기본 텐서
```python
import tensorflow as tf

# 텐서 생성
x = tf.constant([1, 2, 3])
y = tf.zeros([2, 3])
z = tf.ones([3, 4])
r = tf.random.normal([2, 3])

# NumPy 변환
import numpy as np
arr = np.array([1, 2, 3])
x = tf.constant(arr)
arr_back = x.numpy()
```

### 텐서 연산
```python
# 기본 연산
a = tf.constant([1, 2, 3])
b = tf.constant([4, 5, 6])

c = tf.add(a, b)  # 또는 a + b
c = tf.multiply(a, b)  # 원소별 곱
c = tf.matmul(a, b)  # 행렬 곱

# 차원 변경
x = tf.reshape(x, [2, 3, 4])
x = tf.transpose(x, perm=[1, 0, 2])

# 통계 연산
mean = tf.reduce_mean(x)
sum_val = tf.reduce_sum(x, axis=1)
max_val = tf.reduce_max(x)
```

## 자동 미분 (GradientTape)

```python
# 그래디언트 계산
x = tf.Variable(3.0)

with tf.GradientTape() as tape:
    y = x ** 2

dy_dx = tape.gradient(y, x)  # dy/dx = 2x = 6
print(dy_dx)

# 다중 변수
x = tf.Variable(2.0)
y = tf.Variable(3.0)

with tf.GradientTape() as tape:
    z = x ** 2 + y ** 2

dz_dx, dz_dy = tape.gradient(z, [x, y])
```

## 커스텀 학습 루프

```python
model = MyModel()
optimizer = keras.optimizers.Adam()
loss_fn = keras.losses.SparseCategoricalCrossentropy()

@tf.function
def train_step(x, y):
    with tf.GradientTape() as tape:
        predictions = model(x, training=True)
        loss = loss_fn(y, predictions)
    
    gradients = tape.gradient(loss, model.trainable_variables)
    optimizer.apply_gradients(zip(gradients, model.trainable_variables))
    return loss

# 학습 루프
for epoch in range(num_epochs):
    for x_batch, y_batch in train_dataset:
        loss = train_step(x_batch, y_batch)
    
    print(f'Epoch {epoch}, Loss: {loss.numpy():.4f}')
```

## 데이터 파이프라인 (tf.data)

### Dataset API
```python
# NumPy 배열로부터
dataset = tf.data.Dataset.from_tensor_slices((x_train, y_train))

# 배치 처리
dataset = dataset.batch(32)

# 셔플
dataset = dataset.shuffle(buffer_size=1000)

# 프리페치 (성능 최적화)
dataset = dataset.prefetch(tf.data.AUTOTUNE)

# 맵핑
def preprocess(x, y):
    x = tf.cast(x, tf.float32) / 255.0
    return x, y

dataset = dataset.map(preprocess, num_parallel_calls=tf.data.AUTOTUNE)

# 학습에 사용
model.fit(dataset, epochs=5)
```

### 이미지 데이터
```python
# 이미지 폴더로부터 로드
train_dataset = tf.keras.preprocessing.image_dataset_from_directory(
    'data/train',
    image_size=(224, 224),
    batch_size=32,
    label_mode='categorical'
)

# 데이터 증강
data_augmentation = keras.Sequential([
    keras.layers.RandomFlip("horizontal"),
    keras.layers.RandomRotation(0.2),
    keras.layers.RandomZoom(0.2)
])

augmented_dataset = train_dataset.map(
    lambda x, y: (data_augmentation(x, training=True), y)
)
```

## 모델 저장 및 로드

### SavedModel 형식 (권장)
```python
# 전체 모델 저장
model.save('my_model')

# 모델 로드
loaded_model = keras.models.load_model('my_model')
```

### HDF5 형식
```python
# .h5 형식으로 저장
model.save('model.h5')

# 로드
model = keras.models.load_model('model.h5')
```

### 체크포인트
```python
# 체크포인트 콜백
checkpoint_callback = keras.callbacks.ModelCheckpoint(
    filepath='checkpoint/model.ckpt',
    save_weights_only=True,
    save_best_only=True,
    monitor='val_loss'
)

model.fit(x_train, y_train, callbacks=[checkpoint_callback])

# 가중치 로드
model.load_weights('checkpoint/model.ckpt')
```

## TensorBoard

```python
# TensorBoard 콜백
tensorboard_callback = keras.callbacks.TensorBoard(
    log_dir='./logs',
    histogram_freq=1,
    write_graph=True
)

model.fit(
    x_train, y_train,
    epochs=5,
    callbacks=[tensorboard_callback]
)

# 커맨드라인에서 실행
# tensorboard --logdir=./logs
```

### 커스텀 로깅
```python
import datetime

log_dir = "logs/fit/" + datetime.datetime.now().strftime("%Y%m%d-%H%M%S")
tensorboard_callback = keras.callbacks.TensorBoard(log_dir=log_dir)

# 커스텀 메트릭 로깅
file_writer = tf.summary.create_file_writer(log_dir)

with file_writer.as_default():
    tf.summary.scalar('custom_metric', value, step=epoch)
```

## 전이 학습

```python
# 사전 훈련된 모델 로드
base_model = keras.applications.ResNet50(
    weights='imagenet',
    include_top=False,
    input_shape=(224, 224, 3)
)

# 베이스 모델 동결
base_model.trainable = False

# 새로운 레이어 추가
inputs = keras.Input(shape=(224, 224, 3))
x = base_model(inputs, training=False)
x = keras.layers.GlobalAveragePooling2D()(x)
x = keras.layers.Dense(256, activation='relu')(x)
outputs = keras.layers.Dense(10, activation='softmax')(x)

model = keras.Model(inputs, outputs)

# Fine-tuning
base_model.trainable = True
for layer in base_model.layers[:-10]:
    layer.trainable = False
```

## 분산 학습

### MirroredStrategy (단일 머신, 다중 GPU)
```python
strategy = tf.distribute.MirroredStrategy()

with strategy.scope():
    model = create_model()
    model.compile(
        optimizer='adam',
        loss='sparse_categorical_crossentropy',
        metrics=['accuracy']
    )

model.fit(train_dataset, epochs=5)
```

### MultiWorkerMirroredStrategy (다중 머신)
```python
strategy = tf.distribute.MultiWorkerMirroredStrategy()

with strategy.scope():
    model = create_model()
    model.compile(...)

model.fit(train_dataset, epochs=5)
```

## TensorFlow Lite (모바일/엣지)

```python
# 모델 변환
converter = tf.lite.TFLiteConverter.from_keras_model(model)
tflite_model = converter.convert()

# 파일로 저장
with open('model.tflite', 'wb') as f:
    f.write(tflite_model)

# 최적화
converter.optimizations = [tf.lite.Optimize.DEFAULT]

# 양자화
converter.representative_dataset = representative_dataset_gen
converter.target_spec.supported_ops = [tf.lite.OpsSet.TFLITE_BUILTINS_INT8]
```

## TensorFlow.js (웹)

```python
# 모델을 TensorFlow.js 형식으로 변환
import tensorflowjs as tfjs

tfjs.converters.save_keras_model(model, 'tfjs_model')
```

## Mixed Precision Training

```python
# 혼합 정밀도로 학습 속도 향상
from tensorflow.keras import mixed_precision

policy = mixed_precision.Policy('mixed_float16')
mixed_precision.set_global_policy(policy)

# 모델 정의 (자동으로 mixed precision 적용)
model = create_model()
```

## TensorFlow Hub

```python
import tensorflow_hub as hub

# 사전 훈련된 모델 로드
embedding = hub.KerasLayer(
    "https://tfhub.dev/google/universal-sentence-encoder/4",
    trainable=False
)

model = keras.Sequential([
    embedding,
    keras.layers.Dense(16, activation='relu'),
    keras.layers.Dense(1, activation='sigmoid')
])
```

## 실전 예제: CNN 이미지 분류

```python
import tensorflow as tf
from tensorflow import keras

# 데이터 로드
(x_train, y_train), (x_test, y_test) = keras.datasets.cifar10.load_data()

# 전처리
x_train = x_train.astype('float32') / 255.0
x_test = x_test.astype('float32') / 255.0

# 모델 정의
model = keras.Sequential([
    keras.layers.Conv2D(32, (3, 3), activation='relu', input_shape=(32, 32, 3)),
    keras.layers.MaxPooling2D((2, 2)),
    keras.layers.Conv2D(64, (3, 3), activation='relu'),
    keras.layers.MaxPooling2D((2, 2)),
    keras.layers.Conv2D(64, (3, 3), activation='relu'),
    keras.layers.Flatten(),
    keras.layers.Dense(64, activation='relu'),
    keras.layers.Dropout(0.5),
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
    batch_size=64,
    epochs=10,
    validation_split=0.2,
    callbacks=[
        keras.callbacks.EarlyStopping(patience=3),
        keras.callbacks.ReduceLROnPlateau(factor=0.5, patience=2)
    ]
)

# 평가
test_loss, test_acc = model.evaluate(x_test, y_test)
print(f'Test accuracy: {test_acc:.4f}')
```

## TensorFlow 1.x vs 2.x

| 특징 | TensorFlow 1.x | TensorFlow 2.x |
|------|---------------|---------------|
| 실행 모드 | Graph (세션 필요) | Eager (즉시 실행) |
| API | 분산된 API | Keras 중심 통합 |
| 디버깅 | 어려움 | Python 디버거 사용 가능 |
| 코드 복잡도 | 높음 | 낮음 |
| 성능 | 최적화 가능 | @tf.function으로 최적화 |

## TensorFlow vs PyTorch

| 특징 | TensorFlow | [[Pytorch]] |
|------|-----------|---------|
| 배포 | 매우 강력 (Serving, Lite, JS) | 성장 중 (TorchServe) |
| 프로덕션 | 산업계 표준 | 점점 증가 |
| 연구 | 사용 가능 | 연구자 선호 |
| 학습 곡선 | 중간 (2.x), 어려움 (1.x) | 중간 |
| 모바일 | TF Lite (성숙) | PyTorch Mobile |
| 커뮤니티 | 대규모 | 대규모 |

## 장단점

### 장점
- ✅ 프로덕션 배포에 최적화
- ✅ 다양한 플랫폼 지원 (모바일, 웹, 서버)
- ✅ TensorBoard로 강력한 시각화
- ✅ 대규모 분산 학습 지원
- ✅ TPU 최적화

### 단점
- ❌ 1.x는 복잡했음 (2.x에서 많이 개선)
- ❌ [[Pytorch]]에 비해 연구 유연성이 낮음
- ❌ 커뮤니티가 분산되어 있음 (1.x vs 2.x)

## 관련 문서
- [[Keras]] - TensorFlow의 고수준 API
- [[Pytorch]] - 대안 딥러닝 프레임워크
- [[Python]] - 프로그래밍 언어
- [[Machine Learning]] - 머신러닝 개념

## 참고 자료
- [TensorFlow 공식 문서](https://www.tensorflow.org/)
- [TensorFlow 튜토리얼](https://www.tensorflow.org/tutorials)
- [TensorFlow Hub](https://tfhub.dev/)
- [Keras 가이드](https://keras.io/guides/)
