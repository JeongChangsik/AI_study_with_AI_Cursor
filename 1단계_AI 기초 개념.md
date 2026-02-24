# 1단계_AI 기초 개념

---

## 개요

1단계의 목적은 AI를 처음 학습할 때 반드시 필요한 개념 뼈대를 세우는 것입니다.  
특히 AI/ML/DL 관계, 문제정의 방법, 데이터 분할 원리를 정확히 이해해야 이후 단계(수학, 머신러닝, 딥러닝)에서 혼란이 줄어듭니다.

---

## 꼭 알아야 할 핵심 설명 (서술형)

AI를 공부할 때 가장 중요한 첫 기준은 "기술 이름"보다 "문제 정의"입니다.  
내가 무엇을 예측/분류/생성하려는지 명확하지 않으면, 모델을 아무리 바꿔도 결과를 평가하기 어렵습니다. 따라서 Task, Input, Output, Metric을 먼저 적는 습관이 필요합니다.

AI, ML, DL의 관계는 포함관계로 이해하면 가장 깔끔합니다. AI가 가장 큰 범주이고, ML은 데이터를 통해 규칙을 학습하는 방식이며, DL은 신경망을 이용하는 ML의 하위 방식입니다. 이 구분이 명확해야 학습 자료를 읽을 때 개념이 섞이지 않습니다.

또한 Train/Validation/Test 분리는 성능을 부풀리지 않기 위한 기본 원칙입니다. 같은 데이터로 학습과 평가를 동시에 하면 성능이 좋아 보이지만, 실제 환경에서는 쉽게 무너집니다. 데이터 누수(Data Leakage)는 이 원칙을 깨는 대표적 문제로, 초기에 반드시 경계해야 합니다.

---

## 핵심 용어

- AI, ML, DL
- Dataset, Feature, Label, Target
- Task, Input, Output, Metric
- Train/Validation/Test
- Generalization, Overfitting, Data Leakage

---

## 추천 자료

- [Elements of AI](https://www.elementsofai.com/)
- [Google Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course)
- 도서: `핸즈온 머신러닝(3판)` 1~2장

---

## 날짜별 학습 기록

### 2026-02-20

**학습 목표**
1. AI, ML, DL의 차이를 3문장으로 설명한다.  
2. 문제정의(Task/Input/Output/Metric)를 작성한다.  
3. 데이터 분할과 데이터 누수 위험을 설명한다.

**핵심 정리**
- AI ⊃ ML ⊃ DL 관계 정리
- 문제정의 4요소 정리
- 지도/비지도/자기지도학습의 차이 정리
- Train/Validation/Test 분리 이유와 누수 사례 이해

**체크리스트**
- [ ] AI/ML/DL 차이를 설명할 수 있다.
- [ ] 내 프로젝트의 문제정의 4요소를 작성했다.
- [ ] 데이터 누수 사례를 1개 이상 말할 수 있다.

---

다음 학습: [2단계_수학과 통계 기초.md](2단계_수학과%20통계%20기초.md)
