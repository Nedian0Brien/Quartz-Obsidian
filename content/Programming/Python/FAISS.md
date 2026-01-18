#RAG #vector 

[16. FAISS에 대한 모든 것 - NLP AI (dajeblog.co.kr)](https://dajeblog.co.kr/16-faiss%EC%97%90-%EB%8C%80%ED%95%9C-%EB%AA%A8%EB%93%A0-%EA%B2%83/)


## FAISS란?

FAISS (Facebook AI Similarity Search)는 Facebook AI Research에서 개발한 고성능 벡터 유사도 검색 라이브러리입니다. 대규모 벡터 데이터베이스에서 빠르게 유사 벡터를 찾는 데 특화되어 있으며, RAG(Retrieval-Augmented Generation) 시스템의 핵심 구성 요소로 활용됩니다.

## 주요 특징

### 1. 빠른 검색 속도
- CPU와 GPU 모두 지원
- 수억 개의 벡터에서도 밀리초 단위 검색
- 메모리와 디스크 기반 인덱스 모두 지원

### 2. 다양한 인덱스 타입
- Flat (완전 탐색)
- IVF (Inverted File Index)
- PQ (Product Quantization)
- HNSW (Hierarchical Navigable Small World)

### 3. 확장성
- 분산 처리 지원
- 인덱스 샤딩
- 온라인/오프라인 인덱스 빌드

## 설치

```bash
# CPU 버전
pip install faiss-cpu

# GPU 버전
pip install faiss-gpu
```

## 기본 사용법

### 간단한 예제
```python
import numpy as np
import faiss

# 벡터 데이터 생성 (1000개, 128차원)
dimension = 128
n_vectors = 1000
vectors = np.random.random((n_vectors, dimension)).astype('float32')

# 인덱스 생성 (Flat L2)
index = faiss.IndexFlatL2(dimension)

# 벡터 추가
index.add(vectors)

# 검색 (상위 5개)
query = np.random.random((1, dimension)).astype('float32')
distances, indices = index.search(query, k=5)

print(f"가장 유사한 벡터들의 인덱스: {indices}")
print(f"거리: {distances}")
```

## 인덱스 종류

### 1. IndexFlatL2 (완전 탐색)
```python
# L2 거리 기반
index = faiss.IndexFlatL2(dimension)

# 내적(Inner Product) 기반
index = faiss.IndexFlatIP(dimension)
```

**특징:**
- ✅ 100% 정확도
- ✅ 구현이 간단
- ❌ 느린 속도 (벡터가 많을 때)
- ❌ 메모리 사용량 높음

### 2. IndexIVFFlat (역파일 인덱스)
```python
# 클러스터 개수
nlist = 100

# 양자화기 (클러스터링용)
quantizer = faiss.IndexFlatL2(dimension)

# IVF 인덱스 생성
index = faiss.IndexIVFFlat(quantizer, dimension, nlist)

# 학습 (클러스터링)
index.train(vectors)

# 벡터 추가
index.add(vectors)

# 검색 시 탐색할 클러스터 수
index.nprobe = 10
distances, indices = index.search(query, k=5)
```

**특징:**
- ✅ Flat보다 빠름
- ✅ 메모리 효율적
- ❌ 학습 필요
- ❌ 약간의 정확도 손실

### 3. IndexIVFPQ (Product Quantization)
```python
# 클러스터 개수
nlist = 100

# PQ 파라미터
m = 8  # 서브벡터 개수
n_bits = 8  # 각 서브벡터의 비트 수

quantizer = faiss.IndexFlatL2(dimension)
index = faiss.IndexIVFPQ(quantizer, dimension, nlist, m, n_bits)

# 학습 및 추가
index.train(vectors)
index.add(vectors)

# 검색
index.nprobe = 10
distances, indices = index.search(query, k=5)
```

**특징:**
- ✅ 매우 메모리 효율적 (압축)
- ✅ 빠른 검색
- ❌ 정확도 손실
- ❌ 학습 시간이 김

### 4. IndexHNSWFlat (그래프 기반)
```python
# HNSW 파라미터
M = 32  # 각 노드의 연결 수
index = faiss.IndexHNSWFlat(dimension, M)

# 벡터 추가 (학습 불필요)
index.add(vectors)

# 검색
distances, indices = index.search(query, k=5)
```

**특징:**
- ✅ 매우 빠른 검색
- ✅ 높은 정확도
- ❌ 메모리 사용량 높음
- ❌ 인덱스 빌드 시간이 김

## 인덱스 선택 가이드

```python
# 데이터 크기별 추천

# 1만 개 이하: Flat
if n_vectors < 10000:
    index = faiss.IndexFlatL2(dimension)

# 10만 개: IVF
elif n_vectors < 100000:
    index = faiss.IndexIVFFlat(quantizer, dimension, 100)

# 100만 개: IVF + PQ
elif n_vectors < 1000000:
    index = faiss.IndexIVFPQ(quantizer, dimension, 4096, 8, 8)

# 1000만 개 이상: IVF + PQ + 샤딩
else:
    # 분산 처리 필요
    pass
```

## GPU 사용

```python
# GPU 리소스 생성
res = faiss.StandardGpuResources()

# CPU 인덱스를 GPU로 변환
index_cpu = faiss.IndexFlatL2(dimension)
index_gpu = faiss.index_cpu_to_gpu(res, 0, index_cpu)

# GPU에서 벡터 추가 및 검색
index_gpu.add(vectors)
distances, indices = index_gpu.search(query, k=5)

# GPU에서 CPU로 변환 (저장용)
index_cpu = faiss.index_gpu_to_cpu(index_gpu)
```

## 인덱스 저장 및 로드

```python
# 인덱스 저장
faiss.write_index(index, "my_index.faiss")

# 인덱스 로드
index = faiss.read_index("my_index.faiss")
```

## ID 매핑

```python
# ID 매핑 추가
index = faiss.IndexFlatL2(dimension)
index = faiss.IndexIDMap(index)

# 커스텀 ID로 추가
ids = np.array([100, 200, 300]).astype('int64')
vectors_subset = vectors[:3]
index.add_with_ids(vectors_subset, ids)

# 검색 결과는 커스텀 ID 반환
distances, indices = index.search(query, k=3)
print(indices)  # [100, 200, 300] 형태
```

## 벡터 제거

```python
# IDMap이 있어야 가능
index = faiss.IndexFlatL2(dimension)
index = faiss.IndexIDMap(index)

# 벡터 추가
ids = np.arange(1000).astype('int64')
index.add_with_ids(vectors, ids)

# ID로 벡터 제거
remove_ids = np.array([10, 20, 30]).astype('int64')
index.remove_ids(remove_ids)
```

## 실전 RAG 예제

```python
import faiss
import numpy as np
from sentence_transformers import SentenceTransformer

# 임베딩 모델 로드
model = SentenceTransformer('all-MiniLM-L6-v2')

# 문서 임베딩
documents = [
    "Python은 프로그래밍 언어입니다.",
    "FAISS는 벡터 검색 라이브러리입니다.",
    "머신러닝은 AI의 한 분야입니다."
]

embeddings = model.encode(documents)
dimension = embeddings.shape[1]

# FAISS 인덱스 생성
index = faiss.IndexFlatL2(dimension)
index.add(embeddings.astype('float32'))

# 쿼리 검색
query = "벡터 검색 도구는?"
query_embedding = model.encode([query]).astype('float32')

# 상위 2개 검색
distances, indices = index.search(query_embedding, k=2)

print("검색 결과:")
for i, idx in enumerate(indices[0]):
    print(f"{i+1}. {documents[idx]} (거리: {distances[0][i]:.4f})")
```

## 성능 최적화

### 1. 배치 검색
```python
# 여러 쿼리를 한 번에 검색
queries = np.random.random((100, dimension)).astype('float32')
distances, indices = index.search(queries, k=5)
```

### 2. 병렬 처리
```python
# 인덱스 빌드 시 스레드 수 설정
faiss.omp_set_num_threads(8)
```

### 3. 메모리 매핑
```python
# 큰 인덱스를 메모리에 전부 로드하지 않고 사용
index = faiss.read_index("large_index.faiss", 
                        faiss.IO_FLAG_MMAP | faiss.IO_FLAG_READ_ONLY)
```

## 실전 팁

### 1. 정규화
```python
# 코사인 유사도를 위한 정규화
faiss.normalize_L2(vectors)

# L2 거리 인덱스 사용
index = faiss.IndexFlatL2(dimension)
index.add(vectors)
```

### 2. 하이브리드 검색
```python
# 여러 인덱스 결합
index1 = faiss.IndexFlatL2(dimension)
index2 = faiss.IndexIVFFlat(quantizer, dimension, nlist)

# 결과 병합
results1 = index1.search(query, k=10)
results2 = index2.search(query, k=10)

# 스코어 기반 재랭킹
```

### 3. 증분 업데이트
```python
# 새 벡터 추가
new_vectors = np.random.random((100, dimension)).astype('float32')
index.add(new_vectors)

# 주기적으로 인덱스 재빌드
if index.ntotal > threshold:
    index = rebuild_index(index)
```

## FAISS vs 대안

| 도구 | 장점 | 단점 | 사용 사례 |
|------|------|------|-----------|
| FAISS | 매우 빠름, GPU 지원 | 학습 필요 | 대규모 검색 |
| Annoy | 간단함, 메모리 효율 | GPU 미지원 | 중소규모 |
| ScaNN | 높은 정확도 | Google 종속 | 고정밀 검색 |
| Milvus | 분산 처리 | 복잡한 설정 | 프로덕션 |
| Qdrant | 필터링 강력 | 상대적으로 느림 | 복합 검색 |

## 장단점

### 장점
- ✅ 업계 최고 수준의 성능
- ✅ GPU 가속 지원
- ✅ 다양한 인덱스 옵션
- ✅ C++로 작성되어 빠름
- ✅ 대규모 데이터 처리 가능

### 단점
- ❌ 학습 곡선이 있음
- ❌ 메타데이터 필터링 미지원
- ❌ 실시간 업데이트 제한적
- ❌ 분산 처리 지원 제한적

## 관련 문서
- [[Python]] - 프로그래밍 언어
- [[Machine Learning]] - 머신러닝
- [[Vector Search]] - 벡터 검색 개념

## 참고 자료
- [FAISS GitHub](https://github.com/facebookresearch/faiss)
- [FAISS Wiki](https://github.com/facebookresearch/faiss/wiki)
