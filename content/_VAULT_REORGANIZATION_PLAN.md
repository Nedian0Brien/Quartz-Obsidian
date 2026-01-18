# Vault 정리 계획

## 정리 시작 시간
2025-01-03

## 목표
- 루트에 산재된 150+ 파일을 주제별로 체계적으로 정리
- 임시 파일 및 중복 파일 정리
- 이미지 파일 통합 관리

## 새로운 폴더 구조

### 1. Machine Learning & AI/
- Fundamentals/ - 기초 이론
- Models/ - 모델 구조
- Language Models/ - 언어 모델
- Techniques/ - 기법
- Neural Networks/ - 신경망 구조
- Datasets/ - 데이터셋
- Evaluation/ - 평가 지표
- XAI/ - 설명가능 AI

### 2. Computer Science/
- Operating Systems/
- Algorithms/
- OOP/

### 3. Programming/
- Python/
- Java/
- C/
- Git/

### 4. Data Engineering/
- Databases/
- ETL & Pipelines/
- Storage/

### 5. DevOps/
- Kubernetes/
- Cloud/

### 6. Mathematics/
- Statistics/
- Linear Algebra/

### 7. _Archive/
- 임시 파일, 정리 대기

## 작업 단계

### Phase 1: 폴더 구조 생성 ✓ (진행 중)
- [ ] Machine Learning & AI 하위 폴더
- [ ] Computer Science 하위 폴더
- [ ] Programming 하위 폴더
- [ ] Data Engineering 하위 폴더
- [ ] DevOps 하위 폴더
- [ ] Mathematics 하위 폴더
- [ ] _Archive 폴더

### Phase 2: AI 폴더 정리
- [ ] AI/구성 2 → Machine Learning & AI/Neural Networks/로 이동
- [ ] AI/기법 2의 중복 파일 확인 및 병합
- [ ] AI/LM → Machine Learning & AI/Language Models/로 이동
- [ ] AI/기법 → Machine Learning & AI/Techniques/로 이동

### Phase 3: 루트 파일 분류 및 이동
- [ ] ML/AI 관련 파일 이동
- [ ] CS 관련 파일 이동
- [ ] Programming 관련 파일 이동
- [ ] Data Engineering 관련 파일 이동
- [ ] DevOps 관련 파일 이동
- [ ] Mathematics 관련 파일 이동

### Phase 4: 이미지 및 임시 파일 정리
- [ ] Pasted image 파일들 Images/로 이동
- [ ] 무제/Untitled 파일들 _Archive/로 이동

### Phase 5: 최종 검토
- [ ] 링크 깨짐 확인
- [ ] 중복 파일 최종 확인
- [ ] 폴더 구조 최적화

## 파일 이동 목록

### Machine Learning & AI/
#### Fundamentals/
- Gradient.md
- Gradient Descent.md
- Full-batch Gradient Descent.md
- Mini-batch Gradient Descent.md
- Stochastic Gradient Descent.md
- Cost Function.md
- Loss Function.md
- Mean Squared Error.md
- Negative Log-Likelihood, NLL.md
- Partial Derivative.md
- Overfitting.md
- Underfitting.md
- Regularization.md
- Variance.md
- Residual.md
- 마르코프 속성(Markov property).md

#### Models/
- Convolutional Neural Network.md
- Autoregressive Model.md
- GAN.md
- Decision Tree.md
- Random Forest.md
- 오토인코더.md

#### Language Models/
- (AI/LM 폴더 전체 내용)

#### Techniques/
- Supervised Learning.md
- Unsupervised Learning.md
- Reinforcement Learning.md
- RLHF.md
- Embedding.md
- Vectorization.md
- 그래프 기반 임베딩.md
- Beam Search.md
- 하이퍼파라미터 튜닝.md
- (AI/기법 폴더 내용)

#### Neural Networks/
- (AI/구성 2 폴더 전체 내용)

#### Datasets/
- MELD.md
- MELD_A Multimodal Multi-Party Dataset for Emotion Recognition in Conversations, ACL 2019.md
- COSMIC_COmmonSense knowledge for eMotion Identification in Conversations (Findings of EMNLP 2020).md
- CoMPM_Context Modeling with Speaker's Pre-trained Memory Tracking for Emotion Recognition in Conversations, NAACL 2022.md
- FEVER Task.md
- MSMARCO Task.md
- 머신러닝 데이터셋.md

#### Evaluation/
- BLEU.md

#### XAI/
- XAI.md
- SHAP(SHapley Additive exPlanations).md
- 샤플리 값(Shapley values).md

