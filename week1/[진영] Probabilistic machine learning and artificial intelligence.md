# 2️⃣ Probabilistic machine learning and artificial intelligence
> Zoubin Ghahramani
> 
> Nature (2015)

## ✔ Abstract
확률론적 모델링은 경험으로부터 기계가 학습하는 것을 이해하는 프레임워크를 제공하고, 경험을 통해 습득한 데이터로부터 학습하는 주된 이론/실질 적인 접근을 가져왔다. 
확률론적 프레임워크는 모델과 예측에 대한 불확실성을 어떻게 나타내고 제어할 것인지 조절하며, 과학 데이터 분석, 머신러닝, 로보틱스, 인지과학, AI 등에서 주된 역할을 하고 있다.
이 논문에서는 확률론적 프레임워크에 대해 소개하며, 확률론적 프로그래밍, 베이지안 최적화, 데이터 압축 및 자동 모델 발견과 같은 분야의 최첨단 발전 중 일부에 대해 논의한다.

## ✔ What I learned
Probability theory provides a framework for modelling uncertainty. Many aspects of learning and intelligence crucially depend on the careful probabilistic representation of uncertainty.
the writer focus on problems for which uncertainty is really a key ingredient where a decision may depend on the amount of uncertainty. And he highlight five areas of current
research at the frontier of probabilistic machine learning: probabilistic programming, Bayesian optimization, probabilistic data compression, hierarchical modelling
Generally, almost all training algorithms for neural networks can be seen as maximizing a likelihood. The likelihood is the probability of the outputs
given the inputs, or maybe a penalized likelihood if you are trying to avoid over-fitting.

* what is a model?
> A model is a description of possible data which could observe from a system.

모델이 잠재적인 데이터에 대해서 몇가지 주장을 할 수 없다면 좋은 모델인지 아닌지 판단할 수 없다. 모델을 판단시에는 아직 관찰하지 않는 데이터에 기초해야 한다.
아직 관찰하지 않은 데이터에 대해 주장시에는, 아직 관찰하지 않은 데이터의 불확실성에 대해 정직해야한다. 확률이론의 수학을 사용하여 모델과 관련된
모든 형태의 불확실성과 잡음을 표현하고, 확률론적 모델 프레임워크를 사용하여 미지의 양에 대한 추론을 하고, 모델을 적용하고, 예측하고, 데이터에서 학습할 수 있음이 밝혀졌다.
이 모든 것을 확률이라고 한다. 

![image](https://user-images.githubusercontent.com/77235677/156911273-a529bf4d-d798-46f7-b456-fa07371d97e1.png)

In the world of probabilistic modeling and Bayesian machine learning and so on, there are only two kinds of things. There are stuff
which observe or measure what we call data and then there's everything else which is stuff that we didn't measure. The beauty of this
is that we can use this as a unifying principle for a lot of machine learning.

![image](https://user-images.githubusercontent.com/77235677/156911525-b2e10a3a-299a-4e37-a7f8-61ddaaa68e35.png)

베이즈의 기본 규칙은 확률 이론, 합 규칙 및 곱 규칙의 더 간단한 결과이다. 몇가지 매개변수를 가진 모델을 가지고 있다면, 해당 매개변수 값이 무엇인지 모른다는 불확실성을 가진다.
예측을 해야하는 경우, 확률이론은 미지의 수량을 예측하려면, 관찰한 데이터가 주어지면 그 미지의 수량을 x라고 부른다. 그런 다음 합계 및 곱 규칙은 예측을 수행하는 하나의 방법을 제시해준다.

* why should we care?
> Calibrated model and prediction uncertainty: getting systems that know when they don't know
> 
> Automatic model complexity control and structure learning


## ✔ 참고자료
https://www.youtube.com/watch?v=-47G_ULKAHk