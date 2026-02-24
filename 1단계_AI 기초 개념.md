# 1단계_AI 기초 개념

---

## 개요

1단계는 "AI를 제대로 시작하기 위한 기초 체력"을 만드는 단계입니다.  
이 단계에서 흔히 발생하는 실수는 모델/라이브러리 이름만 빠르게 익히고, 문제정의와 평가 기준을 생략하는 것입니다.  
이 문서는 그 실수를 막기 위해, 반드시 필요한 핵심 개념을 빠짐없이 정리합니다.

---

## 학습 목표

1. AI/ML/DL 관계를 사례와 함께 설명할 수 있다.  
2. 문제정의 4요소(Task/Input/Output/Metric)를 직접 작성할 수 있다.  
3. 지도/비지도/자기지도학습의 차이를 이해하고 예시를 들 수 있다.  
4. Train/Validation/Test 분할과 데이터 누수 위험을 설명할 수 있다.  
5. 분류/회귀 문제에서 기본 지표를 올바르게 고를 수 있다.  
6. 지능형 에이전트 관점(PEAS)을 이용해 문제를 구조화할 수 있다.  
7. 혼동행렬 기반으로 오류를 해석하고 임계값 조정 방향을 제안할 수 있다.

---

## 꼭 알아야 할 핵심 설명 (서술형)

AI 학습의 첫 단추는 "어떤 모델을 쓸까?"가 아니라 "무슨 문제를 풀까?"입니다.  
문제를 정확히 정의하지 않으면, 성능이 좋아 보여도 실제로는 쓸 수 없는 모델이 나올 수 있습니다.

AI는 가장 큰 범주이고, ML은 데이터에서 규칙을 학습하는 AI 하위 분야이며, DL은 다층 신경망을 사용하는 ML의 하위 분야입니다.  
즉 `AI ⊃ ML ⊃ DL` 구조를 이해해야 학습 범위가 정리됩니다.

또한 학습 데이터와 평가 데이터는 반드시 분리해야 합니다.  
같은 데이터로 학습과 평가를 하면 점수는 높지만 일반화 성능은 낮아질 수 있습니다.  
데이터 누수(Data Leakage)는 그중 가장 위험한 문제로, 실무 실패의 대표 원인입니다.

---

## 세부 이론

### 1) AI 패러다임 흐름

- **규칙 기반 AI(Symbolic AI)**: 사람이 규칙을 직접 작성
- **통계적 ML**: 데이터 기반으로 규칙을 학습
- **딥러닝/파운데이션 모델**: 대규모 데이터/모델로 표현 학습

핵심은 "규칙 작성의 주체가 사람에서 데이터로 이동"했다는 점입니다.

### 2) 문제 유형 분류

- **분류(Classification)**: 범주 예측 (예: 스팸/정상)
- **회귀(Regression)**: 연속값 예측 (예: 매출, 온도)
- **군집(Clustering)**: 유사 그룹 탐색 (예: 고객 세분화)
- **추천/랭킹**: 상대적 선호 예측 (예: 상품 추천)

### 3) 문제정의 4요소 (Task/Input/Output/Metric)

- `Task`: 해결할 문제
- `Input`: 모델 입력 데이터
- `Output`: 모델 출력 형식
- `Metric`: 성공 판단 지표

예시(이탈 예측):
- Task: 30일 내 이탈 여부 예측
- Input: 최근 접속일, 결제이력, 사용시간
- Output: 이탈 확률(0~1)
- Metric: Recall, ROC-AUC

### 4) 데이터 분할과 누수

기본 원칙:
- Train: 학습
- Validation: 모델/하이퍼파라미터 선택
- Test: 최종 평가

누수 유형:
1. **Target Leakage**: 정답과 직접 연관된 열이 입력에 포함  
2. **Time Leakage**: 미래 정보를 과거 예측에 사용  
3. **Preprocessing Leakage**: 전체 데이터 통계로 전처리 후 분할

### 5) 기본 지표 선택 기준

