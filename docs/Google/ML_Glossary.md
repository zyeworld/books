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
- F1: (2 * precision * recall) / (precision + recall)

### Area under the...

- Precision-Recall curve `= PR AUC`: binary classification에서 threshold에 따른 (Recall, Precision) 그래프
- ROC curve `= AUC`: threshold에 따른 (False Positive Rate, True Positive Rate) 그래프
    - Receiver-Operating Characteristic이란 말은 2차세계대전 때 레이더 탐지 분야에서 나왔다 한다

### Artificial general intelligence

> A non-human mechanism that demonstrates a *broad* range of problem solving, creativity, and adaptability.

### Artificial intelligence

> A non-human program or model that can solve sophisticated tasks

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

### Candidate sampling

- 정답은 항상 정적 강화하되 오답은 (일부만 추려서) 가끔가다만 부적 강화하기
- ex: 개 사진 보여주고 이 사진이 뭐냐? -> '개' 수치는 높아야 하고 나머지 수치는 낮아야 함 -> 나머지 수치(고양이, 사람, 나무...) 중에서는 일부만 랜덤으로 뽑아서 평가하기

### Chain-of-thought prompting

> How many g forces would a driver experience in a car that goes from 0 to 60 miles per hour in 7 seconds? **In the answer, show all relevant calculations.**

- 정답이 말이 되는지 우리가 더 잘 파악 가능
- 주의: 이게 모델의 interpretability를 높여주는 건 아님. (LLM이 black box model임은 여전)

### Class-imbalanced dataset

데이터셋에 각 label에 해당하는 데이터 개수가 현저히 다른 경우 `<-> class-balanced`

- 해결법: 각 batch에 class가 골고루 들어가도록, 다수인 class를 downsampling하고 upweight하기(개수 줄인 대신 틀리면 더 큰일나게)

### Clustering

- Centroid-based clustering: 체계 없음
    - k-means
- Hierarchical clustering: 체계 있음
    - Agglomerative: 모으기
    - Divisive: 쪼개기

### Co-adaptation

어떤 뉴런이 (전체적인 신경망이 아닌) 특정 뉴런들 몇 개의 출력값에만 좌우되는 문제. 오버피팅으로 이어질 수 있음.

- 해결법: Dropout regularization으로 뉴런 무작위로 없애가며 학습

### Collaborative filtering

다른 사람들 데이터로 내 관심사 예측하기

### Concept drift

세상이 바뀌어서 모델 예측 수준이 떨어지는 것. 어떤 특성이 시간에 따라 고정성을 가지지 않으면 일어남(nonstationarity).

### Confabulation

허담증(자기의 공상을 실제의 일처럼 말하면서 자신은 그것이 허위라는 것을 인식하지 못하는 정신병적인 증상). AI Hallucination(환각)과 같은 뜻이지만 보다 적합한 용어.

### Configuration

모델 레이어나 하이퍼파라미터 등 설정하기

