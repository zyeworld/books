# Machine Learning Glossary

- `Link`: [ML Glossary](https://developers.google.com/machine-learning/glossary)

> 책은 아니지만 이런 문서들도 여기에 쓰려 합니다.
>
> 머신러닝 관련 용어집이고, 나중에 제가 다시 봤을 때 헷갈릴 것 같은 개념들만 정리하겠습니다.
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

### Batch

- 크기:
    - Stochastic Gradient Descent(SGD): 1
    - Mini-batch: 적당히 작은 숫자(10~1000)
    - Full batch: 전체

### Batch normalization

- Activation function(ReLU, Sigmoid...) 입력이나 출력 정규화하기
- 효과: 이상치 가중치로부터 보호, 학습률 키우기 가능, 오버피팅 줄임

### Bellman equation

- Infinite-horizon 문제의 경우:
    - Action `a_t`를 통해 State를 `s_t -> s_{t+1}`로 옮겨다니며 받는 Payoff `r(s_t, a_t)`를 최대화하는 문제
    - 영원히 안 끝남(infinite-horizon). 대신 Impatience `gamma (0 ~ 1)`이 존재해 뒤로 갈수록 Payoff의 중요성이 덜해짐
    - 시작 state가 `s_0`일 때 최적해 `Q(s_0)`: "`gamma^t * r(s_t, a_t)`의 합(`t = 0 ~ infty`)"의 최댓값

- Principle of Optimality: 체스에서는 항상 "현재 상황에서 최선의 수"를 두어야 한다. 이산적인 단계로 이루어지는(discrete-time) 최적화 문제에 다이나믹 프로그래밍 도입.
- 즉 `Q(s_0)`은 각 `a_0`에 대해 구한 `r(s_0, a_0) + gamma * Q(s_1)`중 최댓값.

- Stochastic 문제의 경우:
    - Action `a_t`가 State를 `s_t`에서 어디로 옮겨갈지가 확률적으로 정해짐.
    - `gamma^t * r(s_t, a_t)`의 합의 **기댓값(E)**을 최대화해야 함
    - `Q(s_0)`은 각 `a_0`에 대해 구한 `r(s_0, a_0) + gamma * E(Q(s_1))` 중 최댓값.

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

### Boosting

- 단순한 분류 모델(weak model)을 반복적으로(iteratively) 합쳐 더 좋은 분류 모델(strong model) 만들기.
- 각 단계에서 현재의 strong model의 오차에 대한 weak model 만들어 더 합치기
- Gradient Boosted Decision Tree

### Broadcasting

- NumPy에서 행렬이나 스칼라 연산할 때 형변환처럼 알아서 행렬 개수 맞춰주는 거
- 차원을 뒤쪽부터 맞추는데 두 숫자가 같거나 하나가 1이어야 됨
```
A      (4d array):  8 x 1 x 6 x 1
B      (3d array):      7 x 1 x 5
Result (4d array):  8 x 7 x 6 x 5
```

### Bucketing(Binning)

온도 -> 더운가? 따뜻한가? 추운가?처럼 한 feature을 여러 binary feature로 바꾸기

### Clustering

- Centroid-based clustering: 체계 없음
    - k-means
- Hierarchical clustering: 체계 있음
    - Agglomerative: 모으기
    - Divisive: 쪼개기


## ML Glossary에 나와 있는 참고자료

- AdaGrad: [Adaptive Subgradient Methods for Online Learning and Stochastic Optimization](https://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)
- BERT: [Open Sourcing BERT: State-of-the-Art Pre-training for Natural Language Processing](https://research.google/blog/open-sourcing-bert-state-of-the-art-pre-training-for-natural-language-processing/)
- BLEU: [BLEU: a Method for Automatic Evaluation of Machine Translation](https://aclanthology.org/P02-1040.pdf)


## 오탈자 / 오개념 수정 리스트

### average precision at k

The formula should be:
```
average precision at k = \frac{1}{k} \sum_{i=1}^{k} precision at i for each relevant item
```
and the following text "where n is the number of relevant items in the list" should be removed.

### black box model>

title includes unnecessary '>'.

### precision at k (precision@k)

In the example at the end, "Four of the first five movies are very funny" should be changed to "Three of the..." according to the data. The equation that follows must be edited too.

