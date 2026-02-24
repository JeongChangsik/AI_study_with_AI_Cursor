# 6단계_책임있는 AI와 보안

---

## 개요

6단계는 모델 성능 외에 반드시 관리해야 하는 리스크를 다루는 단계입니다.  
편향, 프라이버시, 저작권, 보안 이슈를 이해하고 최소 점검 기준을 세웁니다.

---

## 꼭 알아야 할 핵심 설명 (서술형)

AI 시스템은 정확도가 높아도 위험할 수 있습니다. 학습 데이터가 특정 집단에 불리하게 편향되어 있으면, 모델은 높은 평균 성능을 보이더라도 실제 사용자에게 불공정한 결과를 줄 수 있습니다.

프라이버시와 저작권은 사후 대응이 어려운 영역입니다. 데이터 수집 단계에서 출처, 사용 권한, 개인정보 여부를 먼저 점검하지 않으면 배포 이후 법적/신뢰 리스크가 크게 발생할 수 있습니다.

생성형 AI 환경에서는 보안도 필수입니다. Prompt Injection이나 Data Poisoning 같은 공격은 모델 동작을 왜곡하거나 민감 정보를 노출시킬 수 있으므로, 입력 검증/출력 필터링/권한 분리 전략을 함께 설계해야 합니다.

---

## 핵심 용어

- Fairness, Bias, Sampling Bias
- Privacy, PII, De-identification
- License, Copyright, Data Governance
- Prompt Injection, Data Poisoning, Model Leakage

---

## 추천 자료

- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [Google Responsible AI](https://ai.google/responsibility/)
- [Fairness and Machine Learning](https://fairmlbook.org/)

---

## 날짜별 학습 기록

### 첫 작성 상태
- 다음 작성 시, 편향 점검 체크리스트와 LLM 보안 기본 사례를 날짜별로 누적합니다.

---

다음 학습: [7단계_내 AI 개발 시작.md](7단계_내%20AI%20개발%20시작.md)
