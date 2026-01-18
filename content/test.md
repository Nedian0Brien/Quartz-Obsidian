안녕하세요! AI 논문 스터디Thought Partner Gemini입니다. 텍스트와 복잡한 계층 구조를 가진 표가 혼합된 하이브리드 문서에서 정보를 정확하게 추출하고 추론하는 것은 RAG 시스템의 난제 중 하나였죠. 오늘 소개해 드릴 논문은 이 문제를 해결하기 위해 제안된 **HD-RAG** 프레임워크와 새로운 벤치마크 데이터셋에 관한 연구입니다. 1

---

## **HD-RAG: Retrieval-Augmented Generation for Hybrid Documents Containing Text and Hierarchical Tables**

**(HD-RAG: 텍스트 및 계층적 표를 포함하는 하이브리드 문서를 위한 검색 증강 생성)** 2

---

## 1. 📝 논문 내용 요약 및 핵심 정리

- **저자:** Chi Zhang, Qiyang Chen 3333
    
- **주요 키워드:** Information Retrieval, Question Answering, Retrieval-Augmented Generation, Hybrid Documents, Hierarchical Tables 4
    

### **Abstract**

> "With the rapid advancement of large language models (LLMs), Retrieval-Augmented Generation (RAG) effectively combines LLMs' generative capabilities with external retrieval-based information. 5The Hybrid Document RAG task aims to integrate textual and hierarchical tabular data for more comprehensive retrieval and generation in complex scenarios. 6However, there is no existing dataset specifically designed for this task that includes both text and tabular data. 7Additionally, existing methods struggle to retrieve relevant tabular data and integrate it with text. 8Semantic similarity-based retrieval lacks accuracy, while table-specific methods fail to handle complex hierarchical structures effectively. 9Furthermore, the QA task requires complex reasoning and calculations, further complicating the challenge. 10In this paper, we propose a new large-scale dataset, DocRAGLib, specifically designed for the question answering (QA) task scenario under Hybrid Document RAG. 11To tackle these challenges, we introduce HD-RAG, a novel framework that incorporates a row-and-column level (RCL) table representation, employs a two-stage process combining ensemble and LLM-based retrieval, and integrates RECAP, which is designed for multi-step reasoning and complex calculations in Document-QA tasks. 12We conduct comprehensive experiments with DocRAGLib, showing that HD-RAG outperforms existing baselines in both retrieval accuracy and QA performance, demonstrating its effectiveness." 13

[한국어 번역]

대규모 언어 모델(LLM)의 급격한 발전으로 검색 증강 생성(RAG)은 LLM의 생성 능력과 외부 검색 기반 정보를 효과적으로 결합하고 있습니다. 14하이브리드 문서 RAG 작업은 복잡한 시나리오에서 보다 포괄적인 검색 및 생성을 위해 텍스트와 계층적 표 데이터를 통합하는 것을 목표로 합니다. 15그러나 텍스트와 표 데이터를 모두 포함하여 이 작업에 특화된 기존 데이터셋은 존재하지 않습니다. 16또한 기존 방법들은 관련 표 데이터를 검색하고 이를 텍스트와 통합하는 데 어려움을 겪고 있습니다. 17의미적 유사성 기반 검색은 정확도가 부족하며, 표 특화 방법들은 복잡한 계층 구조를 효과적으로 처리하지 못합니다. 18더욱이 질의응답(QA) 작업은 복잡한 추론과 계산을 요구하여 도전을 더욱 가중시킵니다. 19본 논문에서는 하이브리드 문서 RAG 환경의 QA 작업을 위해 특별히 설계된 새로운 대규모 데이터셋인 DocRAGLib을 제안합니다. 20이러한 문제를 해결하기 위해, 행 및 열 수준(RCL) 표 표현을 포함하고, 앙상블 및 LLM 기반 검색을 결합한 2단계 프로세스를 채택하며, 다단계 추론 및 복잡한 계산을 위해 설계된 RECAP을 통합한 새로운 프레임워크인 HD-RAG를 소개합니다. 21DocRAGLib을 통한 종합적인 실험 결과, HD-RAG가 검색 정확도와 QA 성능 모두에서 기존 베이스라인을 능가함을 입증했습니다. 22

---

### **연구 요약 및 핵심 발견점**

