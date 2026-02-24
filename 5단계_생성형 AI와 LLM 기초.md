# 5단계_생성형 AI와 LLM 기초

---

## 개요

5단계는 생성형 AI/LLM을 "신기한 도구"가 아니라 "구조를 이해하고 통제 가능한 시스템"으로 배우는 단계입니다.  
토큰화, 임베딩, 사전학습, RAG, 파인튜닝의 역할을 분리해서 이해하는 것이 핵심입니다.

---

## 학습 목표

1. LLM의 다음 토큰 예측 원리를 설명할 수 있다.  
2. 토크나이저/임베딩/컨텍스트 윈도우 관계를 설명할 수 있다.  
3. 파인튜닝과 RAG의 차이와 선택 기준을 설명할 수 있다.  
4. 환각/프롬프트 인젝션 등 리스크를 기술적으로 설명할 수 있다.  
5. RAG 파이프라인(청킹/검색/재랭킹/컨텍스트 구성)을 설계할 수 있다.  
6. 생성 품질/안전성/비용을 함께 고려한 평가 체계를 설계할 수 있다.  
7. 추론 최적화(캐시/양자화/배치) 전략의 목적과 트레이드오프를 설명할 수 있다.

---

## 꼭 알아야 할 핵심 설명 (서술형)

LLM은 입력 문장을 토큰 단위로 쪼개고, 각 토큰을 벡터(임베딩)로 바꾼 뒤, 문맥을 이용해 다음 토큰 확률을 예측합니다.  
이 단순한 학습 목표가 대규모 데이터와 모델 크기를 만나면, 요약/번역/질의응답/코드 생성 같은 범용 능력으로 확장됩니다.

실무에서는 "지식을 어디에 둘지"가 매우 중요합니다.  
모델 내부 파라미터에 지식을 녹이는 방식이 파인튜닝이고, 외부 문서를 검색해 컨텍스트로 넣는 방식이 RAG입니다.  
최신성/출처/갱신 비용을 고려하면, 많은 업무에서 RAG가 먼저 선택됩니다.

또한 LLM은 사실처럼 보이는 틀린 답(환각)을 만들 수 있습니다.  
따라서 정답률만 보는 것이 아니라 근거 제시, 출처 추적, 안전 정책 준수 여부를 함께 평가해야 합니다.

---

## 세부 이론

### 1) 토큰화와 임베딩

- Tokenizer: 문자열 -> 토큰 ID
- Embedding: 토큰 ID -> 밀집 벡터
- Context Window: 한 번에 참조 가능한 토큰 길이

컨텍스트가 길수록 메모리/비용이 증가하므로, 문서 압축/검색 전략이 중요합니다.

### 2) 학습 단계

- **Pretraining**: 대규모 텍스트로 일반 언어능력 학습
- **SFT(Instruction Tuning)**: 지시 따르기 능력 강화
- **RLHF/RLAIF**: 인간 선호를 반영해 응답 품질 보정

### 3) RAG와 파인튜닝 비교

- 파인튜닝 장점: 스타일/도메인 행동 일관화
- 파인튜닝 한계: 비용, 재학습 필요, 최신 지식 반영 느림
- RAG 장점: 최신 지식 반영, 출처 연결 용이
- RAG 한계: 검색 실패 시 답변 품질 저하

### 4) 생성형 AI 평가 관점

- 사실성(Factuality)
- 근거성(Groundedness)
- 유해성/안전성(Safety)
- 지연시간/비용(Latency/Cost)

### 5) 디코딩 전략

모델 출력은 디코딩 방식에 크게 영향을 받습니다.

- Greedy: 가장 높은 확률 토큰 선택(안정적, 반복 위험)
- Beam Search: 여러 후보를 유지(품질 향상 가능, 다양성 저하)
- Top-k Sampling: 상위 k개에서 확률 샘플링(다양성 증가)
- Top-p(Nucleus) Sampling: 누적확률 p 구간에서 샘플링
- Temperature: 확률 분포의 날카로움 조절

