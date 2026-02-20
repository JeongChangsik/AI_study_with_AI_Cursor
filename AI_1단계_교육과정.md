# AI 학습 자료 로드맵 (이론부터 차근차근)

이 문서의 목표는 "강의 운영안"이 아니라,  
**내가 AI를 이해하고 직접 개발할 수 있도록 단계별로 공부하는 학습 자료집**을 만드는 것입니다.

---

## 0) 이 문서 사용 방법

- 각 단계를 순서대로 학습합니다.
- 단계마다 아래 4가지를 남깁니다.
  1. 개념 요약 1~2페이지
  2. 핵심 용어 정리
  3. 참고 자료/책에서 배운 내용 메모
  4. 간단한 코드/실험 기록
- 완벽하게 다 이해한 뒤 넘어가기보다, **기본 이해 -> 적용 -> 복습** 루프로 진행합니다.

---

## 1) 전체 학습 지도

| 단계 | 핵심 질문 | 권장 기간 | 완료 기준 |
|---|---|---:|---|
| 1단계. AI 기초 개념 | AI/ML/DL은 어떻게 다를까? | 1주 | 개념 차이를 설명 가능 |
| 2단계. 수학/통계 기초 | 모델이 왜 이런 식으로 학습될까? | 3주 | 선형대수/확률 기초 설명 가능 |
| 3단계. 머신러닝 이론 | 지도/비지도 학습의 핵심은? | 4주 | 대표 알고리즘 원리 설명 가능 |
| 4단계. 딥러닝 이론 | 신경망은 어떻게 성능을 높일까? | 4주 | MLP/CNN/Transformer 구조 이해 |
| 5단계. 생성형 AI/LLM 기초 | LLM은 왜 강력하고 어디서 실패할까? | 2주 | 토큰/어텐션/파인튜닝 개념 이해 |
| 6단계. 내 AI 개발 시작 | 이론을 내 프로젝트로 연결하려면? | 2주 | 베이스라인 + 개선 계획 작성 |

권장 총 학습 기간: **16주 (주당 8~10시간)**  
빠르게 진행하면 10~12주, 여유 있게 진행하면 20주로 확장 가능합니다.

---

## 2) 단계별 학습 자료

### 1단계. AI 기초 개념

**반드시 이해할 개념**
- 인공지능, 머신러닝, 딥러닝의 관계
- 데이터셋, 라벨, 특성, 모델, 추론
- 학습/검증/테스트 데이터 분리 이유