본 연구는 텍스트와 계층적 표가 혼재된 하이브리드 문서에서 정보를 찾고 답하는 **Hybrid Document RAG** 문제를 해결하는 데 집중합니다. 23기존 RAG 방식은 단순히 텍스트 조각(Chunk) 간의 유사도만 따지기 때문에, 표 내부의 복잡한 계층적 관계를 놓치거나 수치 계산이 포함된 질문에 취약했습니다. 24

이를 해결하기 위해 연구진은 세 가지 핵심 요소를 제안합니다. 첫째, 2,178개의 문서와 4,468개의 QA 쌍으로 구성된 대규모 데이터셋 **DocRAGLib**을 구축하여 연구의 기반을 마련했습니다. 25둘째, 표의 행과 열을 계층적 경로로 표현하는 **H-RCL(Hierarchical Row-and-Column Level)** 요약 방식을 제안하여 표의 구조적 정보를 보존했습니다. 2626셋째, **RECAP**이라는 5단계 추론 프레임워크를 도입하여 복잡한 수학적 계산과 논리적 추론을 체계화했습니다. 2727실험 결과, HD-RAG는 기존 모델 대비 검색 성능(Hit@1)에서 약 40% 이상의 획기적인 향상을 보였습니다. 2828

### **기존 접근법의 한계와 HD-RAG의 차별점**

기존의 RAG 기술은 주로 텍스트 위주로 발전해 왔으며, 표를 다루더라도 평면적인(Flat) 구조만 지원하는 경우가 많았습니다. 29복잡한 금융 보고서처럼 계층 구조가 얽힌 표의 경우, 단순히 텍스트로 변환하면 행과 열의 관계가 깨져서 잘못된 정보를 추출하게 됩니다. 30**HD-RAG**는 표의 각 셀이 가지는 계층적 경로(Header Path)를 명시적으로 보존함으로써, 정보의 유실 없이 정교한 데이터 접근을 가능하게 한다는 점에서 강력한 차별점을 가집니다. 3131

---

## 2. 📑 목차 및 내용 정리

### 📂 1. 데이터의 한계 극복: DocRAGLib 데이터셋 구축

- **하이브리드 문서 전용 데이터셋의 부재**: 기존 연구들은 단일 문서 QA나 평면적 표에 국한되어 대규모 하이브리드 문서 코퍼스를 다루는 데 한계가 있었습니다. 32
    
- **DocRAGLib의 구성**: MultiHiertt 및 HiTab 등 검증된 소스에서 2,178개의 문서를 수집하고 정제하여, 텍스트와 계층적 표가 결합된 4,468개의 QA 쌍을 생성했습니다. 33333333
    
- **복잡성 지표**: 데이터셋의 40.2%가 텍스트와 표 모두를 증거로 사용해야 답할 수 있으며, 34.29%는 정밀한 소수점 계산을 요구합니다. 34343434
    

### 🏗️ 2. 구조의 보존: Corpus Construction Module

- **계층적 행-열 수준(H-RCL) 요약**: 표의 계층 구조를 무시하는 기존 요약 방식과 달리, 행과 열의 헤더 경로를 추적하여 각 데이터 셀의 맥락을 완벽히 유지합니다. 35353535
    
- **표 표현 방식의 진화**: 단순 표 단위 요약(Table Level)에서 일반 RCL을 거쳐, 최종적으로 계층 구조를 반영한 H-RCL 방식으로 발전시켜 정보 손실을 최소화했습니다. 36363636
    
- **문장 단위 텍스트 처리**: 텍스트 부분은 문장 수준으로 분할하여 검색 효율성을 높이고 관련 정보를 정밀하게 추출할 수 있도록 구성했습니다. 37
    

### 🔍 3. 정밀한 탐색: Two-Stage Retrieval Module

- **앙상블 검색 단계(Stage 1)**: 키워드 매칭에 강한 **BM25**와 의미적 맥락을 파악하는 **Embedding** 기반 검색을 결합하여 고품질의 후보 문서를 선별합니다. 38383838
    
- **LLM 기반 재검색 단계(Stage 2)**: 1단계에서 걸러진 후보들 중 LLM이 직접 질문과의 논리적 연관성을 검토하여 가장 관련성이 높은 단 하나의 문서를 최종 확정합니다. 39
    
- **토큰 효율성 최적화**: 문서 전체를 LLM에 넣는 대신, 질문과 가장 유사한 정보 조각(Chunk)들만 재조합하여 입력함으로써 토큰 한계 문제를 해결했습니다. 40404040
    

### 🧠 4. 체계적 추론: RECAP QA Inference Module

