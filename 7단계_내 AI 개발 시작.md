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
5. 데이터 계약(schema/range/null ratio)과 피처 일관성 점검을 설계할 수 있다.  
6. 모델 레지스트리/릴리스 게이트를 운영 기준으로 문서화할 수 있다.  
7. 오프라인-온라인 성능 격차를 측정하고 완화 전략을 제안할 수 있다.

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

### 9) 데이터 계약(Data Contract)과 피처 일관성

배포 후 성능 저하의 상당수는 모델이 아니라 입력 데이터 품질 문제에서 시작됩니다.  
따라서 모델 버전과 함께 데이터 계약을 명시해야 합니다.

필수 계약 항목:
1. 컬럼 존재 여부와 타입
2. 허용 범위(range)
3. 결측률 상한(null ratio threshold)
4. 범주형 값 집합
5. 파생 피처 생성 규칙

훈련 시점과 서빙 시점의 피처 생성 코드가 다르면 training-serving skew가 발생하므로,  
가능하면 동일한 변환 파이프라인을 공유해야 합니다.

### 10) 모델 레지스트리와 버전 전략

모델 파일만 보관하면 운영 추적이 어렵습니다.  
아래 메타데이터를 같이 저장해야 "어떤 모델이 왜 배포됐는지" 설명 가능합니다.

- model_version
- data_version
- code_version(commit hash)
- train config
- 주요 지표 + 신뢰구간
- 승인자/승인시각
- 배포 대상 환경(staging/prod)

즉, 모델 배포는 파일 업로드가 아니라 변경 이력 관리 프로세스입니다.

### 11) SLI/SLO와 Error Budget

운영에서는 성능 수치만이 아니라 서비스 품질 목표가 필요합니다.

- SLI(측정값): p95 latency, 오류율, 정책위반율
- SLO(목표): 예) p95<800ms, 오류율<1%
- Error Budget: 허용 가능한 실패량

Error Budget을 소진하면 신규 릴리스보다 안정화 작업을 우선하는 정책이 필요합니다.

### 12) 오프라인-온라인 갭 관리

오프라인 평가가 좋아도 온라인 KPI가 나쁜 경우가 자주 발생합니다.

주요 원인:
- 입력 분포 변화(data drift)
- 라벨 지연(label delay)
- 사용자 행동 피드백 루프
- 실제 비용 함수와 평가 지표 불일치

대응:
1. shadow/canary로 단계적 검증
2. 온라인 이벤트 로그 기반 재평가
3. 임계값 동적 조정
4. 지표 재정의(업무 KPI 중심)

### 13) 재학습 오케스트레이션

재학습은 정기 배치만으로 충분하지 않습니다.  
이벤트 기반 트리거와 운영 정책을 함께 설계해야 합니다.

트리거 예시:
- PSI > 0.2
- 2주 연속 핵심 KPI 하락
- 신규 라벨 데이터 누적 20% 이상
- 정책 위반률 증가

재학습 파이프라인은 학습 -> 검증 -> 릴리스 게이트 -> 단계 배포까지 자동화되어야 합니다.

### 14) 실험과 A/B 검정의 함정

단순 평균 비교로 A/B 승자를 정하면 오판 가능성이 큽니다.

주의점:
- 실험 기간 부족(계절성 미반영)
- 동시 다중 실험 간 간섭
- 샘플 불균형
- 지표 다중 비교로 인한 유의성 착시

가능하면 신뢰구간/검정력(power)/중지 규칙(stopping rule)을 사전에 정의해야 합니다.

### 15) 운영 문서 체계

실무에서는 코드보다 문서가 사고를 줄입니다.

필수 문서:
- Runbook(장애 대응 절차)
- Release Note(변경 요약/리스크)
- Postmortem(사고 회고)
- KPI 주간 리포트(모델/서비스 통합)

문서화가 잘 된 팀은 모델 교체 속도보다 장애 복구 속도가 빠릅니다.

---

## 실무에서 자주 틀리는 포인트

