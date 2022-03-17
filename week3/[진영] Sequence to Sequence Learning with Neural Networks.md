# 1️⃣ Sequence to Sequence Learning with Neural Networks

## ✔ Abstract
Deep Neural Networks(DNN)은 labeled training set에는 작동을 잘하는데, sequence to sequence를 mapping하는데에 어려움을 가지고 있다.
논문에서는, 다층구조의 long short-term memory(LSTM) 2가지(to map input sequence, to decode target sequence) 를 사용하여, DNN이 가진 문제를 해결하는 방법으로 제시한다.
LSTM also learned sensible phrase and sentence representations that are sensitive to word order and relatively invariant to the active and passive voice.
And also the writer found that reversing the order of the words in all source sentences improved the LSTM's performance markedly.

요약) DNN은 고정된 차원의 feature와 고정된 차원의 출력에 특화된 방법으로, 입력과 출력의 길이가 다른 데이터를 학습하고 응용하는데에 어려움이 있다. 이러한 어려움을 극복하기 위해
나온 모델이 LSTM이고, LSTM은 고정된 길이의 sequence를 입력받고, 입력 sequence에 알맞은 길이의 sequence를 출력해주는 모형이다.
여기에서 입력과 출력의 길이란, "I am jinyoung" 의 영어 문장을 한국어로 "나는 진영이야"로 번역하는 과정을 생각해 볼때, 여기에서의 입력의 길이는 "I", "am", "jinyoung" 이렇게 3개,
출력의 길이는 "나는", "진영이야" 이렇게 2개가 된다.

## ✔ Model
LSTM 기반의 Sequence to Sequence model은 encoder와 decoder part로 구성되어 있다. encoder은 입력 sequence의 상태를 추출하는 역할을, 
decoder은 encoder에서 생성된 상태를 초기값으로 사용하여 순차적으로 sequence를 생성하는 역할을 수행한다.

![image](https://user-images.githubusercontent.com/77235677/158810738-47306a93-e165-4b17-99ac-74eb9cc5c19d.png)

### 🔑 training
> 데이터를 전처리하여, sequence to sequence model 모형을 학습하는 단계

- encoder
> encoder은 입력 sequence를 순차적으로 LSTM에 입력받아서 sequence의 마지막에 상태를 추출한다. 문장의 끝을 나타내는 마침표(.)/?/! 등은 sequence의 종료를 나타내며,
이를 별도로 End of Sequence(EOS)로 표기한다.

- decoder
> decoder은 encoder에서 추출한 상태를 초기 상태로 받는 LSTM이 순차적으로 결과를 출력해준다. decoder의 초기 상태 입력으로는 EOS를 받는다.
EOS를 초기 값으로 받는 이유는, 학습 이후 모델을 사용할 때 시작 값을 알 수 없기 때문에 학습단계에서 강제로 EOS로 시작하도록 구성한 것이다.
decoder에서 모형이 학습하는 입력과 출력값에 대해 위 예시를 들어 다시 이해해보면, 
[EOS, "나는", "진영이야"]가 입력값이 되고, ["나는","진영이야",EOS]가 출력값이 된다.
입력값과 출력값에서 1개의 시점(시간차)이가 발생하는 것을 확인해 볼 수 있고, 이렇게 1 step offset으로 학습하는 방법을 teacher forcing이라고 한다.

## ✔ What I learned
Sequence to Sequence 모델은 고정된 크기의 context vector을 encoder 입력값으로 사용하기 때문에, 길이가 긴 context에 적합하지 못하다는 단점을 가진다.
이러한 점을 해결하고자 Sequence to Sequence 모델에 attention 기법을 적용한 ICLR 논문에 이어지고, transformer, GPT, BERT로 이어지는 기계번역 역사를 가진다.
encoder에 넣어주는 입력 단어의 순서를 바꿔서 학습시킬 때, 더 효율/성능이 높다!