#### Other AI/
- Adversarial Attack.md
- Evasion Attack.md
- Exploratory Attack.md
- Poisoning Attack.md
- Perturbation.md
- Hallucination.md
- 감정 인식.md
- 데이터 전처리.md

### Computer Science/
#### Operating Systems/
- Operating System.md
- OSTEP.md
- CPU Scheduling.md
- CPU Virtualization.md
- Memory Virtualization.md
- Virtualization.md
- Virtual Address Space.md
- File System.md
- System Call.md
- Concurrency.md
- Multi-Thread.md
- Persistence.md
- Policy.md
- Mechanism.md

#### Algorithms/
- (현재 없음, 향후 추가 가능)

#### OOP/
- Object-Oriented Programming.md

### Programming/
#### Python/
- Python.md
- Keras.md
- Pytorch.md
- Tensorflow.md
- FAISS.md
- 예외 처리.md

#### Java/
- JAVA.md

#### C/
- C Language.md
- Format Specifier.md
- 가변 인자 문법.md

#### Git/
- Git.md
- Git Branch 전략.md
- Git Stash.md
- Git-Flow.md
- Github.md
- Github-Flow.md
- Gitlab Flow.md
- Trunk-based.md
- Branch.md

### Data Engineering/
#### Databases/
- Database.md
- RDB.md
- NoSQL.md
- MongoDB.md
- Redis.md

#### ETL & Pipelines/
- ETL.md
- Apache Airflow.md
- Kafka.md
- EDA.md

#### Storage/
- 데이터 레이크.md
- 데이터 웨어하우스.md

### DevOps/
#### Kubernetes/
- Kubernetes.md

#### Cloud/
- 아마존 EC2.md
- Apple.md
- Google.md
- Microsoft.md
- OpenAI.md

### Mathematics/
#### Statistics/
- Regression Analysis.md
- Linear Regression.md
- Regression Coefficient.md
- Least Square Method.md
- 베이즈 정리.md
- 베이지안 상태공간 모형.md
- 베이지안 최적화.md
- 베이지안 추론(Bayesian inference).md
- 사전 확률(prior probability).md
- 사후 확률(posterior probability).md
- 조건부 확률.md
- 주변 확률(marginal probability).md
- 상태 변수.md
- population.md
- sample.md

#### Linear Algebra/
- Vector Similarity.md
- Cosine Similarity.md
- Euclidean Distance.md
- Manhattan Distance.md
- Minkowski Distance.md
- Levenshtein Distance.md
- inner product.md
- MCSS(Maximum Cosine Similarity Search).md
- MIPS(Maximum Inner Product Search).md
- NNS(Nearest Neighbor Search).md

### _Archive/
- 무제.md
- 무제 1.md
- 무제 2.md
- 무제 3.md
- 무제 4.md
- 무제 파일.md
- 무제 파일 1.md
- 무제 파일 2.md
- 무제 파일 3.md
- 무제 파일 4.md
- 무제 파일 5.md
- 무제 파일 6.md
- 무제 파일 7.md
- 무제 파일.canvas
- 무제.base
- Untitled.md
- Untitled 1.md
- Untitled Kanban.md
- Untitled.canvas
- asdf.md
- asdkaskdf.md
- AI/Untitled.md

### Other (분류 필요)
- Computer Science.md
- Data Science.md
- Error.md
- Full-Stack.md
- IT Terminology.md
- Programming Languages.md
- Tech Companies.md
- tech stack.md
- Vault.md
- 다중공선성.md
- 프로젝트 관련 논문 찾기.md
- 프로젝트 관련 데이터 찾기.md
- 캔버스 1.canvas

## 진행 상황
- [ ] Phase 1 시작


## ✅ Phase 1 완료: 폴더 구조 생성 완료!

생성된 폴더:
- ✅ Machine Learning & AI/
  - ✅ Fundamentals/
  - ✅ Models/
  - ✅ Language Models/
  - ✅ Techniques/
  - ✅ Neural Networks/
  - ✅ Datasets/
  - ✅ Evaluation/
  - ✅ XAI/
- ✅ Computer Science/
  - ✅ Operating Systems/
  - ✅ OOP/
- ✅ Programming/
  - ✅ Python/
  - ✅ Java/
  - ✅ C/
  - ✅ Git/
- ✅ Data Engineering/
  - ✅ Databases/
  - ✅ ETL & Pipelines/
  - ✅ Storage/
