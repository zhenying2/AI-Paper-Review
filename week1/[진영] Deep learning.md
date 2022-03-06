# 1️⃣ Deep learning 
> Yann LeCun, Yoshua Bengio & Geoffrey Hinton (27 May 2015)
> 
> Nature volume 521, pages436–444(2015)

## ✔ Abstract
딥러닝은 다층 처리 구조로 구성된 모델이 복잡한 데이터를 표현하는 것을 배울 수 있도록 한다. 이 방법은 음성인식, 시각 물체의 인식, 물체 탐지, 다양한 분야(ex. 약, 유전학)에서 많은 발전을 이뤘다.
딥러닝은 복잡하게 얽혀있는 데이터를 역전파 알고리즘을 사용하여 다룬다. 
이때, 역전파 기법은 기계가 어떻게 내부 파라미터(이전 레이어의 표현으로부터 각 레이어의 표현을 계산)를 바꾸는지를 나타내는 것을 의미한다.
Deep convolutional nets(심층 합성곱)은 이미지,비디오, 스피치, 오디오 처리에 획기적인 발전을 가져왔고, Recurrent nets(순환신경망)은 텍스트나 음성과 같은 순차데이터에 발전을 가져왔다.


## ✔ What I learned
* 딥러닝은 단순한 모듈을 여러개의 층으로 쌓은 구조로, 각 모듈에서 input 데이터의 selectivity와 invariance를 모두 증가시킨다. selectivity와 invariance를 동시에 증가시킴에도,
하나의 feature을 학습하면서 가중치 조정시 나머지 feature들도 동시에 가중치가 조정되므로, 좋은 feature을 추출하기 위한 engineering skill이나 domain 지식이 없이도 자동으로
일반적인 learning procedure의 목적에 맞는 좋은 feature만 추출 가능하다.
* 딥러닝의 input vector와 output vector의 error와 평균 기울기를 계산하고 가중치를 조절할 때 stochastic gradient descent(SGD)를 많이 쓴다. SGD는 backpropagation(역전파)를 통해 계산할 수 있다.
* feedforward network는 각 layer을 사전훈련하여, deep network의 가중치를 적절한 값으로 초기화 할 수 있고, 최종 출력 layer을 다시 전체 시스템의 가장 상단에 추가하여 전체 네트워크를 조정할 수 있다.
* CNN은 다차원 데이터를 처리하기 위해 등장하였으며, convolution layer와 pooling layer로 구성되어 있다. convolution layer은 특징을 추출하는 단계이고, pooling layer은 특징을 압축하는 단계이다.
CNN은 사물이나 서비스의 이미지를 이해하는데 주로 사용된다.
* RNN은 관련 정보와 그 정보를 사용하는 지점 사이의 거리가 멀 경우 역전파 그래디언트가 줄어 학습능력이 저하되는 vanishing gradient problem이 발생한다.
이러한 문제를 해결하기 위한 것이 LSTM으로, LSTM은 RNN의 hidden state에 cell-state를 추가한 구조이다. cell state는 컨베이너 벨트 역할을 하며, state가 오래 경과하더라도
그래디언트가 전파가 잘 될 수 있도록 해준다.
## ✔ Introduction
Conventional machine-learning requried careful engineering and considerable domain expertise to design a feature extractor into a suitable internal representation or feature vector
from which the learning subsystem could detect or classify patterns in the input. Contrary, Representation learning is a set of methods that allows a machine to be fed with
raw data and to automatically discover the representations needed for detection or classification. Deep learning methods are one of the representation learning with multiple levels
of representation. The key aspect of deep learning is that each layers of features are not designed by human engineers. They are learned from data using a general-purpose learning procedure.

요약: 딥러닝은 데이터를 통해 기계 스스로 학습하며, representation learning의 각 레벨을 거치면서 단순하지만 비선형 모듈을 이용하여 입력데이터를 더 높은(추상적인) 표현으로 바꾼다.
딥러닝은 수년간 빛을 보지 못 했지만, 이미지 인식, 음성 인식, 자연어 처리 부분에서 다른 머신 러닝 기법들보다 우수한 성과를 거두면서 인정받게 되었다.

## ✔ Supervised learning
compute an objective function that measures the error between the output scores and the desired pattern of scores. machine then modifies its internal adjustable parameters
to reduce this error. These adjustable parameters called weights. To properly adjust the weight vector, the learning algorithm computes a gradient vector that indicates by
what amount the error would increase or decrease if the weight were increased by a tiny amount.
A deep learning architecture is a multilayer stack of simple modules, all of which are subject to learning, and many of which compute non-linear input-output mappings.
Each module in the stack transforms its input to increase both the selectivity and the invariance of the representation. 

