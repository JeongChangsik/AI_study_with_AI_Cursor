# 7단계_내 AI 개발 시작

---

## 개요

7단계는 이론 학습을 실제 제품/서비스 개발로 연결하는 단계입니다.  
핵심은 "정확한 문제정의 + 재현 가능한 실험 + 운영 가능한 배포"를 한 흐름으로 만드는 것입니다.

---

## 학습 목표

1. 프로젝트 문제정의 문서를 작성할 수 있다.  
2. 베이스라인 모델을 만들고 성능 기준선을 확보할 수 있다.  
3. 실험 기록 체계(파라미터/데이터 버전/결과)를 운영할 수 있다.  
4. 배포 후 모니터링과 재학습 조건을 정의할 수 있다.

---

## 꼭 알아야 할 핵심 설명 (서술형)

AI 프로젝트는 모델링보다 의사결정 시스템에 가깝습니다.  
어떤 문제를 해결하는지, 실패 시 비용이 무엇인지, 어떤 지표를 성공으로 볼지 먼저 정해야 시행착오를 줄일 수 있습니다.

베이스라인은 단순하지만 매우 중요합니다.  
기준선이 없으면 "개선"인지 "우연"인지 판단할 수 없고, 복잡한 모델이 실제로 이득인지도 알 수 없습니다.

실험은 기록이 남아야 자산이 됩니다.  
데이터 버전, 전처리 방식, 모델/파라미터, 시드, 결과 지표를 함께 저장해야 재현성이 확보되고 팀 협업이 쉬워집니다.

배포 이후에는 데이터 분포 변화(Data Drift), 개념 변화(Concept Drift), 오류 유형 변화가 발생합니다.  
따라서 모델 개발의 끝은 배포가 아니라, 모니터링과 개선 루프를 운영하는 것입니다.

---

## 세부 이론

### 1) 문제정의 문서(Problem Definition Card)

필수 항목:
1. 비즈니스 목표
2. 예측 대상/단위
3. 입력 데이터 범위
4. 성공 지표(기술+비즈니스)
5. 실패 허용 범위
6. 윤리/법적 제약

### 2) 베이스라인 전략

- 단순 모델 우선(로지스틱 회귀/의사결정나무)
- 데이터 누수 검증 후 평가
- 최소 기준선(KPI Threshold) 설정

### 3) 실험 설계 원칙

- 한 번에 한 변수만 변경(Ablation)
- 동일 seed로 비교
- 교차검증 또는 고정 validation split
- 결과 표준 양식으로 저장

### 4) 배포와 모니터링

모니터링 항목:
- 입력 분포 변화(피처 통계)
- 출력 분포 변화(예측 확률)
- 지표 저하(정확도/F1/업무 KPI)
- 오류 케이스 누적 패턴

재학습 트리거 예시:
- 2주 연속 KPI 5% 이상 하락
- 핵심 피처 분포 PSI > 0.2
- 신규 데이터 20% 이상 축적

### 5) 문서화 표준

- 실험 로그: 날짜, 데이터버전, 코드버전, 파라미터, 지표
- 모델 카드: 용도, 한계, 금지 사용 시나리오
- 운영 가이드: 장애 대응, 롤백 기준, 점검 주기

### 6) 시스템 아키텍처 관점

실무 프로젝트는 모델 하나로 끝나지 않고, 여러 구성요소가 연결됩니다.

- 데이터 수집/정제 파이프라인
- 학습 파이프라인(피처 생성, 학습, 검증)
- 추론 API(온라인/배치)
- 모니터링/알림 시스템
- 피드백 루프(사용자 신고, 정답 수집, 재학습)

초기에 아키텍처를 단순하게 설계하되, 관측성(로그/메트릭)만큼은 반드시 확보해야 합니다.

### 7) 실험 우선순위 설계

개선 아이디어가 많아도 모두 동시에 시도하면 학습이 느려집니다.  
아래 기준으로 우선순위를 정합니다.

1. 기대 효과(성능/안정성 개선 폭)
2. 구현 난이도
3. 리스크(안전/운영 영향)
4. 검증 용이성(재현 가능성)

RICE(Reach, Impact, Confidence, Effort) 같은 프레임워크로 정량화할 수 있습니다.

### 8) 배포 전략과 롤백

- Canary 배포: 일부 트래픽에 먼저 적용
- A/B 테스트: 기존 모델과 성능 비교
- Shadow 테스트: 사용자 영향 없이 새 모델 검증
- 롤백 조건: KPI 하락, 오류율 상승, 정책 위반 증가

