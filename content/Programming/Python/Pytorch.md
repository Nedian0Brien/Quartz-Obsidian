#AI 

텐서플로와 함께 양대 주축을 이루는 [[Python]]의 [[Machine Learning]] 라이브러리

연구 목적으로는 텐서플로보다 파이토치를 사용하는 경우가 더 많다고 한다.

쉽게 신경망을 구성할 수 있도록 해 주는 [[Keras]]라는 라이브러리가 있는 텐서플로에 비해서 사용하기 보다 어렵지만, 대신 연구자가 마음대로 수정할 수 있는 부분이 더 많다.


## PyTorch란?

PyTorch는 Facebook AI Research(FAIR)에서 개발한 오픈소스 딥러닝 프레임워크입니다. 2016년 출시 이후 연구 커뮤니티에서 빠르게 인기를 얻었으며, 현재 AI 연구의 사실상 표준으로 자리잡았습니다.

## 주요 특징

### 1. Dynamic Computational Graph (동적 연산 그래프)
- 실행 시점에 그래프가 생성되어 유연성이 높음
- 디버깅이 쉬움 (일반 Python 디버거 사용 가능)
- 조건문, 반복문 등을 자유롭게 사용 가능

```python
import torch

def forward(x, condition):
    if condition:
        return x * 2
    else:
        return x + 2
```

### 2. Pythonic한 설계
- NumPy와 유사한 API
- Python의 자연스러운 흐름을 따름
- 직관적인 텐서 연산

### 3. GPU 가속
```python
# CPU 텐서
x = torch.tensor([1, 2, 3])

# GPU로 이동
x = x.cuda()  # 또는 x.to('cuda')

# 다시 CPU로
x = x.cpu()
```

### 4. 강력한 자동 미분
```python
x = torch.tensor([2.0], requires_grad=True)
y = x ** 2
y.backward()
print(x.grad)  # dy/dx = 2x = 4
```

## 설치

```bash
# CPU 버전
pip install torch torchvision torchaudio

# CUDA 11.8 버전
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# CUDA 12.1 버전
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

## 텐서 (Tensor)

PyTorch의 기본 자료구조입니다.

### 텐서 생성
```python
import torch

# 다양한 생성 방법
x = torch.tensor([1, 2, 3])
x = torch.zeros(3, 4)
x = torch.ones(2, 3)
x = torch.randn(2, 3)  # 정규분포
x = torch.arange(0, 10, 2)  # [0, 2, 4, 6, 8]
x = torch.linspace(0, 1, 5)  # [0, 0.25, 0.5, 0.75, 1]

# NumPy 변환
import numpy as np
arr = np.array([1, 2, 3])
x = torch.from_numpy(arr)
arr_back = x.numpy()
```

### 텐서 연산
```python
# 기본 연산
a = torch.tensor([1, 2, 3])
b = torch.tensor([4, 5, 6])

c = a + b  # 덧셈
c = a * b  # 원소별 곱
c = a @ b  # 내적 (dot product)

# 행렬 연산
A = torch.randn(3, 4)
B = torch.randn(4, 5)
C = A @ B  # 또는 torch.matmul(A, B)

# 차원 변경
x = torch.randn(2, 3, 4)
x = x.view(2, 12)  # reshape
x = x.transpose(0, 1)  # 차원 교환
x = x.permute(2, 0, 1)  # 여러 차원 재배치
```

## 신경망 구축 (nn.Module)

### 기본 구조
```python
import torch.nn as nn

class SimpleNet(nn.Module):
    def __init__(self):
        super(SimpleNet, self).__init__()
        self.fc1 = nn.Linear(784, 128)
        self.fc2 = nn.Linear(128, 10)
        self.relu = nn.ReLU()
        self.dropout = nn.Dropout(0.2)
    
    def forward(self, x):
        x = self.fc1(x)
        x = self.relu(x)
        x = self.dropout(x)
        x = self.fc2(x)
        return x

model = SimpleNet()
```

### Sequential 모델
```python
model = nn.Sequential(
    nn.Linear(784, 128),
    nn.ReLU(),
    nn.Dropout(0.2),
    nn.Linear(128, 10)
)
```

### 주요 레이어들
```python
# 선형 레이어
nn.Linear(in_features, out_features)

# 합성곱 레이어
nn.Conv2d(in_channels, out_channels, kernel_size)
nn.Conv1d(in_channels, out_channels, kernel_size)