## ✔ Backpropagation(역전파) to train multilayer architectures
multilayer architectures can be trained by simple stochastic gradient descent. The backpropagation procedure to compute the gradient of an objective function with respect to the weights of a multilayer
stack of modules is nothing more than a practical application of the chain rule for derivatives.The backpropagation equation can be applied repeatedly to propagate gradients
through all modules, starting from the output at the top all way to the bottom.
![image](https://user-images.githubusercontent.com/77235677/156907658-44cb34e0-d205-480f-aff1-3254f8563955.png)

요약: backpropagation(역전파)를 사용하여 모델의 가중치(weight)를 수정한다. 이때, backpropagation은 chain rule(미적분의 연쇄법칙)을 적용한다.
학습과정에서 한 층에서 다음 층으로 넘어가는 forward propagation에는 비선형함수가 사용되고, 현재 가장 유명한 비선형함수는 ReLU이다. 
90년대까지는 이러한 학습 방법이 poor local minima(weight configurations for which no small change would reduce the average error)가 생길 것이라고 우려했지만, 큰 문제가 아니라고 여러 이론과 경험적 결과에서 밝혀졌다.

## ✔ CNN(Convolutional neural networks)
ConvNets are designed to process data that come in the form of multiple arrays. The architecture of a typical ConvNet is structured as a series of stages. The first few stages
are composed of two types of layers: convolutional layers and pooling layers.the role of the convolutional layer is to detect local conjunctions of features from the previous layer.
The role of the pooling layer is to merge semantically similar features into one. 
![image](https://user-images.githubusercontent.com/77235677/156908033-be5220c2-0500-4e06-bb7f-4fc8439574a0.png)

## ✔ Distributed representations and language processing
learning distributed representations enable generalization to new combinations of the values of learned features beyond those seen during training. composing layers of
representation in a deep net brings the potential for another exponential advantage. Each word in the context is presented to the network as a one-of-N vector,
one component has a value of 1 and the rest are 0. neural networks just use big activity vectors, big weight matrices and scalar non-linearities to perform the type of
fast intuitive inference that underpins effortless commonsense reasoning. N-grams treat each word as an atomic unit, so they cannot generalize across semantically related sequences of words whereas neural language models can because they
associate each word with a vector of real valued features and semantically related words end up close to each other in that vector space.

요약: one-hot encoding은 표현하고 싶은 단어의 인덱스 값을 1 나머지 값들을 모두 0으로 설정한다. 원핫 인코딩을 통해 나온 벡터를 원핫 벡터라고 하고, 이 벡터의 차원은 어휘 집합의 크기와 동일하다.
그러나, 어휘의 집합이 커지면, 희소벡터(sparse vector_ 해당 단어 인덱스만 1이고 나머지 벡터 모두 0)와 같은 메모리/계산복잡도가 비효율적인 문제가 발생하고,
두 벡터의 내적이 항상 0이 되는 문제가 있다. (내적이 0이라는 것은 두 벡터가 직교한다=두 벡터가 항상 독립적이다 != 실제로는 두 단어사이에 전혀 연관성이 없지 않다.)
이러한 원-핫 벡터의 문제점을 해결하기 위한 방법이 바로 Distributed representation이다. 분산 표현은 1과 0으로 이뤄진 이진 벡터(sparse)를 연속형의 실수 값 벡터(dense vector)로 변환하여 표현한다.
2차원 벡터인 dense vector은 실수 값을 가지기 때문에 공간상에서 벡터 간의 거리나 유사도를 구할 수 있으며, 의미가 유사한 단어는 가깝게, 반대의 경우는 멀게 표현할 수 있다.

## ✔ Recurrent neural networks
![image](https://user-images.githubusercontent.com/77235677/156908907-4b7f16d7-5bcc-4946-8c81-41b21fb00f12.png)

RNN은 한 층의 출력이 순환하면서 다시 입력되는 재귀 결합을 가진 순환 신경망이다. 자신의 출력을 다시 자신에게 돌아오는 네트워크라고 보면 된다.
까다로운 구조의 네트워크는 이전의 CNN(이미지와 같은 정적인 데이터)과는 달리 시계열 및 가변 길이의 시간 개념의 데이터(자연언어처리 nlp)를 사용하기 때문에,
자신의 출력을 다시 자신에게 돌아오는 재귀 형태의 까다로운 구조를 가진다고 볼 수 있다. 

## ✔ The future of deep learning
논문에서는 사람과 동물이 학습하는 과정이 Unsupervised, 즉 정답을 제공하지 않아도 스스로 관찰을 통해 학습하는 방식이기 때문에 unsupervised learning이 중요해질 것으로 보고 있다.
또한, future progress in vision에는 CNN과 RNN을 결합한 강화학습일 것이라고 예상하고 있다. (deep learning과 강화학습은 사실 이미 분류 문제나 많은 video game과 같은 것을 학습하는데 사용되고 있다.)
한편, 자연어 처리에도 딥러닝이 효과적일 것이라고 보고 있다. 궁극적으로, AI에서의 주된 방향은 복잡한 추론을 사용한 표현학습 시스템일 것이라고 보고 있다.