1. 문제정의 없이 모델 튜닝부터 시작  
2. 베이스라인 없이 복잡 모델부터 적용  
3. 결과는 저장하지만 설정(seed/버전)은 저장하지 않음  
4. 배포 후 성능 모니터링 미구축  
5. 실패 사례 분석 없이 모델만 교체  
6. 데이터 계약 없이 API 스펙 변경  
7. 모델 버전은 있으나 데이터/코드 버전 누락  
8. 오프라인 성능만으로 배포 승인  
9. Error Budget 정책 없이 릴리스 빈도만 증가

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

데이터 계약(schema/range/null ratio) 검증 예시:

```python
import pandas as pd

EXPECTED_SCHEMA = {
    "age": {"dtype": "float", "min": 0, "max": 120, "null_ratio_max": 0.05},
    "usage_time": {"dtype": "float", "min": 0, "max": 1_000_000, "null_ratio_max": 0.1},
    "plan_type": {"dtype": "object", "allowed": {"basic", "pro", "enterprise"}, "null_ratio_max": 0.02},
}

def validate_data_contract(df: pd.DataFrame, schema: dict) -> list[str]:
    errors = []
    for col, rule in schema.items():
        if col not in df.columns:
            errors.append(f"{col}: missing column")
            continue

        null_ratio = df[col].isna().mean()
        if null_ratio > rule.get("null_ratio_max", 1.0):
            errors.append(f"{col}: null_ratio {null_ratio:.3f} > {rule['null_ratio_max']}")

        if rule["dtype"] == "float":
            s = pd.to_numeric(df[col], errors="coerce")
            if s.min(skipna=True) < rule["min"] or s.max(skipna=True) > rule["max"]:
                errors.append(f"{col}: out of range")
        elif rule["dtype"] == "object":
            allowed = rule.get("allowed")
            if allowed is not None:
                invalid = set(df[col].dropna().astype(str)) - set(allowed)
                if invalid:
                    errors.append(f"{col}: invalid categories {invalid}")

    return errors
```

PSI 기반 drift 탐지 예시:

```python
import numpy as np

def psi(expected: np.ndarray, actual: np.ndarray, bins: int = 10) -> float:
    eps = 1e-6
    q = np.linspace(0, 1, bins + 1)
    cut = np.quantile(expected, q)
    cut[0], cut[-1] = -np.inf, np.inf
    e_hist, _ = np.histogram(expected, bins=cut)
    a_hist, _ = np.histogram(actual, bins=cut)
    e_ratio = e_hist / max(e_hist.sum(), 1) + eps
    a_ratio = a_hist / max(a_hist.sum(), 1) + eps
    return float(np.sum((a_ratio - e_ratio) * np.log(a_ratio / e_ratio)))

# 예시
rng = np.random.default_rng(42)
train_feature = rng.normal(0, 1, 5000)
serving_feature = rng.normal(0.4, 1.2, 5000)
psi_value = psi(train_feature, serving_feature)
print("psi:", round(psi_value, 4))
```

릴리스 게이트(품질+안정성+비용) 예시:

```python
def can_promote(metrics: dict) -> bool:
    """
    metrics 예시:
    {
      "f1": 0.91,
      "f1_ci_low": 0.89,
      "policy_violation_rate": 0.002,
      "p95_latency_ms": 640,
      "psi_max": 0.16
    }
    """
    return (
        metrics["f1_ci_low"] >= 0.88
        and metrics["policy_violation_rate"] <= 0.005
        and metrics["p95_latency_ms"] <= 800
        and metrics["psi_max"] <= 0.2
    )

candidate = {
    "f1": 0.91,
    "f1_ci_low": 0.89,
    "policy_violation_rate": 0.003,
    "p95_latency_ms": 700,
    "psi_max": 0.12,
}
print("promote:", can_promote(candidate))
```

모델 레지스트리 메타데이터 기록 예시:

