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

---

## 실무에서 자주 틀리는 포인트

1. 정확도만 보고 모델 선택  
2. Validation 없이 Test를 반복 조회  
3. 문제정의 없이 모델부터 구현  
4. 시간 순서가 있는 데이터를 랜덤 분할  
5. 전처리를 분할 전에 전체 데이터에 적용

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

---

## 미니 과제

1. 위 코드의 `ProblemCard`를 본인 아이디어로 바꿔 작성하기  
2. 지표 우선순위를 "정확도 중심"과 "재현율 중심"으로 각각 비교 이유 적기  
3. 데이터 누수 사례 2개를 실제 서비스 맥락으로 작성하기

---

## 핵심 용어

- AI, ML, DL
- Dataset, Feature, Label, Target
- Task, Input, Output, Metric
- Train/Validation/Test
- Generalization, Overfitting, Data Leakage
- Precision, Recall, F1, ROC-AUC

---

## 추천 자료

- [Elements of AI](https://www.elementsofai.com/)
- [Google Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course)
- 도서: `핸즈온 머신러닝(3판)` 1~2장

---

## 날짜별 학습 기록

### 2026-02-20

**학습 내용**
- AI/ML/DL 포함관계 정리
- 문제정의 4요소 문서화
- Train/Validation/Test 분할 원칙
- 데이터 누수 유형 정리

**체크리스트**
- [ ] AI/ML/DL을 사례로 설명 가능
- [ ] 내 문제정의 4요소를 작성 완료
- [ ] 누수 유형 3가지를 구분 가능

---

다음 학습: [2단계_수학과 통계 기초.md](2단계_수학과%20통계%20기초.md)
