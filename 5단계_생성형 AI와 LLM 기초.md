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

---

## 실무에서 자주 틀리는 포인트

1. "모델 크기만 키우면 해결"이라는 접근  
2. RAG 없이 내부 지식으로만 운영  
3. 프롬프트만 개선하고 검색 품질은 방치  
4. 출처 없는 답변을 신뢰  
5. 안전 정책(금지 주제, 개인정보) 미적용

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

---

## 미니 과제

1. 토크나이저를 `bert-base-uncased`와 `gpt2`로 바꿔 토큰 길이 비교  
2. 미니 RAG 문서 수를 3 -> 20으로 늘려 검색 품질 확인  
3. 답변 템플릿에 "근거 인용" 형식 추가

---

## 핵심 용어

- Tokenizer, Token ID, Embedding, Context Window
- Pretraining, SFT, RLHF, Alignment
- RAG, Retriever, Re-ranking, Grounding
- Hallucination, Prompt Injection, Safety Filter

---

## 추천 자료

- [Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/chapter1/1)
- [Attention Is All You Need](https://arxiv.org/abs/1706.03762)
- 도서: `Natural Language Processing with Transformers`

---

## 이해도 점검 질문

1. 토크나이저 선택이 모델 비용/성능에 영향을 주는 이유는?  
2. 파인튜닝과 RAG를 각각 선택해야 하는 조건은 무엇인가?  
3. Temperature와 Top-p를 동시에 조정할 때 주의할 점은?  
4. 환각 완화 전략을 3가지 이상 설명하고 장단점을 말할 수 있는가?  
5. 에이전트 파이프라인에서 실패 제어가 필요한 이유는 무엇인가?

---

다음 학습: [6단계_책임있는 AI와 보안.md](6단계_책임있는%20AI와%20보안.md)
