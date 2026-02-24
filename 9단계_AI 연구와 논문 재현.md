# 9단계_AI 연구와 논문 재현

---

## 개요

9단계는 "모델을 사용"하는 수준을 넘어,  
**논문을 읽고 재현하고 검증하는 연구형 역량**을 만드는 단계입니다.

핵심은 새로운 아이디어를 무작정 구현하는 것이 아니라,  
재현 가능한 실험 설계와 통계적으로 신뢰할 수 있는 결론을 만드는 것입니다.

---

## 학습 목표

1. 논문 핵심 기여를 구조적으로 요약할 수 있다.  
2. 재현 실험의 변수(데이터/코드/설정/시드)를 통제할 수 있다.  
3. ablation과 비교 실험을 통해 기여도를 분해할 수 있다.  
4. 통계적 신뢰구간을 포함한 결과 해석을 수행할 수 있다.  
5. 재현 패키지(코드/환경/리포트)를 팀 공유 가능한 형태로 구성할 수 있다.

---

## 꼭 알아야 할 핵심 설명 (서술형)

논문 구현은 "코드 복사"가 아니라 "가설 검증"입니다.  
논문에서 주장하는 성능 향상이 어떤 조건에서 성립하는지 확인하려면  
데이터 분할, 전처리, 하이퍼파라미터, 평가 지표를 동일하게 맞추는 통제 실험이 필요합니다.

또한 재현 성공 여부는 단일 점수보다 **변동성**이 중요합니다.  
시드가 바뀌면 성능이 크게 변하는 경우가 많기 때문에, 평균과 신뢰구간을 함께 보고 결론을 내려야 합니다.

좋은 연구 기록은 실패 실험까지 포함합니다.  
왜 실패했는지, 어떤 가정이 틀렸는지 남겨야 다음 반복이 빨라지고 팀 생산성이 올라갑니다.

---

## 세부 이론

### 1) 논문 읽기 프레임

핵심 질문:
1. 문제 정의는 무엇인가?
2. 기존 방법 대비 기여는 무엇인가?
3. 실험 설정은 공정한가?
4. 재현에 필요한 정보가 충분한가?
5. 실제 적용 시 제약은 무엇인가?

### 2) 재현 실험 설계

- 데이터 버전 고정
- 시드 고정(복수 시드 실험 권장)
- 동일 지표/동일 전처리
- baseline과 proposed method 동등 비교

### 3) Ablation Study 설계

모델의 각 구성요소를 하나씩 제거/변경해 기여도를 측정합니다.

예시:
- 정규화 유무
- 데이터 증강 유무
- 특정 모듈 on/off
- 손실 함수 변경

### 4) 하이퍼파라미터 탐색의 공정성

제안 모델만 과도하게 튜닝하면 비교가 왜곡됩니다.  
baseline과 제안 모델 모두 유사한 탐색 예산을 배정해야 공정합니다.

### 5) 통계적 검증

- 평균 점수 + 표준편차
- bootstrap 신뢰구간
- paired 비교(같은 샘플에서 비교)

작은 성능 차이는 우연일 수 있으므로, 유의미성 검토가 필요합니다.

### 6) 벤치마크 해석 주의

- 데이터 누수 위험
- 리더보드 과최적화
- 과도한 사전학습 데이터 활용 여부
- 실제 서비스 분포와 벤치마크 분포 차이

### 7) 재현 패키징

최소 구성:
- requirements.txt / 환경 정보
- 실행 스크립트(run.sh)
- 실험 설정(config)
- 결과 리포트(markdown/json)
- 체크포인트/로그 경로 규칙

### 8) 연구 윤리와 보고 원칙

- 실패 실험 숨기지 않기
- 공정 비교 조건 명시
- 데이터 권리/라이선스 준수
- 결과 과장 표현 지양

---

## 실무에서 자주 틀리는 포인트

1. 논문 설정과 다르게 구현하고 성능만 비교  
2. baseline보다 제안 모델에만 튜닝 예산 집중  
3. 단일 시드 결과를 최종 결론으로 사용  
4. 실패 실험을 기록하지 않아 반복 실수 발생  
5. 재현 코드를 문서 없이 공유해 팀 전파 실패

---

## Python 샘플 코드 (재현 실험 템플릿 + 통계 검증)

