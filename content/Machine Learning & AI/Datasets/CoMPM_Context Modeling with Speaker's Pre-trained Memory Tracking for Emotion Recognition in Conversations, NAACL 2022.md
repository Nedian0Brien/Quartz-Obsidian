#논문 

## 연구 목표
1. Commonsense를 이용해서, 즉 외부 데이터를 이용해서 감정 인식의 성능을 향상시키는 기존 연구가 있었음
2. 그러나 이는 한국어에서는 사용할 수 없는 방법임
3. CoMPM은 이러한 문제를 해결하기 위한 것

## Methods
- 두 가지 모듈을 제시함
	- CoM(context module)
		- 일반적으로 백본으로 가져와서 finetuning 시키는 pre-trained 모델을 말함
		- 입력으로는 대화의 발화들이 전부 들어감
	- PM(pre-trained memory module)
		- 이 또한 pre-trained 모델을 의미하나, CSK와 같이 context-independent 발화의 feature들을 담아내기 위함
		- ==즉, CommonSense Knowledge를 PLM(pre-trained language model)로 대체할 수 있다는 것==
			-> PLM은 general corpus로 학습되므로 CSK를 대체할 수 있음. 즉 구조화된 데이터의 역할을 할 수 있음