- **RECAP 전략 도입**: 질문 재진술(Restate), 데이터 추출(Extract), 계산(Compute), 답변(Answer), 수식 제시(Present)의 5단계를 거쳐 답변의 정확도를 높입니다. 41
    
- **외부 계산 도구 활용**: LLM의 연산 오류를 방지하기 위해 추론 과정에서 도출된 수식을 외부 계산기(Calculator)로 실행하여 결과를 산출합니다. 42
    
- **추론 경로의 일관성**: 하나의 논리적 경로 내에서 수식 추상화와 언어적 설명을 동시에 진행하여 기존의 반복 생성 방식보다 효율적입니다. 43
    

### 📊 5. 성능 검증 및 실험 결과

- **검색 성능**: HD-RAG는 Hit@1 지표에서 0.5410을 기록하여, Standard RAG(0.0159)나 LangChain(0.2390) 등의 베이스라인을 압도했습니다. 444444
    
- **QA 정확도**: GPT-4o 기반 실험에서 Exact Match(EM) 점수가 0.6466에 달해, 다른 프롬프트 전략(CoT, PoT 등)보다 뛰어난 성능을 입증했습니다. 454545
    
- **확장성(Scalability)**: 문서 코퍼스 크기가 커져도 성능 저하 폭이 가장 적어 대규모 데이터 환경에서도 견고함을 보였습니다. 46
    

---

## 3. 💡 논문에서 반드시 알아야 하는 내용

### **핵심 기술: H-RCL (Hierarchical Row-and-Column Level) Table Summary**

기존 RAG는 표를 단순 텍스트로 펼쳐버려 구조적 맥락을 잃습니다. HD-RAG는 표의 각 셀을 좌표가 아닌 **'헤더의 경로'**로 정의합니다.

- **수식적 표현**: 계층적 표 $T$는 행 헤더 구조 $H_l$, 열 헤더 구조 $H_t$, 그리고 데이터 $d$로 정의됩니다. 47
    
- **경로 정의**: 특정 셀 $d_{ij}$를 찾기 위해 좌측 헤더 경로 $P_l(i)$와 상단 헤더 경로 $P_t(j)$를 결합합니다. 48
    
    - 예: $P_l(3) = h_l^1(1) \rightarrow h_l^2(3)$ (첫 번째 레벨의 1번 헤더에서 두 번째 레벨의 3번 헤더로 이동) 49
        
- **요약 생성**: LLM은 이러한 경로 정보를 바탕으로 각 행($S_{row}$)과 열($S_{col}$)에 대한 요약을 생성하며, 이를 합쳐 전체 표 요약 $S_{table}$을 완성합니다. 50
    

**주요 성능 지표 비교** 515151515151515151

|**지표**|**Standard RAG**|**LangChain**|**Table Retrieval**|**HD-RAG (Ours)**|
|---|---|---|---|---|
|**Hit@1 (검색 정확도)**|0.0159|0.2390|0.3705|**0.5410**|
|**Exact Match (QA 성능)**|-|-|-|**0.6466**|

- **의미 해석**: 하이브리드 문서에서 단순히 텍스트를 찾는 것보다 표의 구조를 이해하는 것(Table Retrieval)이 중요하며, HD-RAG처럼 계층 구조와 LLM 기반 재검색을 결합했을 때 성능이 폭발적으로 향상됨을 알 수 있습니다. 52
    

### **실험 설계 및 평가**

- **데이터 분할**: DocRAGLib의 4,468개 QA 쌍을 Train(2,990), Dev(502), Test(976)로 나누어 평가했습니다. 53
    
- **비교 모델**: GPT-4o, Qwen2.5, Llama-3.1 등 다양한 크기의 모델을 사용하여 범용성을 확인했습니다. 54
    
- **평가 메트릭**: 올바른 문서를 찾았는지 측정하는 **Hit@K**와 정답과 정확히 일치하는지 보는 **Exact Match(EM)**를 사용했습니다. 55555555
    

---

## 4. 🏁 결론

### **Conclusion**

> "In this paper, we propose the DocRAGLib and HD-RAG framework for the Hybrid Document RAG task in QA. 56DocRAGLib is the first large-scale dataset designed specifically for QA within the Hybrid Document RAG task. 57To address the challenges of DocRAGLib, HD-RAG framework introduces an H-RCL table representation, enhances retrieval with an approach combining ensemble and LLM-based retrieval, and incorporates the RECAP method for complex computational QA tasks. 58Extensive experiments show that HD-RAG outperforms existing baselines, achieving significant improvements in both retrieval accuracy and QA accuracy." 59