- 클래스 균형 + 비용이 비슷: Accuracy
- 양성 놓치면 치명적(의료/이탈 방지): Recall
- 오탐 줄이는 것이 중요(스팸 필터): Precision
- 균형 잡힌 종합 판단: F1
- 임계값 독립 비교: ROC-AUC

### 6) 임계값(Threshold)과 의사결정

분류 모델은 보통 확률을 출력하고, 임계값을 기준으로 클래스가 정해집니다.  
임계값을 0.5로 고정하는 것은 관례일 뿐 정답이 아닙니다.  
예를 들어, 사기 탐지처럼 놓치면 손해가 큰 문제는 임계값을 낮춰 Recall을 높이고,  
오탐 비용이 큰 문제는 임계값을 높여 Precision을 높일 수 있습니다.

### 7) 베이스라인 설계 원칙

좋은 베이스라인은 복잡하지 않지만 비교 가능한 기준을 제공합니다.

필수 조건:
1. 간단한 모델(로지스틱 회귀 등)
2. 재현 가능한 분할(seed 고정)
3. 최소 2개 이상 지표 기록
4. 누수 점검 체크리스트 포함

### 8) 지능형 에이전트 관점(PEAS)

AI를 단순 예측기로만 보면 문제의 실제 맥락을 놓치기 쉽습니다.  
AIMA(Artificial Intelligence: A Modern Approach)에서 강조하는 에이전트 관점은 문제를 다음처럼 구조화합니다.

- **P (Performance Measure)**: 성공 기준
- **E (Environment)**: 시스템이 동작하는 환경
- **A (Actuators)**: 에이전트가 취할 행동/출력
- **S (Sensors)**: 에이전트가 관측하는 입력

이 틀을 사용하면 "모델 정확도"뿐 아니라 운영 조건, 의사결정 방식, 실패 비용까지 함께 설계할 수 있습니다.

### 9) 데이터 중심 AI(Data-centric AI) 기초

초급 단계에서 자주 간과되지만, 모델보다 데이터가 성능을 더 크게 좌우하는 경우가 많습니다.

핵심 포인트:
1. 라벨 품질: 라벨 오류/불일치 점검
2. 대표성: 실제 운영 분포를 반영하는 샘플 구성
3. 누락 특성: 중요한 변수 미수집 여부
4. 데이터 문서화: 수집 방법/시점/제약 조건 기록

좋은 데이터셋은 "크기"보다 "정확성/일관성/대표성"이 중요합니다.

### 10) 학습 패러다임 4가지 구분

- **지도학습**: 라벨이 있는 데이터로 학습
- **비지도학습**: 라벨 없이 구조 탐색
- **자기지도학습**: 데이터 자체로 학습 신호 생성
- **강화학습**: 보상 신호를 최대화하는 정책 학습

1단계에서는 최소한 "어떤 문제에 어떤 패러다임이 맞는지"를 구분할 수 있어야 합니다.

### 11) 혼동행렬(Confusion Matrix)과 오류 비용

모델이 어디서 틀리는지를 보려면 혼동행렬이 필요합니다.

- TP: 양성을 양성으로 예측
- TN: 음성을 음성으로 예측
- FP: 음성을 양성으로 잘못 예측(오탐)
- FN: 양성을 음성으로 놓침(미탐)

실무에서는 FP와 FN의 비용이 다릅니다.  
예를 들어 의료 진단에서는 FN 비용이 매우 커서 Recall을 우선하는 경우가 많습니다.

---

## 실무에서 자주 틀리는 포인트

1. 정확도만 보고 모델 선택  
2. Validation 없이 Test를 반복 조회  
3. 문제정의 없이 모델부터 구현  
4. 시간 순서가 있는 데이터를 랜덤 분할  
5. 전처리를 분할 전에 전체 데이터에 적용  
6. FP/FN 비용 차이를 고려하지 않고 임계값을 고정  
7. 데이터 품질 점검 없이 알고리즘만 교체

---

## Python 샘플 코드 (기초 베이스라인)

아래 코드는 분류 문제에서 안전한 분할과 기본 지표 확인 흐름을 보여줍니다.