ablation 실행 템플릿 예시:

```python
from dataclasses import dataclass
import numpy as np
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import f1_score


@dataclass
class ExpConfig:
    use_scaler: bool
    C: float
    seed: int


def run_once(cfg: ExpConfig) -> float:
    X, y = load_breast_cancer(return_X_y=True)
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, stratify=y, random_state=cfg.seed
    )
    steps = []
    if cfg.use_scaler:
        steps.append(("scaler", StandardScaler()))
    steps.append(("clf", LogisticRegression(max_iter=3000, C=cfg.C, random_state=cfg.seed)))
    model = Pipeline(steps=steps)
    model.fit(X_train, y_train)
    pred = model.predict(X_test)
    return float(f1_score(y_test, pred))


seeds = [11, 22, 33, 44, 55]
base_scores = [run_once(ExpConfig(use_scaler=True, C=1.0, seed=s)) for s in seeds]
abl_scores = [run_once(ExpConfig(use_scaler=False, C=1.0, seed=s)) for s in seeds]

print("baseline_mean_f1:", round(float(np.mean(base_scores)), 4))
print("ablation_mean_f1:", round(float(np.mean(abl_scores)), 4))
print("delta:", round(float(np.mean(base_scores) - np.mean(abl_scores)), 4))
```

paired bootstrap 신뢰구간 예시:

```python
import numpy as np

def paired_bootstrap_ci(a: np.ndarray, b: np.ndarray, n_boot: int = 2000):
    rng = np.random.default_rng(42)
    n = len(a)
    diffs = []
    for _ in range(n_boot):
        idx = rng.integers(0, n, n)
        diffs.append(np.mean(a[idx] - b[idx]))
    lo, hi = np.percentile(diffs, [2.5, 97.5])
    return float(np.mean(diffs)), float(lo), float(hi)

a = np.array(base_scores)
b = np.array(abl_scores)
mean_diff, lo, hi = paired_bootstrap_ci(a, b)
print("paired_diff_mean:", round(mean_diff, 4), "95%CI:", (round(lo, 4), round(hi, 4)))
```

간단 리포트 생성 예시:

```python
from pathlib import Path

report = f"""# Reproduction Report

- baseline_mean_f1: {np.mean(base_scores):.4f}
- ablation_mean_f1: {np.mean(abl_scores):.4f}
- paired_diff_mean: {mean_diff:.4f}
- paired_diff_95ci: [{lo:.4f}, {hi:.4f}]

## Conclusion
Difference is {'significant' if lo > 0 else 'inconclusive'} based on CI.
"""

Path("artifacts").mkdir(exist_ok=True)
Path("artifacts/reproduction_report.md").write_text(report, encoding="utf-8")
print("report saved")
```

---

## 미니 과제

1. 논문 1편을 골라 기여/한계/재현 난점을 1페이지로 요약  
2. baseline/proposed를 동일 튜닝 예산으로 비교  
3. 시드 5개 이상으로 평균+신뢰구간 리포트 작성  
4. ablation 항목 3개 이상 설계하고 기여도 해석

---

## 핵심 용어

- Reproducibility, Replicability, Benchmark
- Ablation, Baseline, Fair Comparison
- Confidence Interval, Bootstrap, Paired Test
- Experiment Registry, Artifact, Report

---

## 추천 자료

- [Papers With Code](https://paperswithcode.com/)
- [ML Reproducibility Checklist](https://www.cs.mcgill.ca/~jpineau/ReproducibilityChecklist.pdf)
- 도서: `The Elements of Statistical Learning`
- 도서: `Deep Learning` (실험 설계/최적화 장)

---

## 이해도 점검 질문

1. 재현(reproducibility)과 복제(replication)의 차이를 설명할 수 있는가?  
2. 공정한 baseline 비교를 위해 통제해야 할 변수는 무엇인가?  
3. 단일 시드 결과를 신뢰하면 위험한 이유는 무엇인가?  
4. ablation에서 기여도를 해석할 때 주의할 점은 무엇인가?  
5. 연구 결과를 팀/조직에서 재사용 가능하게 만들기 위한 최소 산출물은 무엇인가?

---

최상위 허브: [0단계_학습자료.md](0단계_학습자료.md)