**추천 자료 (입문)**
- [Elements of AI](https://www.elementsofai.com/)
- [Google Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course)

**추천 도서**
- `핸즈온 머신러닝(3판)` - 실전 연결용
- `AI 2041` - AI 활용 관점 확장용

**자기 점검 질문**
1. "AI vs ML vs DL"을 3문장으로 설명할 수 있는가?
2. 학습 데이터와 테스트 데이터를 나누는 이유를 말할 수 있는가?

---

### 2단계. 수학/통계 기초 (AI 이론의 뼈대)

**반드시 이해할 개념**
- 선형대수: 벡터, 행렬, 선형변환, 내적
- 미분: 기울기, 연쇄법칙(Chain Rule), 경사하강법
- 확률/통계: 확률분포, 기댓값, 분산, 조건부확률, 베이즈 정리

**추천 자료 (무료)**
- [Mathematics for Machine Learning (무료 교재)](https://mml-book.github.io/)
- [Khan Academy - Statistics and Probability](https://www.khanacademy.org/math/statistics-probability)
- [3Blue1Brown - Linear Algebra](https://www.3blue1brown.com/topics/linear-algebra)

**추천 도서**
- `Mathematics for Machine Learning` (Deisenroth et al.)
- `Practical Statistics for Data Scientists` (Bruce et al.)

**자기 점검 질문**
1. 경사하강법이 "손실을 줄이는 방향"으로 가는 이유를 설명할 수 있는가?
2. 분산이 큰 데이터가 모델 학습에 주는 영향을 설명할 수 있는가?

---

### 3단계. 머신러닝 이론

**반드시 이해할 개념**
- 지도학습: 회귀, 분류
- 비지도학습: 군집, 차원축소
- 과적합/과소적합, 편향-분산 트레이드오프
- 모델 평가: Accuracy, Precision, Recall, F1, ROC-AUC

**추천 자료 (무료)**
- [An Introduction to Statistical Learning (ISLR)](https://www.statlearning.com/)
- [scikit-learn User Guide](https://scikit-learn.org/stable/user_guide.html)

**추천 도서**
- `An Introduction to Statistical Learning (2nd Edition)`
- `Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow`

**자기 점검 질문**
1. 정확도(Accuracy)가 높은데도 모델이 쓸모없을 수 있는 이유는?
2. 데이터 누수(Data Leakage)가 왜 치명적인가?

---

### 4단계. 딥러닝 이론

**반드시 이해할 개념**
- 퍼셉트론, 다층신경망(MLP), 활성화함수
- 역전파(Backpropagation)와 최적화(Adam, SGD)
- CNN 기본 구조(합성곱, 풀링)
- Transformer 핵심(Attention, Positional Encoding)

**추천 자료 (무료)**
- [Dive into Deep Learning](https://d2l.ai/)
- [fast.ai Practical Deep Learning](https://course.fast.ai/)
- [CS231n Notes](https://cs231n.github.io/)

**추천 도서**
- `밑바닥부터 시작하는 딥러닝 1, 2`
- `Deep Learning` (Goodfellow, Bengio, Courville)

**자기 점검 질문**
1. 역전파가 필요한 이유를 계산 그래프 관점으로 설명할 수 있는가?
2. CNN과 Transformer가 입력을 다루는 방식이 어떻게 다른가?

---

### 5단계. 생성형 AI/LLM 기초

**반드시 이해할 개념**
- 토크나이저, 임베딩, 다음 토큰 예측
- 사전학습(Pretraining), 미세조정(Fine-tuning), 지시학습(Instruction Tuning)
- RAG(Retrieval-Augmented Generation) 기본 구조
- 환각(Hallucination), 안전성(Safety), 평가의 어려움

**추천 자료 (무료)**
- [Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/chapter1/1)
- [Attention Is All You Need (원 논문)](https://arxiv.org/abs/1706.03762)
- [Lilian Weng - LLM 관련 아티클](https://lilianweng.github.io/)

**추천 도서**
- `Natural Language Processing with Transformers`
- `Generative Deep Learning` (David Foster)

**자기 점검 질문**
1. 파인튜닝과 RAG는 어떤 상황에서 각각 유리한가?
2. LLM의 환각을 줄이기 위한 방법 3가지를 말할 수 있는가?

---

### 6단계. 내 AI 개발 시작 (이론 -> 프로젝트 연결)

**반드시 이해할 개념**
- 문제정의(Task, Input, Output, Metric)
- 베이스라인 모델의 중요성
- 실험 기록(재현성)과 오류 분석(Error Analysis)

**추천 자료 (무료)**
- [Full Stack Deep Learning](https://fullstackdeeplearning.com/)
- [Made With ML](https://madewithml.com/)

**추천 도서**
- `Designing Machine Learning Systems` (Chip Huyen)
- `Machine Learning Engineering` (Andriy Burkov)

**자기 점검 질문**
1. "모델 성능이 올랐다"를 증명하려면 무엇이 필요한가?
2. 다음 실험을 설계할 때 바꿔야 할 변수는 몇 개가 적절한가?

---

## 3) 16주 추천 학습 플랜 (예시)

| 주차 | 학습 주제 | 해야 할 일 |
|---:|---|---|
| 1주 | AI 개념 | AI/ML/DL 구분, 용어 정리 노트 작성 |
| 2~4주 | 수학/통계 | 선형대수 + 확률/통계 핵심 개념 정리 |
| 5~8주 | 머신러닝 | 회귀/분류/평가 지표 + 누수/과적합 이해 |
| 9~12주 | 딥러닝 | MLP/CNN/Transformer 기본 구조 학습 |
| 13~14주 | 생성형 AI | LLM, 토큰화, 파인튜닝/RAG 개념 학습 |
| 15~16주 | 내 프로젝트 | 문제 정의 -> 베이스라인 -> 개선 계획 수립 |

---

## 4) 추천 도서 읽는 순서 (최소 코스 / 확장 코스)

### 최소 코스 (5권)
1. `Mathematics for Machine Learning`
2. `An Introduction to Statistical Learning`
3. `핸즈온 머신러닝(3판)`
4. `밑바닥부터 시작하는 딥러닝 1`
5. `Natural Language Processing with Transformers`

### 확장 코스 (심화)
- `Deep Learning` (Goodfellow et al.)
- `Designing Machine Learning Systems`
- `Machine Learning Engineering`

---

## 5) 자기 점검 템플릿 (시험용이 아닌 학습 점검용)

아래 5문항을 매주 스스로 점검하면 됩니다.

1. 이번 주 핵심 개념 3개를 내 말로 설명할 수 있는가?
2. 새로 배운 수식/알고리즘의 직관을 설명할 수 있는가?
3. 틀리기 쉬운 개념(예: 과적합 vs 데이터 누수)을 구분할 수 있는가?
4. 참고한 책/문서에서 중요한 문장 3개를 기록했는가?
5. 다음 주에 무엇을 복습/보완할지 정했는가?

---

## 6) 바로 시작할 첫 주 학습 가이드

**Day 1**
- AI/ML/DL 관계 정리 (A4 1장)
- 용어 20개 정리 (데이터셋, 라벨, 피처, 모델, 손실 등)

**Day 2**
- 선형대수 입문 영상/교재 학습 (벡터, 행렬, 내적)
- 관련 예제 2개 손으로 계산

**Day 3**
- 확률/통계 핵심(기댓값, 분산, 조건부확률) 정리

**Day 4**
- 머신러닝 문제 유형(분류/회귀/군집) 사례 조사

**Day 5**
- ISLR 또는 핸즈온 머신러닝 1~2장 읽고 요약

**Day 6**
- 간단한 데이터셋을 보고 "어떤 문제인지" 정의해보기

**Day 7**
- 1주 회고: 이해한 것 / 모르는 것 / 다음 주 계획

---

## 7) 마지막 체크리스트

- [ ] AI 기본 용어를 설명할 수 있다.
- [ ] 모델이 학습되는 기본 원리(손실 최소화)를 설명할 수 있다.
- [ ] 대표 지표(Precision/Recall/F1)의 차이를 설명할 수 있다.
- [ ] 딥러닝과 LLM 핵심 개념을 큰 흐름으로 설명할 수 있다.
- [ ] 내 AI 프로젝트의 첫 베이스라인 계획서를 작성했다.

---

이 문서는 앞으로 계속 확장하면서,  
다음 버전에서는 `2단계 딥러닝 심화(수식/아키텍처/논문 읽기 가이드)`를 추가하면 좋습니다.