생성형 서비스에서는 품질/다양성/안전성 균형을 위해 디코딩 조합 튜닝이 필요합니다.

### 6) 파라미터 효율 미세조정(PEFT)

전체 모델 파인튜닝은 비용이 큽니다.  
LoRA, Prefix Tuning 같은 PEFT는 적은 파라미터만 학습해 비용을 줄이면서 도메인 적응을 수행합니다.

선택 기준:
- 예산/시간이 제한적이면 PEFT 우선
- 모델 행동을 크게 바꿔야 하면 전체 파인튜닝 고려

### 7) 환각 완화 전략

환각은 "정답이 없는 상태에서 그럴듯한 문장을 생성"하는 현상입니다.

완화 방법:
1. RAG로 근거 문서 주입
2. 답변 형식에 근거 인용 강제
3. 신뢰도 낮을 때 "모름" 답변 허용
4. 후처리 검증기(규칙/모델) 추가
5. 금지 도메인에 대한 차단 정책

### 8) 에이전트형 파이프라인 기초

단일 프롬프트로 어려운 문제를 해결하기 어려운 경우,  
"계획 -> 검색 -> 도구 호출 -> 검증 -> 응답" 구조의 에이전트 파이프라인을 사용합니다.  
이때 도구 호출 실패/반복 루프/비용 폭증을 방지하는 제어 로직이 중요합니다.

### 9) 프롬프트 설계 원칙

좋은 프롬프트는 길이가 길어서가 아니라 "역할과 제약이 명확"해서 좋습니다.

핵심 구조:
1. 역할(Role): 너는 무엇을 해야 하는가
2. 목표(Goal): 무엇을 산출해야 하는가
3. 근거(Context): 어떤 자료를 우선 참고해야 하는가
4. 제약(Constraints): 금지 규칙, 안전 규칙, 형식 규칙
5. 출력 포맷(Output Format): JSON/표/불릿 등

실무에서는 자유 텍스트보다 구조화 출력(JSON schema)을 강제하는 편이 후처리 안정성이 높습니다.

### 10) RAG 고급 설계

RAG는 단순 검색이 아니라, 다음 단계의 품질 합성 문제입니다.

- 청킹(Chunking): 문서 분할 단위(너무 크면 노이즈, 너무 작으면 맥락 손실)
- 임베딩(Embedding): 의미 검색 품질 결정
- 검색(Retrieval): dense/sparse/hybrid 선택
- 재랭킹(Re-ranking): 상위 후보 정밀 정렬
- 컨텍스트 압축: 토큰 제한 내 근거 유지

권장 흐름:
`문서 정제 -> 청킹 -> 인덱싱 -> 1차 검색 -> 재랭킹 -> 컨텍스트 구성 -> 응답 생성 -> 근거 검증`

### 11) 정렬(Alignment) 관점: SFT, RLHF, DPO

- SFT: 지시 수행 능력의 기본 틀 형성
- RLHF: 인간 선호를 보상으로 학습
- DPO: 선호쌍 비교를 통한 직접 최적화(실무 단순화 장점)

핵심은 "정답률"이 아니라 "사용자 기대와 정책 준수"를 모델 행동에 반영하는 것입니다.

### 12) 추론 최적화(Inference Optimization)

LLM 운영 비용의 대부분은 추론에서 발생합니다.

- KV Cache: 디코딩 반복 계산 절감
- Quantization(8bit/4bit): 메모리/속도 최적화
- Dynamic Batching: 처리량 증가
- Speculative Decoding: 지연시간 단축

정확도 손실과 비용 절감의 균형을 환경별로 실험해야 합니다.

### 13) 생성형 AI 평가 체계

평가는 하나의 숫자로 끝나지 않습니다.

- 오프라인: golden set 기준 정확성/근거성/포맷 준수
- 온라인: 사용자 만족도, 재질문율, 실패율
- 안전성: 금지 응답 차단율, 민감정보 누출률