# 풀링 레이어
nn.MaxPool2d(kernel_size)
nn.AvgPool2d(kernel_size)

# 순환 레이어
nn.RNN(input_size, hidden_size)
nn.LSTM(input_size, hidden_size)
nn.GRU(input_size, hidden_size)

# 정규화 레이어
nn.BatchNorm2d(num_features)
nn.LayerNorm(normalized_shape)
nn.Dropout(p=0.5)

# 활성화 함수
nn.ReLU()
nn.Sigmoid()
nn.Tanh()
nn.LeakyReLU()
nn.GELU()
```

## 학습 루프

### 기본 학습 코드
```python
import torch.optim as optim

# 모델, 손실 함수, 옵티마이저 정의
model = SimpleNet()
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

# 학습 루프
for epoch in range(num_epochs):
    for batch_idx, (data, target) in enumerate(train_loader):
        # Forward pass
        output = model(data)
        loss = criterion(output, target)
        
        # Backward pass
        optimizer.zero_grad()  # 그래디언트 초기화
        loss.backward()        # 역전파
        optimizer.step()       # 가중치 업데이트
        
        if batch_idx % 100 == 0:
            print(f'Epoch: {epoch}, Loss: {loss.item():.4f}')
```

### 평가 모드
```python
model.eval()  # 평가 모드 (Dropout, BatchNorm 동작 변경)

with torch.no_grad():  # 그래디언트 계산 비활성화
    for data, target in test_loader:
        output = model(data)
        # 평가 로직

model.train()  # 다시 학습 모드로
```

## 데이터 로딩 (DataLoader)

### Dataset 클래스
```python
from torch.utils.data import Dataset, DataLoader

class CustomDataset(Dataset):
    def __init__(self, data, labels):
        self.data = data
        self.labels = labels
    
    def __len__(self):
        return len(self.data)
    
    def __getitem__(self, idx):
        return self.data[idx], self.labels[idx]

# 사용
dataset = CustomDataset(data, labels)
dataloader = DataLoader(
    dataset,
    batch_size=32,
    shuffle=True,
    num_workers=4
)
```

### 내장 데이터셋
```python
from torchvision import datasets, transforms

# MNIST 예제
transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))
])

train_dataset = datasets.MNIST(
    root='./data',
    train=True,
    download=True,
    transform=transform
)

train_loader = DataLoader(
    train_dataset,
    batch_size=64,
    shuffle=True
)
```

## 옵티마이저

```python
import torch.optim as optim

# SGD
optimizer = optim.SGD(model.parameters(), lr=0.01, momentum=0.9)

# Adam
optimizer = optim.Adam(model.parameters(), lr=0.001)

# AdamW (Weight Decay 포함)
optimizer = optim.AdamW(model.parameters(), lr=0.001, weight_decay=0.01)

# 학습률 스케줄러
scheduler = optim.lr_scheduler.StepLR(optimizer, step_size=10, gamma=0.1)

# 학습 루프에서
for epoch in range(num_epochs):
    train(...)
    scheduler.step()
```

## 손실 함수

```python
# 분류
criterion = nn.CrossEntropyLoss()  # 다중 클래스
criterion = nn.BCELoss()  # 이진 분류 (sigmoid 후)
criterion = nn.BCEWithLogitsLoss()  # 이진 분류 (sigmoid 내장)

# 회귀
criterion = nn.MSELoss()  # 평균 제곱 오차
criterion = nn.L1Loss()  # 평균 절대 오차
criterion = nn.SmoothL1Loss()  # Huber Loss

# 커스텀 손실 함수
def custom_loss(output, target):
    return torch.mean((output - target) ** 2)
```

## 모델 저장 및 로드

```python
# 전체 모델 저장
torch.save(model, 'model.pth')
model = torch.load('model.pth')

# 상태 딕셔너리만 저장 (권장)
torch.save(model.state_dict(), 'model_weights.pth')
model.load_state_dict(torch.load('model_weights.pth'))

# 체크포인트 저장 (학습 재개용)
checkpoint = {
    'epoch': epoch,
    'model_state_dict': model.state_dict(),
    'optimizer_state_dict': optimizer.state_dict(),
    'loss': loss
}
torch.save(checkpoint, 'checkpoint.pth')

