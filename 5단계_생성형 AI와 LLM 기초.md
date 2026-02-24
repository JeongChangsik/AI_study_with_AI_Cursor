# 5단계_생성형 AI와 LLM 기초

---

## 개요

5단계는 생성형 AI와 LLM의 동작 원리를 이해하는 단계입니다.  
토큰, 임베딩, 다음 토큰 예측, RAG/파인튜닝 차이를 명확히 구분하는 것을 목표로 합니다.

---

## 꼭 알아야 할 핵심 설명 (서술형)

LLM은 본질적으로 "다음 토큰 예측" 목표로 학습되지만, 대규모 데이터와 모델 규모 덕분에 번역, 요약, 추론, 코드 생성 같은 다양한 능력이 나타납니다. 즉 단순한 학습 목표가 큰 표현 능력으로 확장되는 구조를 이해해야 합니다.

실무에서는 파인튜닝과 RAG의 역할을 구분해야 합니다. 파인튜닝은 모델 파라미터 자체를 바꿔 행동을 조정하고, RAG는 외부 지식을 검색해 컨텍스트로 주입하는 방식입니다. 둘은 대체재가 아니라 문제에 따라 조합 가능한 전략입니다.

또한 LLM은 환각, 근거 부족, 프롬프트 주입 공격 같은 리스크가 있습니다. 따라서 성능만 보는 것이 아니라 근거성, 안정성, 보안성을 함께 점검해야 실제 서비스 품질을 확보할 수 있습니다.

---

## 핵심 용어

- Tokenizer, Token, Embedding
- Pretraining, Fine-tuning, Instruction Tuning
- RAG, Retrieval, Context Window
- Hallucination, Prompt Injection, Grounding

---

## 추천 자료

- [Hugging Face NLP Course](https://huggingface.co/learn/nlp-course/chapter1/1)
- [Attention Is All You Need](https://arxiv.org/abs/1706.03762)
- 도서: `Natural Language Processing with Transformers`

---

## 날짜별 학습 기록

### 첫 작성 상태
- 다음 작성 시, 토큰화/임베딩과 RAG/파인튜닝 비교 내용을 날짜별로 누적합니다.

---

다음 학습: [6단계_책임있는 AI와 보안.md](6단계_책임있는%20AI와%20보안.md)