배포 성공 기준과 롤백 기준을 사전에 문서화해야 운영 리스크를 줄일 수 있습니다.

---

## 실무에서 자주 틀리는 포인트

1. 문제정의 없이 모델 튜닝부터 시작  
2. 베이스라인 없이 복잡 모델부터 적용  
3. 결과는 저장하지만 설정(seed/버전)은 저장하지 않음  
4. 배포 후 성능 모니터링 미구축  
5. 실패 사례 분석 없이 모델만 교체

---

## Python 샘플 코드 (프로젝트 베이스라인 템플릿)

```python
from dataclasses import dataclass, asdict
from pathlib import Path
import json
import time

import numpy as np
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import f1_score, roc_auc_score


@dataclass
class ProblemDefinition:
    project_name: str
    task: str
    input_desc: str
    output_desc: str
    primary_metric: str
    secondary_metric: str


def save_json(path: str, data: dict) -> None:
    Path(path).parent.mkdir(parents=True, exist_ok=True)
    with open(path, "w", encoding="utf-8") as f:
        json.dump(data, f, ensure_ascii=False, indent=2)


def run_baseline(random_state: int = 42) -> dict:
    X, y = load_breast_cancer(return_X_y=True)
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, stratify=y, random_state=random_state
    )

    model = Pipeline(
        steps=[
            ("scaler", StandardScaler()),
            ("clf", LogisticRegression(max_iter=3000, random_state=random_state)),
        ]
    )
    model.fit(X_train, y_train)
    pred = model.predict(X_test)
    proba = model.predict_proba(X_test)[:, 1]

    return {
        "f1": float(f1_score(y_test, pred)),
        "roc_auc": float(roc_auc_score(y_test, proba)),
    }


if __name__ == "__main__":
    problem = ProblemDefinition(
        project_name="cancer_baseline",
        task="악성/양성 분류",
        input_desc="검사 수치 30개",
        output_desc="악성 확률 및 클래스",
        primary_metric="f1",
        secondary_metric="roc_auc",
    )

    metrics = run_baseline(random_state=42)
    run_id = f"run_{int(time.time())}"
    artifact_dir = f"artifacts/{run_id}"

    save_json(f"{artifact_dir}/problem_definition.json", asdict(problem))
    save_json(f"{artifact_dir}/metrics.json", metrics)

    print("run_id:", run_id)
    print("metrics:", metrics)
```

실험 비교용 간단 로거:

```python
import csv
from pathlib import Path


def append_experiment_log(path: str, row: dict) -> None:
    Path(path).parent.mkdir(parents=True, exist_ok=True)
    file_exists = Path(path).exists()
    with open(path, "a", encoding="utf-8", newline="") as f:
        writer = csv.DictWriter(f, fieldnames=row.keys())
        if not file_exists:
            writer.writeheader()
        writer.writerow(row)


append_experiment_log(
    "artifacts/experiment_log.csv",
    {
        "date": "2026-02-25",
        "model": "logistic_regression",
        "feature_set": "v1",
        "seed": 42,
        "f1": 0.97,
        "roc_auc": 0.99,
        "note": "baseline",
    },
)
```

---

## 미니 과제

1. 본인 프로젝트 ProblemDefinition을 실제로 작성  
2. 베이스라인 모델 1개 구현 후 metrics.json 저장  
3. 실험 로그 CSV에 3회 이상 실험 결과 누적  
4. 성능 개선 가설 3개와 우선순위 작성

---

## 핵심 용어

- Problem Definition, Baseline, KPI
- Iteration, Ablation, Reproducibility
- Data Drift, Concept Drift, Monitoring
- Model Card, Experiment Log, Rollback

---

## 추천 자료

- [Full Stack Deep Learning](https://fullstackdeeplearning.com/)
- [Made With ML](https://madewithml.com/)
- 도서: `Designing Machine Learning Systems`
- 도서: `Machine Learning Engineering`

---

## 이해도 점검 질문

1. 문제정의 카드 없이 실험을 시작했을 때 어떤 비용이 발생하는가?  
2. 베이스라인 성능을 기준으로 개선 여부를 어떻게 판정할 것인가?  
3. 실험 우선순위를 정량적으로 정하는 방법을 설명할 수 있는가?  
4. 배포 전략(Canary/A-B/Shadow)의 선택 기준을 설명할 수 있는가?  
5. 롤백 조건을 사전에 정의하지 않으면 어떤 위험이 생기는가?

---

최상위 허브: [0단계_학습자료.md](0단계_학습자료.md)