# 체크포인트 로드
checkpoint = torch.load('checkpoint.pth')
model.load_state_dict(checkpoint['model_state_dict'])
optimizer.load_state_dict(checkpoint['optimizer_state_dict'])
epoch = checkpoint['epoch']
```

## 전이 학습

```python
import torchvision.models as models

# 사전 훈련된 모델 로드
model = models.resnet18(pretrained=True)

# 특정 레이어 동결
for param in model.parameters():
    param.requires_grad = False

# 마지막 레이어만 학습
model.fc = nn.Linear(512, 10)  # 클래스 수에 맞게 변경

# Fine-tuning (일부 레이어만 동결 해제)
for param in model.layer4.parameters():
    param.requires_grad = True
```

## 실전 CNN 예제

```python
class CNN(nn.Module):
    def __init__(self):
        super(CNN, self).__init__()
        self.conv_layers = nn.Sequential(
            nn.Conv2d(1, 32, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2),
            
            nn.Conv2d(32, 64, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2)
        )
        
        self.fc_layers = nn.Sequential(
            nn.Flatten(),
            nn.Linear(64 * 7 * 7, 128),
            nn.ReLU(),
            nn.Dropout(0.5),
            nn.Linear(128, 10)
        )
    
    def forward(self, x):
        x = self.conv_layers(x)
        x = self.fc_layers(x)
        return x
```

## GPU 활용

```python
# GPU 사용 가능 여부 확인
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')

# 모델과 데이터를 GPU로 이동
model = model.to(device)

for data, target in train_loader:
    data, target = data.to(device), target.to(device)
    output = model(data)
    loss = criterion(output, target)
    # ...

# 다중 GPU 사용
if torch.cuda.device_count() > 1:
    model = nn.DataParallel(model)
```

## 디버깅 팁

### 그래디언트 체크
```python
# 그래디언트가 제대로 흐르는지 확인
for name, param in model.named_parameters():
    if param.grad is not None:
        print(f'{name}: {param.grad.abs().mean():.4f}')
```

### 모델 구조 확인
```python
from torchsummary import summary

summary(model, input_size=(1, 28, 28))
```

### 그래디언트 클리핑
```python
# 그래디언트 폭발 방지
torch.nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)
```

## PyTorch vs Keras/TensorFlow

| 특징 | PyTorch | [[Keras]]/[[Tensorflow]] |
|------|---------|-------------------------|
| 학습 곡선 | 중간 | 쉬움 (Keras) |
| 연구 유연성 | 매우 높음 | 중간 |
| 프로덕션 배포 | TorchServe | TF Serving (성숙) |
| 커뮤니티 | 연구 중심 | 산업 + 연구 |
| 디버깅 | 쉬움 | 중간 |
| 동적 그래프 | 기본 지원 | Eager Execution |

## 주요 라이브러리

### torchvision
```python
from torchvision import transforms, models, datasets

# 이미지 전처리
transform = transforms.Compose([
    transforms.Resize(256),
    transforms.CenterCrop(224),
    transforms.ToTensor(),
    transforms.Normalize([0.485, 0.456, 0.406], 
                        [0.229, 0.224, 0.225])
])
```

### torchtext
```python
from torchtext.data import Field, TabularDataset, BucketIterator

# 텍스트 처리
TEXT = Field(tokenize='spacy', lower=True)
LABEL = Field(sequential=False)
```

### torchaudio
```python
import torchaudio

# 오디오 로드
waveform, sample_rate = torchaudio.load('audio.wav')
```

## 장단점

### 장점
- ✅ 매우 유연하고 Pythonic
- ✅ 디버깅이 쉬움
- ✅ 연구에 최적화
- ✅ 강력한 커뮤니티와 풍부한 자료
- ✅ 동적 그래프로 복잡한 모델 구현 용이

### 단점
- ❌ Keras보다 코드가 길고 복잡
- ❌ 프로덕션 배포 생태계가 TensorFlow보다 작음
- ❌ 초보자에게는 진입 장벽이 있음

## 관련 문서
- [[Keras]] - 고수준 딥러닝 API
- [[Tensorflow]] - 구글의 딥러닝 프레임워크
- [[Python]] - 프로그래밍 언어
- [[Machine Learning]] - 머신러닝 개념

## 참고 자료
- [PyTorch 공식 문서](https://pytorch.org/docs/)
- [PyTorch 튜토리얼](https://pytorch.org/tutorials/)
- [PyTorch Forums](https://discuss.pytorch.org/)