- [HParam](https://www.tensorflow.org/tensorboard/hyperparameter_tuning_with_hparams)
- [Gin](https://github.com/google/gin-config)
- [Fiddle](https://github.com/google/fiddle)

### Constituency parsing

문장을 문법 요소로 쪼개기

### Context window

프롬프트를 토큰 몇 개까지 처리할 수 있는지

### Conversational coding

그냥 바이브코딩을 더 있어보이게 한 말

### Crash blossom

중의적인 의미를 가진 문구

### Data analysis

> Obtaining an understanding of data by considering samples, measurment, and visualization.

### Data parallelism

(모델 크기가 작을 때) 모델 전체를 여러 장치에 복사해 학습/추론 과정 병렬화. (더 빠름)

비교 - Model parallelism: (모델 크기가 클 때) 모델을 여러 부분으로 쪼개 여러 장치에 나누어 담아 학습/추론 과정 병렬화. (더 느림)

### Decision forest

Decision tree들을 합쳐서 예측하기

- Random forest
- Gradient boosted tree

### Deep model(Deep neural network)

> A neural network containing more than one hidden layer

### Denoising

노이즈를 입힌 데이터에서 원래 데이터를 예측하는 모델 학습시키기(self-supervised learning. masked language model 등)

### Depth

입력 레이어 빼고 hidden, output, embedding 레이어 개수 합

### Differential privacy

개별 데이터에 있는 민감한 정보를 모델에 학습시키지 않기 위해 노이즈 추가 등 하기

### Direct prompting

Zero-shot prompting.

### Discriminative model

Label을 예측하는 모델. 분류나 회귀 모델 전부 포함. vs. Generative model.

### Disparate impact

어떤 결정이 여러 인간 집단에 주는 영향이 다른 상황. (각 집단을 차별해서 그 결정을 한 건지는 중요하지 않음)

### Disparate treatment

사회적으로 민감한 특성(sensitive attirubte)을 의사결정 과정에서 보는 요소 중 하나로 넣어서, 여러 인간 집단을 차별하게 되는 상황.
(민감한 특성 자체가 아니더라도 그 proxy가 되는 특성이 들어가 있을 수도 있음)

### Distillation

큰 모델(teacher)을 작은 모델(student)로 따라하기

### Dynamic

= Online. 무언가를 자주/계속적으로 할 때 씀. Dynamic model(계속 재학습시키는 모델) / Dynamic training(자주 학습시키기) / Dynamic inference(요청 있을 때마다 예측값 내기)

### Earth mover's distance(EMD)

두 분포의 유사성 측정 지표. 그래프가 쌓인 흙(Earth)이라 생각하고 한 그래프에서 다른 그래프를 만드려면 흙을 얼마나 옮겨야 하나(양 * 거리) 측정. 확률분포의 경우 "Wasserstein 거리 W_1"과 같은 말.

### Edit distance

두 문자열의 유사성 측정 지표.

- Levenshtein distance: 한 문자열에서 다른 문자열을 만드려면 삽입/삭제/치환 연산을 최소 몇 번 해야 하나.

### Einsum notation

Einstein summation. 텐서 곱셈 쉽게 나타내기. [참고](https://ita9naiwa.github.io/numeric%20calculation/2018/11/10/Einsum.html)

```python
# A의 차원, B의 차원, ... -> 결과 차원
np.einsum('ik,kj->ij', A, B) # matmul
torch.einsum('ik,kj->ij', [A, B])
np.einsum('ij,j->i', A, x) # matrix * vector
np.einsum('i,i->', x, y) # vector dot product
np.einsum('i,j->ij', x, y) # vector cross product
np.einsum('ij->', A) # sum
np.einsum('ij->i', A) # sum the 2nd dimension ([[1,2],[3,4]] -> [3,7])
np.einsum('ij->ji', A) # transpose
np.einsum('ii->', A) # trace
```

### Embedding

고차원 데이터(많은 라벨의 자료가 one-hot encoding된 입력 벡터 등)를 저차원으로 표현하기.

- 비교 - Hashing: 많은 라벨을 적은 라벨에 그냥 나누어 담기(해시 충돌 발생해도 신경 X)

### Entropy

확률분포 `p(x)`에 대해 `H(p) = -p(x) log p(x)의 합`. 두 가지 값으로 이루어진 집합에서 `-a log(a) -(1-a)log(1-a)`. a=0.5일 때 1.

- Information gain: Decision forest에서 [한 노드의 엔트로피]와 [그 자식들의 엔트로피 가중평균]의 차이. 최대화해야 좋음.

- Gini impurity: 두 가지 값으로 이루어진 집합에서 `1 - (a^2 + (1-a)^2)`. a=0.5일 때 0.5.

- Cross-entropy: 두 확률분포 `p(x), q(x)`에 대해 `H_p(q) = -q(x) log p(x)의 합`. 확률분포 간 차이의 지표.

- Kullback-Leibler divergence: `D_KL(q||p) = H_p(q) - H(q)`. Cross-entropy와 entropy 차이. 항상 0 이상. 보통 q에 실제 확률분포, p에 예측한 확률분포를 넣고 차이를 보는 지표.

### Epsilon greedy policy

Random policy를 따를 확률이 `e`이고 Greedy policy를 따를 확률이 `1-e`인 policy. Episode(Agent가 환경을 학습하려는 시도)를 여러 번 거치며 e를 점차 낮춤. (일단 맘대로 탐색하고 나중에 진지하게 하기)

### Evaluation

Validation set이나 Test set으로 성능 측정하기. 또는 LLM 모델 성능 측정.

### Exploding gradient problem

RNN 등에서 gradient가 매우 커지는 문제. 해결책: Gradient clipping(최댓값 제한) 등.

- 비교 - Vanishing gradient problem: 앞쪽에 있는 hidden layer들의 gradient가 매우 작아지는 문제. 해결책: Long Short-Term Memory, Auxiliary loss 등.

### Factuality

사실성. 사실에 기반했는지.

- 비교 - Groundedness: 특정 입력 데이터를 주었을 때 그 데이터에 기반했는지.

### Fairness metric

공평성에 대한 측정 가능한 척도. 인종 같은 사회적으로 민감한 특성(sensitive attribute)을 다룰 때 씀. 각각의 척도는 상충하기도 함(incompatible).

- Equality of opportunity: 각 그룹에 대해 True positive rate가 같아야 함 (positive가 좋은 결과라 했을 때)
- Equalized odds: 각 그룹에 대해 True positive rate와 False positive rate가 같아야 함
- Predictive parity: 각 그룹에 대해 Precision이 같은가
- Counterfactual fairness: Sensitive attribute만 바꿨을 때 예측 결과가 똑같은가
- Demographic parity: (결과 전체적으로) Sensitive attribute와 결과가 독립인가

### Fast decay

LLM 학습시키는 동안 학습률을 확 감소시켜서 오버피팅 막기

### Federated learning

스마트폰 등 여러 장치에 모델을 복사해 학습을 시킨 다음, 모델만 중앙 서버로 보내 업데이트하기. 장치에 있는 데이터는 서버에 보내지지 않음.

- Secure aggregation: 개별 장치에서 학습한 모델은 zero-sum mask로 암호화되어 중앙 서버로 보내지고, 그것들이 전부 합쳐진 결과만 복호화가 가능.
    - [Practical Secure Aggregation for Privacy-Preserving Machine Learning](https://research.google/pubs/practical-secure-aggregation-for-privacy-preserving-machine-learning/)

- Differential privacy: 모델이 특정 장치에만 있는 특별한 정보를 외우는(model memorization) 걸 줄이기 위해 희귀한 데이터를 필터링하는 등.
    - [The Algorithmic Foundations of Differential Privacy](https://www.cis.upenn.edu/~aaroth/privacybook.html)

> [구글에서 제공하는 Federated Learning 만화](https://federated.withgoogle.com/).
> 음, 이걸 읽으면 참 비즈니스 연구자의 관점은 소비자가 느끼는 바와 다르다는 생각이 든다.
> 코미디 만화인 건 알겠는데, 화려해 보이는 기술 이름이 나오면 무조건 도입하는 상사가 나오고... 모든 이용자에게 영향을 줄 서비스를 만드는데 보안 같은 거 모르는 인턴들로 팀을 꾸리고... "(머신 러닝에) 가장 좋은 데이터는 바로 여기, 우리들이 매일 쓰는 휴대폰 안에 있다" 같은 대사가 나오고...
> 일부러 이 기술을 못 미더워 보이게 만드려고 만화가가 수작을 부렸나? 싶을 정도다.

### Feedback loop

모델이 내놓는 결과가 나중에 어떤 식으로라도 입력 데이터에 영향을 주는 상황.

### Feedforward neural network

초기 Deep neural network처럼 뒤에서 앞으로 cyclic하게 연결된 경우가 없는 신경망. (반대로는 RNN 등)

### Fine-tuning

- Full fine-tuning: 모든 파라미터 수정
- Parameter-efficient tuning: 일부 파라미터만(보통 출력 레이어 근처) 수정
- 그 외: 출력 레이어 근처 레이어 개수 늘리기 등

- Prompt tuning: 실제 프롬프트에 prefix 다는 것 학습. 보통 입력 레이어에만 달음.
- Prefix tuning: 모든 레이어에 prefix 달기.
- Instruction tuning: (생성형 AI에서) 여러 과제에 대한 지시 프롬프트로 zero-shot prompt 능력 키우기

### Fraction of successes

모델이 생성한 텍스트(코드나 수학 등) 중 성공적인 것의 비율

### Zero-shot learning

학습하지 않은 과제에 대해 추론하라고 하는 것.

- One-shot learning: 예시 단 하나로 분류 모델 학습시키기
- Few-shot learning: 예시 몇 개로.

### Zero-shot prompting

LLM에 예시 없이 질문하기

```
What is the official currency of the specified country?
India:
```

- One-shot prompting

```
What is the official currency of the specified country?
France: EUR
India:
```

- Few-shot prompting

```
What is the official currency of the specified country?
France: EUR
United Kingdom: GBP
India:
```

## ML Glossary에 나와 있는 참고자료

- AdaGrad: [Adaptive Subgradient Methods for Online Learning and Stochastic Optimization](https://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)
- BERT: [Open Sourcing BERT: State-of-the-Art Pre-training for Natural Language Processing](https://research.google/blog/open-sourcing-bert-state-of-the-art-pre-training-for-natural-language-processing/)
- BLEU: [BLEU: a Method for Automatic Evaluation of Machine Translation](https://aclanthology.org/P02-1040.pdf)
- Convex optimization: [Convex Optimization](https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf)
- Co-training: [Combining Labeled and Unlabeled Data with Co-Training](https://www.cs.cmu.edu/%7Eavrim/Papers/cotrain.pdf)
- Counterfactual fairness: [When Worlds Collide: Integrating Different Counterfactual Assumptions in Fairness](https://papers.nips.cc/paper/2017/file/1271a7029c9df08643b631b02cf9e116-Paper.pdf)
- Dropout regularization: [Dropout: A Simple Way to Prevent Neural Networks from Overfitting](https://jmlr.org/papers/volume15/srivastava14a/srivastava14a.pdf)
- Fairness Metric: [Fairness Definitions Explained](https://fairware.cs.umass.edu/papers/Verma.pdf)
- Incompatibility of Fairness Metrics: [On the (im)possibility of fairness](https://arxiv.org/pdf/1609.07236)
- sepCNN: [Xception: Deep Learning with Depthwise Separable Convolutions](https://arxiv.org/pdf/1610.02357)
- Inception: [inception](https://github.com/tensorflow/tpu/tree/master/models/experimental/inception)

## 오탈자 / 오개념 수정 리스트

### average precision at k

The formula should be:
```
average precision at k = \frac{1}{k} \sum_{i=1}^{k} precision at i for each relevant item
```
and the following text "where n is the number of relevant items in the list" should be removed.

### black box model>

title includes unnecessary '>'.

### condition

Part of the definition is missing. It may be edited like "In a decision tree, any node that **is not an endpoint. For example, the following** decision tree contains two conditions:"

### early stopping

"Contrast with early exit" links to a non-existing entry of "early exit".

### precision at k (precision@k)

In the example at the end, "Four of the first five movies are very funny" should be changed to "Three of the..." according to the data. The equation that follows must be edited too.

### Q

The link `https://developers.google.com/machine-learning/glossary#q` doesn't lead to the anchor point `Q` in the glossary, but rather the search query box.