```python
from dataclasses import dataclass
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score


@dataclass
class ProblemCard:
    task: str
    input_desc: str
    output_desc: str
    metric: str


card = ProblemCard(
    task="유방암 악성/양성 분류",
    input_desc="의학적 측정 특성값 30개",
    output_desc="악성 확률 및 클래스",
    metric="F1, ROC-AUC",
)
print(card)

# 데이터 로드
X, y = load_breast_cancer(return_X_y=True)

# 분할: 먼저 분할하고, 전처리는 Pipeline 내부에서 학습
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

model = Pipeline(
    steps=[
        ("scaler", StandardScaler()),
        ("clf", LogisticRegression(max_iter=2000, random_state=42)),
    ]
)

model.fit(X_train, y_train)
pred = model.predict(X_test)
proba = model.predict_proba(X_test)[:, 1]

metrics = {
    "accuracy": accuracy_score(y_test, pred),
    "precision": precision_score(y_test, pred),
    "recall": recall_score(y_test, pred),
    "f1": f1_score(y_test, pred),
    "roc_auc": roc_auc_score(y_test, proba),
}

for k, v in metrics.items():
    print(f"{k}: {v:.4f}")
```

혼동행렬과 임계값 변화 분석 예시:

```python
import numpy as np
from sklearn.metrics import confusion_matrix, precision_score, recall_score

thresholds = np.linspace(0.1, 0.9, 9)
print("thr | precision | recall | tn fp fn tp")
for thr in thresholds:
    pred_thr = (proba >= thr).astype(int)
    tn, fp, fn, tp = confusion_matrix(y_test, pred_thr).ravel()
    p = precision_score(y_test, pred_thr, zero_division=0)
    r = recall_score(y_test, pred_thr, zero_division=0)
    print(f"{thr:.1f} | {p:.4f}    | {r:.4f} | {tn:2d} {fp:2d} {fn:2d} {tp:2d}")
```

---

## 미니 과제

1. 위 코드의 `ProblemCard`를 본인 아이디어로 바꿔 작성하기  
2. 지표 우선순위를 "정확도 중심"과 "재현율 중심"으로 각각 비교 이유 적기  
3. 데이터 누수 사례 2개를 실제 서비스 맥락으로 작성하기  
4. 임계값 0.3/0.5/0.7에서 FP/FN 변화 표를 작성하기  
5. 본인 프로젝트를 PEAS로 1페이지 정리하기

---

## 핵심 용어

- AI, ML, DL
- Dataset, Feature, Label, Target
- Task, Input, Output, Metric
- Train/Validation/Test
- Generalization, Overfitting, Data Leakage
- Precision, Recall, F1, ROC-AUC
- Confusion Matrix, Threshold, Class Imbalance
- PEAS, Data-centric AI, Label Quality

---

## 추천 자료

- [Elements of AI](https://www.elementsofai.com/)
- [Google Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course)
- 도서: `핸즈온 머신러닝(3판)` 1~2장
- 도서: `Artificial Intelligence: A Modern Approach` (에이전트/문제정의 관점)
- 도서: `An Introduction to Statistical Learning` (평가와 일반화 기초)

---

## 이해도 점검 질문

1. AI/ML/DL의 포함관계를 실제 서비스 예시로 설명할 수 있는가?  
2. 문제정의 4요소(Task/Input/Output/Metric)가 빠진 상태에서 발생할 실패 사례는 무엇인가?  
3. 데이터 누수 3가지 유형(Target/Time/Preprocessing)을 각각 구분할 수 있는가?  
4. 임계값을 조정하면 Precision/Recall이 어떻게 바뀌는지 설명할 수 있는가?  
5. 혼동행렬에서 FP/FN의 비즈니스 비용 차이를 설명할 수 있는가?  
6. 내 프로젝트를 PEAS 틀로 구조화할 수 있는가?  
7. 데이터 중심 AI 관점에서 현재 데이터셋의 취약점을 3가지 이상 찾을 수 있는가?

---

다음 학습: [2단계_수학과 통계 기초.md](2단계_수학과%20통계%20기초.md)