```python
import json
from pathlib import Path
from datetime import datetime

def register_model(registry_path: str, metadata: dict) -> None:
    path = Path(registry_path)
    path.parent.mkdir(parents=True, exist_ok=True)
    row = {
        "registered_at": datetime.utcnow().isoformat(),
        **metadata,
    }
    with open(path, "a", encoding="utf-8") as f:
        f.write(json.dumps(row, ensure_ascii=False) + "\n")

register_model(
    "artifacts/model_registry.jsonl",
    {
        "model_version": "v1.2.0",
        "data_version": "dataset_2026_02",
        "code_version": "commit_hash_example",
        "f1": 0.91,
        "f1_ci_low": 0.89,
        "approved_by": "ml_lead",
        "target_env": "staging",
    },
)
print("model registered")
```

A/B uplift 신뢰구간(bootstrap) 예시:

```python
import numpy as np

def bootstrap_uplift_ci(control: np.ndarray, treatment: np.ndarray, n_boot: int = 1000):
    rng = np.random.default_rng(42)
    uplifts = []
    n_c, n_t = len(control), len(treatment)
    for _ in range(n_boot):
        c = control[rng.integers(0, n_c, n_c)]
        t = treatment[rng.integers(0, n_t, n_t)]
        uplifts.append(t.mean() - c.mean())
    lo, hi = np.percentile(uplifts, [2.5, 97.5])
    return float(np.mean(uplifts)), float(lo), float(hi)

# 예시: 클릭 여부(0/1) 또는 전환율 지표
control = np.array([0, 1, 0, 0, 1, 0, 1, 0, 0, 1])
treatment = np.array([1, 1, 0, 1, 1, 0, 1, 1, 0, 1])
mean_uplift, lo, hi = bootstrap_uplift_ci(control, treatment)
print("uplift_mean:", round(mean_uplift, 4), "95%CI:", (round(lo, 4), round(hi, 4)))
```

---

## 미니 과제

1. 본인 프로젝트 ProblemDefinition을 실제로 작성  
2. 베이스라인 모델 1개 구현 후 metrics.json 저장  
3. 실험 로그 CSV에 3회 이상 실험 결과 누적  
4. 성능 개선 가설 3개와 우선순위 작성  
5. 데이터 계약 문서와 검증 코드 작성  
6. PSI 기반 drift 알람 임계값 정책 정의  
7. 릴리스 게이트 기준표(품질/안전/비용) 작성  
8. 장애 runbook 초안 작성(탐지->완화->복구)

---

## 핵심 용어

- Problem Definition, Baseline, KPI
- Iteration, Ablation, Reproducibility
- Data Drift, Concept Drift, Monitoring
- Model Card, Experiment Log, Rollback
- Data Contract, Training-Serving Skew, Feature Store
- Model Registry, SLI/SLO, Error Budget
- Canary, Shadow, A/B Test, Release Gate
- PSI, Confidence Interval, Runbook

---

## 추천 자료

- [Full Stack Deep Learning](https://fullstackdeeplearning.com/)
- [Made With ML](https://madewithml.com/)
- 도서: `Designing Machine Learning Systems`
- 도서: `Machine Learning Engineering`
- 도서: `Building Machine Learning Powered Applications`

---

## 이해도 점검 질문

1. 문제정의 카드 없이 실험을 시작했을 때 어떤 비용이 발생하는가?  
2. 베이스라인 성능을 기준으로 개선 여부를 어떻게 판정할 것인가?  
3. 실험 우선순위를 정량적으로 정하는 방법을 설명할 수 있는가?  
4. 배포 전략(Canary/A-B/Shadow)의 선택 기준을 설명할 수 있는가?  
5. 데이터 계약이 없는 상태에서 발생할 대표 장애는 무엇인가?  
6. 오프라인 성능과 온라인 KPI가 충돌할 때 어떤 절차로 판단할 것인가?  
7. 릴리스 게이트에 포함해야 할 최소 지표 4가지는 무엇인가?  
8. 롤백 조건을 사전에 정의하지 않으면 어떤 위험이 생기는가?

---

심화 학습: [8단계_멀티모달과 에이전트 시스템.md](8단계_멀티모달과%20에이전트%20시스템.md)

---

최상위 허브: [0단계_학습자료.md](0단계_학습자료.md)
