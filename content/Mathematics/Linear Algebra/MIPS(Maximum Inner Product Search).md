#RAG 


[Maximum Inner Product Search. Retrieval이란 사전에 준비 된 데이터 내부에서 가장 적절한 것을… | by Hop | mojitok | Medium](https://medium.com/platfarm/mips-c1db30a3e73e)

'Retrieval' 이란 사전에 준비된 데이터 내부에서 가장 적절한 것을 찾는 것

이를 수행하기 위해 다양한 접근 방법이 있을 수 있는데, MIPS는 그 중 하나임

Query 정보를 [[Vectorization]](벡터화) 하여 사전에 벡터화되어 있는 데이터들 중 쿼리 벡터와의 내적([[inner product]]) 값이 가장 큰 것을 찾아주는 것

----

### 다른 알고리즘들과의 비교
- MIPS(Maximum Inner Product Search)
- [[NNS(Nearest Neighbor Search)]]
- [[MCSS(Maximum Cosine Similarity Search)]]

쿼리 벡터를 q, 답변 후보군을 V라고 할 때, 우리가 해야 할 일은 결국 V에 속해 있는 각 답변 벡터들 v_i 중에서 q와의 '상성이 가장 좋은' 것을 찾아내는 것.

이때 '좋은 상성'의 기준이 무엇인가? -> 이게 바로 위 알고리즘들

- q와 v_i의 내적이 클수록 좋다! -> MIPS
- q와 v_i의 유클리디안 거리(Euclidean Distance)가 작을수록 좋다! -> NNS
- q와 v_i의 코사인 유사도(Cosine Similarity)가 클수록 좋다! -> MCSS

#### 공식 살펴보기
1. MIPS
	![[Pasted image 20240126151754.png]]
2. NNS
	![[Pasted image 20240126151820.png]]
3. MCSS
	![[Pasted image 20240126151832.png]]

> 여기서 주목해야 할 부분은 세 경우 모두 q와 v_i의 내적이 클 수록 좋다는 공통점이 있지만, NNS와 MCSS는 v_i의 norm이 작아야 한다는 추가 제약이 있는 반면 MIPS의 경우는 그렇지 않다는 점.

모든 v_i  벡터들의 norm이 같다면 MCSS, NNS는 결국 MIPS와 같은 문제가 된다.

----

