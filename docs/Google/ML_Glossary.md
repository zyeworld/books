# Machine Learning Glossary

- `Link`: [ML Glossary](https://developers.google.com/machine-learning/glossary)

> 책은 아니지만 이런 문서들도 여기에 쓰려 합니다.
>
> 그냥 머신러닝 관련 용어집이기 때문에, A부터 Z까지 읽으면서 메모하고 싶은 부분만 하겠습니다.
>
> 만약 오탈자나 오개념을 발견하면 모아 두었다가 나중에 구글에다가 피드백으로 보내려 합니다.

## 정리

### Accuracy / Precision / Recall

- Accuracy(정확도): 얼마나 맞췄냐
- Precision(정밀도): 참이라고 예측한 것 중에 얼마나 진짜 참이냐
- Recall(재현율): 진짜 참인 것 중에 얼마나 참이라고 예측했냐

### Area under the...

- Precision-Recall curve `= PR AUC`: binary classification에서 threshold에 따른 (Recall, Precision) 그래프
- ROC curve `= AUC`: threshold에 따른 (False Positive Rate, True Positive Rate) 그래프
    - Receiver-Operating Characteristic이란 말은 2차세계대전 때 레이더 탐지 분야에서 나왔다 한다


### Autoencoder

- 고차원 입력 `-> Encoder ->` 저차원 데이터 `-> Decoder ->` 원본 최대한 복원하기.
- 중요한 부분만 어떻게 남길지 알아서 학습
- Variational Autoencoder(VAE): 고차원 입력 `-> Encoder ->` 데이터의 확률분포 `->` 하나 뽑기 `-> Decoder ->` 원본 최대한 복원하기.
    - [한글 설명](https://medium.com/@hugmanskj/autoencoder-%EC%99%80-variational-autoencoder%EC%9D%98-%EC%A7%81%EA%B4%80%EC%A0%81%EC%9D%B8-%EC%9D%B4%ED%95%B4-171b3968f20b)

### Automatic evaluation

- Programmatic evaluation: 간단한 프로그램으로 모델의 답 검사하기
    - ROUGE(Recall-Oriented Understudy for Gisting Evaluation): 재현율 기반이므로 요약 과제에 적합
        - ROUGE-L: 모델과 정답 텍스트의 Longest Common Subsequence 비교
        - ROUGE-N: (N에 따라) 공통 N-gram 개수 비교
        - ROUGE-S: N-gram인데 skip-gram(건너뛰기) 매칭도 인정
    - BLEU(Bilingual Evaluation Understudy): N-gram 비교. 정밀도 기반이므로 번역 과제에 적합
    - BLEURT(...from Transformers): LLM(BERT) 사용. 영어 의미 유사성도 파악해 좀 더 정확
- Autorater: human evaluation으로 만든 데이터로 모델 학습시키기

### Auto-regressive model

자신의 과거 예측 바탕으로 새 예측 하기 (LLM)

### Bias

- Reporting bias: 댓글창이 창나는 이유
- Historical bias: 역사적으로도 그래왔다
- Automation bias: 편한 거 하자
- Selection bias
    - Coverage bias: 한 쪽 의견만 들음
    - Non-response bias: (비슷) 의견 안 낸 사람들이 너무 많음
    - Sampling bias: 시끄러운 사람 의견만 들음
- Group attribution bias
    - In-group bias: 우리가 좋다
    - Out-group homogeneity bias: 남들은 똑같다
- Implicit bias: 나한테는 당연하다
- Confirmation bias: 내가 맞다 생각하는 쪽 말만 듣는다
- Experimenter's bias: 고등학교 소논문 대회

### Clustering

- Centroid-based clustering: 체계 없음
    - k-means
- Hierarchical clustering: 체계 있음
    - Agglomerative: 모으기
    - Divisive: 쪼개기


## ML Glossary에 나와 있는 참고자료

- AdaGrad: [Adaptive Subgradient Methods for Online Learning and Stochastic Optimization](https://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)
- BLEU: [BLEU: a Method for Automatic Evaluation of Machine Translation](https://aclanthology.org/P02-1040.pdf)


## 오탈자 / 오개념 수정 리스트

### average precision at k

The formula should be:
```
average precision at k = \frac{1}{k} \sum_{i=1}^{k} precision at i for each relevant item
```
and the following text "where n is the number of relevant items in the list" should be removed.

### precision at k (precision@k)

In the example at the end, "Four of the first five movies are very funny" should be changed to "Three of the..." according to the data. The equation that follows must be edited too.

