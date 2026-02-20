# AI 분야별 1단계 교육 과정

## 📚 1단계: 기초 단계 (Foundation Level)

### 🎯 학습 목표
- AI의 기본 개념과 원리 이해
- 머신러닝의 기초 지식 습득
- 데이터 처리의 기본 원리 파악
- 시각적 학습을 통한 직관적 이해

---

## 📊 주요 학습 영역

### 1. AI 기초 개념

**핵심 내용:**
- 인공지능의 정의와 역사
- AI vs 머신러닝 vs 딥러닝의 차이점
- AI의 현재와 미래

**👨‍💻 작성자 참고 자료:**
- [네이버 AI 스쿨](https://ai.naver.com/) - AI 기초 개념 강의
    - https://bizschool.naver.com/online/course/65144/lecture/1461729?currentTab=curriculum


### 2. 머신러닝 기초

**학습 요소:**
- 지도학습 vs 비지도학습
- 분류와 회귀 문제
- 모델 평가 방법

**👨‍💻 작성자 참고 자료:**


### 3. 데이터 처리 기초

**중요 개념:**
- 데이터 전처리
- 특성 엔지니어링
- 데이터 시각화

---

## 🎨 시각적 학습 자료

### 학습 플로우 차트
```
입력 데이터 → 전처리 → 모델 학습 → 평가 → 결과
    ↓           ↓         ↓        ↓      ↓
   이미지     정규화    알고리즘   정확도   예측
```

### AI 분야별 로드맵
```
┌─────────────────┐
│   AI 1단계      │
├─────────────────┤
│ • 기초 개념     │
│ • 머신러닝      │
│ • 데이터 처리    │
│ • 시각화        │
└─────────────────┘
         ↓
┌─────────────────┐
│   AI 2단계      │
├─────────────────┤
│ • 딥러닝        │
│ • 신경망        │
│ • 고급 알고리즘  │
└─────────────────┘
         ↓
┌─────────────────┐
│   AI 3단계      │
├─────────────────┤
│ • 특화 분야     │
│ • 실무 적용     │
│ • 프로젝트      │
└─────────────────┘
```

---

## 📋 실습 프로젝트

### 1. 이미지 분류 프로젝트

**목표:** 간단한 이미지 분류 모델 만들기
- MNIST 데이터셋 활용
- 기본 분류 알고리즘 적용
- 결과 시각화

### 2. 데이터 시각화 프로젝트

**목표:** 다양한 차트와 그래프 만들기
- matplotlib, seaborn 활용
- 인사이트 도출
- 스토리텔링

---

## 🛠️ 사용 도구 및 기술

### 프로그래밍 언어
- **Python** (주요 언어)
- **R** (통계 분석)

### 라이브러리
```python
# 데이터 처리
import pandas as pd
import numpy as np

# 시각화
import matplotlib.pyplot as plt
import seaborn as sns

# 머신러닝
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
```

### 개발 환경
- **Jupyter Notebook** (대화형 개발)
- **Google Colab** (클라우드 환경)
- **VS Code** (코드 편집)

---

## 📈 평가 기준

### 이론 평가 (40%)
- AI 기본 개념 이해도
- 머신러닝 원리 파악
- 용어 및 정의 숙지

### 실습 평가 (60%)
- 코드 작성 능력
- 데이터 처리 능력
- 결과 시각화 능력
- 문제 해결 능력

---

## 🎯 학습 성과 지표

### 완료 시 달성 목표
- ✅ AI 기본 개념 완전 이해
- ✅ 머신러닝 알고리즘 3개 이상 구현
- ✅ 데이터 시각화 차트 5종류 이상 제작
- ✅ 간단한 예측 모델 구축
- ✅ 프로젝트 2개 이상 완성

---

## 📚 추천 학습 자료

### 온라인 강의
1. **Coursera** - Machine Learning by Andrew Ng
2. **edX** - Introduction to Artificial Intelligence
3. **Udacity** - Intro to Machine Learning

### 도서
1. **"Hands-On Machine Learning"** - Aurélien Géron
2. **"Python for Data Analysis"** - Wes McKinney
3. **"Data Science from Scratch"** - Joel Grus

### 실습 플랫폼
- **Kaggle** - 데이터 사이언스 커뮤니티
- **GitHub** - 코드 공유 및 협업
- **Google Colab** - 무료 GPU 환경

---

## 🚀 다음 단계 준비

1단계 완료 후 2단계로 진행할 준비사항:
- 딥러닝 기초 개념 학습
- 신경망 구조 이해
- 고급 머신러닝 알고리즘 탐구
- 실무 프로젝트 참여

---

*이 문서는 AI 교육의 1단계 과정을 시각적 자료 중심으로 정리한 것입니다.*

---

## 🧑‍🏫 1단계 이론 수업형 확장 커리큘럼 (8주)

아래는 "개념 이해 → 수식 감각 → 코드 적용" 순서로 학습하도록 설계한 1단계 이론 수업안입니다.

### 1주차. AI 문제 정의와 학습 목표 설정

**학습 목표**
- AI 프로젝트에서 "문제 정의"가 왜 성능보다 먼저인지 이해한다.
- 분류/회귀/군집/추천 문제를 구분한다.

**핵심 이론**
- 문제 정의 4요소: `Task`, `Input`, `Output`, `Metric`
- 좋은 목표의 조건: 측정 가능성, 데이터 수집 가능성, 비즈니스 연계성

**필수 용어**
- Task, Label, Feature, Target, Baseline

**확인 문제**
1. "고객 이탈 예측"은 분류인가 회귀인가?
2. Metric이 없는 AI 프로젝트는 왜 실패 확률이 높은가?

**수업 과제**
- 관심 도메인 1개를 골라 `문제정의 카드(1페이지)` 작성

---

### 2주차. 데이터 이해와 전처리 기초

**학습 목표**
- 데이터 품질이 모델 성능에 미치는 영향을 설명한다.
- 결측치/이상치/스케일 문제를 처리할 수 있다.

**핵심 이론**
- 데이터 품질 체크: 결측, 중복, 타입 오류, 클래스 불균형
- 전처리 기본 흐름: `수집 → 정제 → 변환 → 분할(train/valid/test)`

**필수 용어**
- Missing Value, Outlier, Imbalance, Leakage

**확인 문제**
1. 데이터 누수(Data Leakage)는 어떻게 발생하는가?
2. 표준화(Standardization)와 정규화(Normalization)의 차이는?

**수업 과제**
- 샘플 데이터셋 1개를 선택해 EDA 리포트 작성

---

### 3주차. 머신러닝을 위한 통계/확률 핵심

**학습 목표**
- 평균, 분산, 상관관계, 조건부확률을 ML 관점으로 이해한다.
- 손실함수 최소화의 개념을 직관적으로 설명할 수 있다.

**핵심 이론**
- 평균/분산: 데이터 분포 파악의 기본
- 베이즈 정리 기초: 사전확률과 사후확률
- 손실함수 예시: MSE(회귀), Cross-Entropy(분류)

**필수 용어**
- Distribution, Variance, Bias, Likelihood, Loss

**확인 문제**
1. 분산이 큰 데이터는 학습에 어떤 영향을 주는가?
2. 왜 학습은 결국 "손실 최소화" 문제로 귀결되는가?

**수업 과제**
- 동일 데이터에 MSE와 MAE를 각각 계산하고 해석 비교

---

### 4주차. 지도학습 알고리즘 입문

**학습 목표**
- 회귀/분류 대표 알고리즘의 특성을 비교한다.
- 단순 모델부터 시작해야 하는 이유를 이해한다.

**핵심 이론**
- 회귀: Linear Regression
- 분류: Logistic Regression, Decision Tree, Random Forest
- 베이스라인 모델의 필요성: 복잡한 모델 전에 기준선 확보

**필수 용어**
- Underfitting, Overfitting, Linear/Non-linear Boundary

**확인 문제**
1. 선형회귀를 분류에 바로 쓰기 어려운 이유는?
2. 트리 기반 모델이 표형 데이터에서 강한 이유는?

**수업 과제**
- 분류 데이터셋으로 `Logistic Regression vs Random Forest` 성능 비교

---

### 5주차. 모델 평가와 실험 설계

**학습 목표**
- 데이터 분할과 검증 전략을 올바르게 선택한다.
- 평가 지표를 문제 특성에 맞게 선택할 수 있다.

**핵심 이론**
- Train/Validation/Test의 역할 분리
- 교차검증(Cross Validation) 개념
- 주요 지표: Accuracy, Precision, Recall, F1, ROC-AUC

**필수 용어**
- Confusion Matrix, Threshold, Generalization

**확인 문제**
1. 불균형 데이터에서 Accuracy만 보면 위험한 이유는?
2. Recall이 중요한 산업 도메인 예시는?

**수업 과제**
- 임계값(Threshold)을 바꿔 Precision/Recall trade-off 분석

---

### 6주차. 비지도학습과 표현 학습 기초

**학습 목표**
- 라벨 없는 데이터에서 패턴을 찾는 방법을 이해한다.
- 차원축소의 목적과 활용 사례를 설명할 수 있다.

**핵심 이론**
- 군집화: K-Means, Hierarchical Clustering
- 차원축소: PCA 기초
- 활용 사례: 고객 세분화, 이상탐지, 탐색적 분석

**필수 용어**
- Cluster, Centroid, Distance Metric, Explained Variance

**확인 문제**
1. K를 잘못 선택하면 어떤 문제가 생기는가?
2. PCA가 시각화에 자주 사용되는 이유는?

**수업 과제**
- 2차원 PCA 시각화 후 군집 구조 해석

---

### 7주차. 일반화 성능과 모델 개선 전략

**학습 목표**
- 과적합 원인을 설명하고 해결 전략을 선택한다.
- 하이퍼파라미터 튜닝의 기본 절차를 익힌다.

**핵심 이론**
- 과적합 완화: 정규화(L1/L2), 데이터 증강, 모델 단순화
- 튜닝 전략: Grid Search, Random Search
- 실험 기록의 중요성: 동일 조건 재현 가능성 확보

**필수 용어**
- Regularization, Hyperparameter, Reproducibility

**확인 문제**
1. 학습 성능은 높고 검증 성능은 낮다면 어떤 상태인가?
2. Random Search가 실무에서 자주 쓰이는 이유는?

**수업 과제**
- 2개 이상 하이퍼파라미터를 조정해 성능 변화 로그 작성

---

### 8주차. 미니 캡스톤: 내 AI 베이스라인 만들기

**학습 목표**
- 문제정의부터 평가까지 하나의 사이클을 완성한다.
- 결과를 문서화하고 개선 방향을 제안할 수 있다.

**핵심 이론**
- End-to-End 파이프라인 구성
- 실패 분석(Error Analysis) 중심 개선
- 모델 카드(Model Card) 작성 기초

**필수 용어**
- Pipeline, Baseline Report, Error Analysis

**확인 문제**
1. 성능 수치 외에 반드시 보고해야 할 항목은?
2. "좋은 실험 기록"의 조건은 무엇인가?

**수업 과제**
- 최종 보고서 3페이지 작성
  - 문제 정의
  - 데이터/모델/평가
  - 실패 사례와 개선 계획

---

## 📝 이론 수업 운영 템플릿 (차시별 공통)

각 차시는 아래 템플릿으로 운영하면 학습 효율이 높습니다.

1. **도입 (10분)**: 지난주 핵심 복습 + 오늘 학습 목표 확인  
2. **핵심 이론 (25분)**: 개념/수식/그림 중심 설명  
3. **개념 점검 (10분)**: OX 또는 단답형 퀴즈 5문항  
4. **미니 실습 (20분)**: 노트북에서 코드 1~2개 실행  
5. **정리 (5분)**: 용어 카드 정리 + 다음 주 예습 키워드

---

## 🧭 내 AI 개발을 위한 단계별 학습 루프

아래 루프를 반복하면 "공부"와 "개발"이 분리되지 않고 함께 성장합니다.

### STEP 1. 문제 정의
- 내가 만들 AI의 사용자, 입력 데이터, 출력 형태를 한 문단으로 정리

### STEP 2. 데이터 확보
- 최소 동작 가능한 데이터셋(Minimum Dataset)부터 시작
- 데이터 수집 경로와 저작권/개인정보 이슈 확인

### STEP 3. 베이스라인 구축
- 가장 단순한 모델부터 구현하여 기준 성능 확보

### STEP 4. 평가와 실패 분석
- 지표 1개만 보지 말고 오분류 사례를 직접 확인

### STEP 5. 개선 실험
- 한 번에 한 요소만 변경(모델, 전처리, 파라미터 중 1개)
- 실험 결과를 표 형태로 기록

### STEP 6. 문서화와 회고
- "무엇을 시도했고, 왜 좋아졌거나 나빠졌는지"를 주간 회고로 저장

---

## 📚 주제별 추가 학습 자료 (이론 중심)

### AI/ML 기초
- [Machine Learning Crash Course (Google)](https://developers.google.com/machine-learning/crash-course)
- [Elements of AI](https://www.elementsofai.com/)
- [Kaggle Learn - Intro to Machine Learning](https://www.kaggle.com/learn/intro-to-machine-learning)

### 수학/통계 기초
- [Khan Academy - Statistics and Probability](https://www.khanacademy.org/math/statistics-probability)
- [3Blue1Brown - Essence of Linear Algebra](https://www.3blue1brown.com/topics/linear-algebra)

### 딥러닝 사전 준비
- [DeepLearning.AI - Deep Learning Specialization](https://www.coursera.org/specializations/deep-learning)
- [fast.ai Practical Deep Learning](https://course.fast.ai/)

### 실습/문서화
- [scikit-learn User Guide](https://scikit-learn.org/stable/user_guide.html)
- [Pandas User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
- [Weights & Biases Reports](https://wandb.ai/site)

---

## ✅ 1단계 완료 체크리스트 (이론 수업 기준)

- [ ] AI 문제를 분류/회귀/군집 중 하나로 명확히 정의할 수 있다.
- [ ] 데이터 누수와 과적합의 차이를 설명할 수 있다.
- [ ] 기본 지표(Accuracy, Precision, Recall, F1)를 상황에 맞게 선택할 수 있다.
- [ ] 베이스라인 모델 1개 이상을 구축하고 결과를 보고서로 작성했다.
- [ ] 실패 사례를 분석하고 다음 실험 계획을 제시할 수 있다.

---

### 다음 문서 확장 제안

이 문서 다음 버전에서 아래를 추가하면 2단계(딥러닝)로 자연스럽게 넘어갈 수 있습니다.
- 퍼셉트론과 다층신경망(MLP) 이론
- 역전파(Backpropagation) 직관 설명
- CNN/RNN/Transformer 입문 비교표
- 실습형 과제(이미지/텍스트) 1개씩