- ✅ DevOps/
  - ✅ Kubernetes/
  - ✅ Cloud/
- ✅ Mathematics/
  - ✅ Statistics/
  - ✅ Linear Algebra/
- ✅ _Archive/

## 📝 다음 단계: 파일 이동 가이드

옵시디언에서 파일을 이동하는 방법:
1. 파일을 드래그 앤 드롭으로 새 폴더로 이동
2. 또는 파일 우클릭 → "Move file to..." 선택

### 우선순위 1: AI 폴더 정리
**즉시 이동할 파일들:**

#### AI/구성 2/ → Machine Learning & AI/Neural Networks/
- Activation Function.md
- Artificial Neural Network.md
- Attention Mechanism.md
- Deep Neural Network.md
- Feed-Forward Neural Network.md
- GRU.md
- LSTM.md
- Perceptron.md
- Recurrent Neural Network.md
- Transformer.md
- Vanishing Gradient.md

#### AI/LM/ → Machine Learning & AI/Language Models/
- BARD.md
- BERT.md
- BioBERT.md
- ChatGPT.md
- GPT.md
- GPT4.md
- Kullm.md
- LLM.md
- LM.md
- Llama.md
- PharmBERT.md
- 한국어 LLM.md

#### AI/기법/ → Machine Learning & AI/Techniques/
- Deep Learning.md
- Embedding.md
- Foundation Model.md
- LoRA.md
- Machine Learning.md
- Model Fine-Tuning.md
- Multi-head Attention.md
- PEFT.md
- QLoRA.md
- SVM.md

**주의:** AI/기법 2/의 LoRA.md, QLoRA.md는 중복 확인 후 처리

### 우선순위 2: 루트의 ML/AI 파일들

#### → Machine Learning & AI/Fundamentals/
루트에서 이동:
- Gradient.md
- Gradient Descent.md
- Full-batch Gradient Descent.md
- Mini-batch Gradient Descent.md
- Stochastic Gradient Descent.md
- Cost Function.md
- Loss Function.md
- Mean Squared Error.md
- Negative Log-Likelihood, NLL.md
- Partial Derivative.md
- Overfitting.md
- Underfitting.md
- Regularization.md
- Variance.md
- Residual.md
- 마르코프 속성(Markov property).md

#### → Machine Learning & AI/Models/
- Convolutional Neural Network.md
- Autoregressive Model.md
- GAN.md
- Decision Tree.md
- Random Forest.md
- 오토인코더.md

#### → Machine Learning & AI/Techniques/
- Supervised Learning.md
- Unsupervised Learning.md
- Reinforcement Learning.md
- RLHF.md
- Vectorization.md
- 그래프 기반 임베딩.md
- Beam Search.md
- 하이퍼파라미터 튜닝.md

#### → Machine Learning & AI/Datasets/
- MELD.md
- MELD_A Multimodal Multi-Party Dataset for Emotion Recognition in Conversations, ACL 2019.md
- COSMIC_COmmonSense knowledge for eMotion Identification in Conversations (Findings of EMNLP 2020).md
- CoMPM_Context Modeling with Speaker's Pre-trained Memory Tracking for Emotion Recognition in Conversations, NAACL 2022.md
- FEVER Task.md
- MSMARCO Task.md
- 머신러닝 데이터셋.md

#### → Machine Learning & AI/Evaluation/
- BLEU.md

#### → Machine Learning & AI/XAI/
- XAI.md
- SHAP(SHapley Additive exPlanations).md
- 샤플리 값(Shapley values).md

### 우선순위 3: 기타 루트 파일들

#### → Computer Science/Operating Systems/
- Operating System.md
- OSTEP.md
- CPU Scheduling.md
- CPU Virtualization.md
- Memory Virtualization.md
- Virtualization.md
- Virtual Address Space.md
- File System.md
- System Call.md
- Concurrency.md
- Multi-Thread.md
- Persistence.md
- Policy.md
- Mechanism.md

#### → Computer Science/OOP/
- Object-Oriented Programming.md

#### → Programming/Python/
- Python.md
- Keras.md
- Pytorch.md
- Tensorflow.md
- FAISS.md
- 예외 처리.md

#### → Programming/Java/
- JAVA.md

#### → Programming/C/
- C Language.md
- Format Specifier.md
- 가변 인자 문법.md

#### → Programming/Git/
- Git.md
- Git Branch 전략.md
- Git Stash.md
- Git-Flow.md
- Github.md
- Github-Flow.md
- Gitlab Flow.md
- Trunk-based.md
- Branch.md