LLM-as-judge는 빠르지만 편향될 수 있으므로 사람 평가와 혼합하는 것이 안전합니다.

### 14) 장문 컨텍스트 전략

컨텍스트가 길어질수록 품질이 항상 좋아지는 것은 아닙니다.  
중요하지 않은 문서가 늘면 오히려 정답 근거가 희석될 수 있습니다.

실무 팁:
1. 질의 중심 청킹
2. 중복 제거
3. 출처 신뢰도 기반 필터
4. 요약 후 재검색(iterative retrieval)

### 15) 구조화 출력과 도구 호출

실서비스 연동에서는 자연어보다 구조화 결과가 중요합니다.

- JSON schema 강제
- 필드 검증 및 기본값 처리
- 도구 호출 실패 시 fallback 경로
- 응답 후 검증기(validator) 적용

이 흐름이 있으면 LLM 출력을 API/업무시스템과 안전하게 연결할 수 있습니다.

---

## 실무에서 자주 틀리는 포인트

1. "모델 크기만 키우면 해결"이라는 접근  
2. RAG 없이 내부 지식으로만 운영  
3. 프롬프트만 개선하고 검색 품질은 방치  
4. 출처 없는 답변을 신뢰  
5. 안전 정책(금지 주제, 개인정보) 미적용  
6. 청킹 전략 없이 임의로 문서를 잘라 검색 품질 저하  
7. 오프라인/온라인 평가를 분리하지 않아 개선 방향 상실  
8. 추론 비용/지연시간을 측정하지 않고 배포  
9. JSON 출력 검증 없이 다운스트림 시스템에 바로 전달

---

## Python 샘플 코드 (토큰화 + 미니 RAG)

토큰화 예시(사전 다운로드 필요):

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")
text = "Large language models learn from token sequences."
encoded = tokenizer(text, return_tensors="pt")
print("input_ids:", encoded["input_ids"][0][:10].tolist())
print("num_tokens:", encoded["input_ids"].shape[1])
```

TF-IDF 기반 미니 RAG 예시(외부 API 없이 구조 이해용):

```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
import numpy as np

docs = [
    "RAG는 검색된 문서를 컨텍스트로 넣어 답변 근거를 강화한다.",
    "파인튜닝은 모델 파라미터를 업데이트해 특정 도메인 성능을 높인다.",
    "환각은 사실이 아닌 내용을 사실처럼 생성하는 현상이다.",
]

vectorizer = TfidfVectorizer()
doc_vectors = vectorizer.fit_transform(docs)


def retrieve(query: str, top_k: int = 2):
    q_vec = vectorizer.transform([query])
    scores = cosine_similarity(q_vec, doc_vectors).flatten()
    top_idx = np.argsort(scores)[::-1][:top_k]
    return [(docs[i], float(scores[i])) for i in top_idx]


query = "RAG와 파인튜닝의 차이를 설명해줘"
results = retrieve(query, top_k=2)
for i, (doc, score) in enumerate(results, start=1):
    print(f"[{i}] score={score:.4f} | {doc}")

# 실제 서비스에서는 아래 retrieved context를 LLM 입력 프롬프트에 붙여 사용
context = "\n".join([r[0] for r in results])
prompt = f"다음 근거를 참고해 답변하라.\n근거:\n{context}\n질문:{query}"
print("\n---prompt preview---\n", prompt)
```

하이브리드 검색 + 간단 재랭킹 예시:

```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
import numpy as np

docs = [
    "RAG는 검색된 문서를 컨텍스트로 넣어 답변 근거를 강화한다.",
    "파인튜닝은 모델 파라미터를 업데이트해 특정 도메인 성능을 높인다.",
    "Prompt Injection은 모델 지시를 우회하려는 공격이다.",
    "LLM 평가는 정확성, 근거성, 안전성, 비용을 함께 본다.",
]
vectorizer = TfidfVectorizer()
doc_vec = vectorizer.fit_transform(docs)

