
Python은 1991년 귀도 반 로섬(Guido van Rossum)이 개발한 고급 프로그래밍 언어입니다. 간결하고 읽기 쉬운 문법으로 초보자부터 전문가까지 널리 사용됩니다.

## 주요 특징

### 1. 간결하고 읽기 쉬운 문법
- 들여쓰기(indentation)로 코드 블록을 구분
- 세미콜론(;) 불필요
- 직관적인 키워드 사용

### 2. 동적 타이핑
```python
x = 10        # 정수
x = "hello"   # 문자열로 재할당 가능
x = [1, 2, 3] # 리스트로 재할당 가능
```

### 3. 인터프리터 언어
- 컴파일 과정 없이 바로 실행
- REPL(Read-Eval-Print Loop) 지원으로 대화형 프로그래밍 가능

### 4. 다양한 패러다임 지원
- 절차적 프로그래밍
- 객체지향 프로그래밍 ([[Object-Oriented Programming]])
- 함수형 프로그래밍

## 기본 문법

### 변수와 자료형
```python
# 기본 자료형
integer_var = 42
float_var = 3.14
string_var = "Python"
boolean_var = True
list_var = [1, 2, 3, 4, 5]
tuple_var = (1, 2, 3)
dict_var = {"name": "Dennis", "age": 25}
set_var = {1, 2, 3, 4, 5}
```

### 제어문
```python
# 조건문
if x > 0:
    print("양수")
elif x == 0:
    print("영")
else:
    print("음수")

# 반복문
for i in range(5):
    print(i)

while condition:
    # 반복 실행
    pass
```

### 함수 정의
```python
def greet(name, greeting="Hello"):
    """인사 메시지를 반환하는 함수"""
    return f"{greeting}, {name}!"

# 람다 함수
square = lambda x: x ** 2
```

### 클래스와 객체
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def introduce(self):
        return f"안녕하세요, 저는 {self.name}입니다."

# 객체 생성
person = Person("Dennis", 25)
```

## 주요 라이브러리

### 표준 라이브러리
- `os`, `sys` - 운영체제 인터페이스
- `datetime` - 날짜와 시간 처리
- `json` - JSON 데이터 처리
- `re` - 정규표현식
- `collections` - 고급 자료구조

### 데이터 과학
- `numpy` - 수치 연산
- `pandas` - 데이터 분석
- `matplotlib`, `seaborn` - 데이터 시각화
- `scikit-learn` - 전통적인 머신러닝

### 머신러닝/딥러닝
- [[Tensorflow]] - Google의 딥러닝 프레임워크
- [[Pytorch]] - Facebook의 딥러닝 프레임워크
- [[Keras]] - 고수준 신경망 API

### 웹 개발
- `Flask` - 마이크로 웹 프레임워크
- `Django` - 풀스택 웹 프레임워크
- `FastAPI` - 고성능 API 프레임워크

## 가상환경

Python 프로젝트마다 독립적인 패키지 환경을 관리하기 위해 가상환경을 사용합니다.

### venv (내장)
```bash
# 가상환경 생성
python -m venv myenv

# 활성화 (Windows)
myenv\Scripts\activate

# 활성화 (Linux/Mac)
source myenv/bin/activate

# 비활성화
deactivate
```

### conda
```bash
# 가상환경 생성
conda create -n myenv python=3.10

# 활성화
conda activate myenv

# 비활성화
conda deactivate
```

## 패키지 관리

### pip
```bash
# 패키지 설치
pip install package_name

# 특정 버전 설치
pip install package_name==1.2.3

# requirements.txt로 일괄 설치
pip install -r requirements.txt

# 패키지 목록 저장
pip freeze > requirements.txt
```

## Python 버전

- **Python 2.x**: 2020년 공식 지원 종료
- **Python 3.x**: 현재 주류 버전
  - Python 3.9: 타입 힌팅 개선
  - Python 3.10: 구조적 패턴 매칭
  - Python 3.11: 성능 대폭 개선
  - Python 3.12: 최신 안정 버전

## PEP (Python Enhancement Proposal)

Python의 개선 제안 문서로, 새로운 기능과 표준을 정의합니다.

- **PEP 8**: 코드 스타일 가이드
- **PEP 20**: The Zen of Python (Python의 철학)
- **PEP 484**: 타입 힌팅
- **PEP 257**: Docstring 규약

## 관련 문서
- [[예외 처리]] - Python의 에러 핸들링
- [[Keras]] - 딥러닝 고수준 API
- [[Pytorch]] - 연구용 딥러닝 프레임워크
- [[Tensorflow]] - 프로덕션 딥러닝 프레임워크
- [[FAISS]] - 벡터 유사도 검색 라이브러리

## 참고 자료
- [Python 공식 문서](https://docs.python.org/3/)
- [PEP 8 스타일 가이드](https://peps.python.org/pep-0008/)
- [Python Package Index (PyPI)](https://pypi.org/)


[[예외 처리]]