#### → Data Engineering/Databases/
- Database.md
- RDB.md
- NoSQL.md
- MongoDB.md
- Redis.md

#### → Data Engineering/ETL & Pipelines/
- ETL.md
- Apache Airflow.md
- Kafka.md
- EDA.md

#### → Data Engineering/Storage/
- 데이터 레이크.md
- 데이터 웨어하우스.md

#### → DevOps/Kubernetes/
- Kubernetes.md

#### → DevOps/Cloud/
- 아마존 EC2.md
- Apple.md
- Google.md
- Microsoft.md
- OpenAI.md

#### → Mathematics/Statistics/
- Regression Analysis.md
- Linear Regression.md
- Regression Coefficient.md
- Least Square Method.md
- 베이즈 정리.md
- 베이지안 상태공간 모형.md
- 베이지안 최적화.md
- 베이지안 추론(Bayesian inference).md
- 사전 확률(prior probability).md
- 사후 확률(posterior probability).md
- 조건부 확률.md
- 주변 확률(marginal probability).md
- 상태 변수.md
- population.md
- sample.md

#### → Mathematics/Linear Algebra/
- Vector Similarity.md
- Cosine Similarity.md
- Euclidean Distance.md
- Manhattan Distance.md
- Minkowski Distance.md
- Levenshtein Distance.md
- inner product.md
- MCSS(Maximum Cosine Similarity Search).md
- MIPS(Maximum Inner Product Search).md
- NNS(Nearest Neighbor Search).md

### 우선순위 4: 이미지 정리
#### Images/로 이동:
- Pasted image 20230922091847.png
- Pasted image 20230922092226.png
- Pasted image 20240126151754.png
- Pasted image 20240126151820.png
- Pasted image 20240126151832.png
- Pasted image 20240126152609.png
- Pasted image 20240126155616.png
- Pasted image 20240126155834.png
- Pasted image 20240126155933.png
- Pasted image 20240126160017.png
- Pasted image 20240126160048.png
- Pasted image 20240126160156.png
- Pasted image 20240126160319.png
- Pasted image 20240126160555.png

### 우선순위 5: 임시 파일 아카이브
#### _Archive/로 이동:
- 무제.md
- 무제 1.md
- 무제 2.md
- 무제 3.md
- 무제 4.md
- 무제 파일.md
- 무제 파일 1.md
- 무제 파일 2.md
- 무제 파일 3.md
- 무제 파일 4.md
- 무제 파일 5.md
- 무제 파일 6.md
- 무제 파일 7.md
- 무제 파일.canvas
- 무제.base
- Untitled.md
- Untitled 1.md
- Untitled Kanban.md
- Untitled.canvas
- asdf.md
- asdkaskdf.md
- AI/Untitled.md

### 분류 보류 (추후 검토 필요):
- Computer Science.md (인덱스 파일로 활용 가능)
- Data Science.md (인덱스 파일로 활용 가능)
- Error.md (Programming/ 또는 Computer Science/로 이동 고려)
- Full-Stack.md (Programming/로 이동 고려)
- IT Terminology.md (루트 유지 또는 별도 References/ 폴더 생성)
- Programming Languages.md (Programming/로 이동 고려)
- Tech Companies.md (루트 유지 또는 DevOps/로 이동)
- tech stack.md (DevOps/ 또는 Programming/로 이동)
- Vault.md (루트 유지 - 볼트 설정 문서)
- 다중공선성.md (Mathematics/Statistics/로 이동 고려)
- 프로젝트 관련 논문 찾기.md (루트 유지 또는 별도 Projects/ 폴더)
- 프로젝트 관련 데이터 찾기.md (루트 유지 또는 별도 Projects/ 폴더)
- 캔버스 1.canvas (내용 확인 필요)
- 데이터 전처리.md (Machine Learning & AI/ 또는 Data Engineering/로)
- 감정 인식.md (Machine Learning & AI/로)
- Adversarial Attack.md, Evasion Attack.md, Exploratory Attack.md, Poisoning Attack.md, Perturbation.md (Machine Learning & AI/로)
- Hallucination.md (Machine Learning & AI/Language Models/로)

## 💡 작업 팁
1. 한 번에 하나의 폴더씩 정리하세요
2. AI 폴더부터 시작하면 가장 큰 효과를 볼 수 있습니다
3. 이동 후에는 링크가 자동으로 업데이트되는지 확인하세요
4. 불확실한 파일은 _Archive/에 두고 나중에 판단하세요
