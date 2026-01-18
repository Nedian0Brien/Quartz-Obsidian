#논문 

#### 상식을 이용해 대화 속 감정 인식의 성능 높이기

> Findings는 메인 컨퍼런스는 아니지만 아쉽게 떨어진 좋은 논문들을 의미한다고 보면 됨

- 이 논문은 DialogueRNN 이라는 다른 연구와 비슷한 방식으로 진행이 됨
- 논문의 핵심은 speaker tracking, listener tracking, context tracking 세 가지 요소
	- Speaker는 화자의 감정 상태가 업데이트 되는 state
	- Listener는 다른 사람의 감정 상태가 업데이트 되는 state
	- Context는 이를 통합하는 state라고 생각하면 된다.

- 여기서 사용되는 feature vector는 2가지가 있다
	1) RoBERTa 모델을 문장 단위의 감정 분석에 학습을 한다 (기존 데이터)
		- 이 모델로 발화의 feature를 뽑는 것
		- Context independent feature라고 명명한다.
		- 세부적으로는, 마지막 4개의 layers의 activations를 추출
		- 이 4개의 vectors을 평균을 취하여 얻는다.
			-> 왜 이렇게 했는가? 논리적인 근거는 없음. 실험적으로 이렇게 했을 때 성능이 가장 높게 나온 것.
	2) commonsense feature로 ATOMIC이라는 상식 그래프에 해당하는 데이터세트로 학습된 모델의 feature
		- 감정을 인식할 발화를 말한 사람이 speaker가 되고 다른 사람들은 listener가 됨.
		- ==직관적인 개념은, 서로의 발화가 서로의 state에 연락을 준다는 것!==

#### 논문 핵심)
- CommonSense를 이용해 감정 인식 모델의 성능을 향상시킴
- Speaker, Listener, Context 세 가지의 벡터를 사용한다