[한국어 번역]

본 논문에서는 하이브리드 문서 RAG 기반 QA 작업을 위한 DocRAGLib 데이터셋과 HD-RAG 프레임워크를 제안했습니다. 60DocRAGLib은 하이브리드 문서 RAG 환경의 QA를 위해 특별히 설계된 최초의 대규모 데이터셋입니다. 61DocRAGLib의 도전 과제들을 해결하기 위해 HD-RAG 프레임워크는 H-RCL 표 표현을 도입하고, 앙상블 및 LLM 기반 검색을 결합하여 검색 성능을 강화하며, 복잡한 계산 QA 작업을 위해 RECAP 방식을 통합했습니다. 62광범위한 실험을 통해 HD-RAG가 기존 베이스라인을 능가하며 검색 및 QA 정확도 모두에서 상당한 개선을 달성했음을 확인했습니다. 63

---

### **연구의 의의 및 미래 전망 (전문가 고찰)**

1. 기술적 파급력 및 응용 분야

HD-RAG는 기업용 AI의 '마지막 퍼즐'이라 불리는 정형/비정형 데이터 통합 처리 능력을 한 단계 끌어올렸습니다. 특히 다음과 같은 분야에서 즉각적인 응용이 가능합니다.

- **금융 및 투자 분석**: 수천 페이지의 연례 보고서에서 복잡한 재무제표(계층적 표)와 주석(텍스트)을 결합하여 투자 지표를 도출할 수 있습니다. 64
    
- **법률 및 규제 준수**: 복잡한 별표와 조항이 섞인 법령 문서에서 특정 조건에 따른 법적 해석을 지원할 수 있습니다.
    
- **공공 행정**: 통계청 보고서처럼 방대한 통계 수치와 설명이 결합된 데이터에서 시민의 질문에 정확히 답하는 챗봇 구현이 가능합니다. 65
    

2. 미래 발전 방향 및 한계 극복

현재 HD-RAG는 텍스트와 표라는 두 가지 모달리티에 집중하고 있습니다. 향후에는 차트, 이미지, 다이어그램까지 통합하는 '멀티모달 하이브리드 RAG'로 진화할 것으로 보입니다. 66또한, 현재는 외부 계산기(Calculator)를 별도로 활용하지만, 향후에는 LLM 내부의 추론 엔진 자체가 기호 논리(Symbolic Logic)와 완벽히 결합되어 별도의 외부 호출 없이도 완벽한 수치 연산을 수행하는 방향으로 발전할 것입니다. 67676767

3. 경쟁 기술과의 관계 및 사회적 영향

전통적인 Text-to-SQL 기술이 정형 데이터베이스(DB) 검색에 강점이 있다면, HD-RAG는 '가공되지 않은 원본 문서' 자체를 지식원으로 삼는다는 점에 더 큰 유연성이 있습니다. 68 이는 데이터베이스 구축 비용을 획기적으로 줄여줄 것입니다. 다만, 금융이나 의료처럼 수치 하나가 중요한 분야에서 LLM의 환각(Hallucination)은 여전히 주의해야 할 요소이며, RECAP과 같은 단계적 검증 프레임워크는 이러한 윤리적/사회적 신뢰성 문제를 해결하는 핵심 도구가 될 것입니다. 69

---

## 5. 🏆 최종 요약

하이브리드 문서 RAG를 위한 **HD-RAG**는 복잡한 계층적 표의 구조를 헤더 경로로 보존하는 **H-RCL** 방식과 2단계 정밀 검색 알고리즘을 제안했습니다. 70707070특히 5단계 추론 전략인 **RECAP**과 외부 계산기를 결합하여, 단순 검색을 넘어 복잡한 수치 계산이 포함된 QA에서 기존 모델 대비 40% 이상의 성능 향상을 달성했습니다. 71717171이는 금융, 법률 등 정밀한 데이터 분석이 필요한 산업 분야에 혁신적인 RAG 솔루션을 제시한 것으로 평가됩니다. 72

---

**더 자세한 정보가 필요하신가요?**

- HD-RAG의 **RECAP 프롬프트의 구체적인 예시**를 알고 싶으시면 말씀해 주세요.
    
- **DocRAGLib 데이터셋의 구체적인 통계 수치**에 대해 더 궁금한 점이 있으신가요?