def keyword_overlap_score(query: str, doc: str) -> float:
    q_tokens = set(query.lower().split())
    d_tokens = set(doc.lower().split())
    if not q_tokens:
        return 0.0
    return len(q_tokens & d_tokens) / len(q_tokens)

def hybrid_retrieve(query: str, top_k: int = 3, alpha: float = 0.7):
    q_vec = vectorizer.transform([query])
    dense = cosine_similarity(q_vec, doc_vec).flatten()
    sparse = np.array([keyword_overlap_score(query, d) for d in docs])
    score = alpha * dense + (1 - alpha) * sparse
    idx = np.argsort(score)[::-1][:top_k]
    return [(docs[i], float(score[i])) for i in idx]

query = "RAG와 평가 지표를 설명해줘"
for i, (doc, score) in enumerate(hybrid_retrieve(query), start=1):
    print(f"[{i}] {score:.4f} | {doc}")
```

구조화 출력(JSON) 검증 예시:

```python
import json

REQUIRED_KEYS = {"answer", "citations", "confidence"}

def validate_json_output(text: str):
    obj = json.loads(text)
    missing = REQUIRED_KEYS - set(obj.keys())
    if missing:
        raise ValueError(f"missing keys: {missing}")
    if not isinstance(obj["citations"], list):
        raise ValueError("citations must be list")
    if not (0.0 <= float(obj["confidence"]) <= 1.0):
        raise ValueError("confidence must be in [0,1]")
    return obj

sample = '{"answer":"RAG는 외부 문서를 검색해 근거를 보강합니다.","citations":["doc_1"],"confidence":0.82}'
parsed = validate_json_output(sample)
print("validated:", parsed)
```

---

## 미니 과제

1. 토크나이저를 `bert-base-uncased`와 `gpt2`로 바꿔 토큰 길이 비교  
2. 미니 RAG 문서 수를 3 -> 20으로 늘려 검색 품질 확인  
3. 답변 템플릿에 "근거 인용" 형식 추가  
4. 하이브리드 검색(alpha) 값을 바꿔 검색 순위 변화를 비교  
5. JSON 출력 검증기를 통과하지 못한 케이스 3개 설계  
6. latency/비용/정확성을 동시에 기록하는 평가표 작성

---

## 핵심 용어

- Tokenizer, Token ID, Embedding, Context Window
- Pretraining, SFT, RLHF, Alignment
- RAG, Retriever, Re-ranking, Grounding
- Hallucination, Prompt Injection, Safety Filter
- DPO, PEFT, Quantization, KV Cache
- Hybrid Retrieval, Chunking, Structured Output
- Calibration, Golden Set, LLM-as-judge

---

## 추천 자료

- [Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/chapter1/1)
- [Attention Is All You Need](https://arxiv.org/abs/1706.03762)
- 도서: `Natural Language Processing with Transformers`
- 도서: `Speech and Language Processing` (Jurafsky & Martin, 최신 초안)
- 도서: `Designing Machine Learning Systems` (LLM 운영 관점)

---

## 이해도 점검 질문

1. 토크나이저 선택이 모델 비용/성능에 영향을 주는 이유는?  
2. 파인튜닝과 RAG를 각각 선택해야 하는 조건은 무엇인가?  
3. Temperature와 Top-p를 동시에 조정할 때 주의할 점은?  
4. 환각 완화 전략을 3가지 이상 설명하고 장단점을 말할 수 있는가?  
5. 하이브리드 검색과 재랭킹이 필요한 이유를 설명할 수 있는가?  
6. SFT/RLHF/DPO의 역할 차이를 설명할 수 있는가?  
7. 추론 최적화(KV cache/quantization)의 트레이드오프를 설명할 수 있는가?  
8. 에이전트 파이프라인에서 실패 제어가 필요한 이유는 무엇인가?  
9. 구조화 출력 검증이 없는 경우 어떤 운영 장애가 발생할 수 있는가?

---

다음 학습: [6단계_책임있는 AI와 보안.md](6단계_책임있는%20AI와%20보안.md)
