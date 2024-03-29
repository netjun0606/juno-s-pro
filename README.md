 # 박준오 보고서
 
 ### 목차
* 수치 예측
   1. 선형 회귀
   1. 손실 함수, 경사 하강법

* 이진 분류
   1. 퍼셉트론
   1. 다층 퍼셉트론
   1. 다중 분류 
   1. 로지스틱 회귀
   1. Sigmoid Function
***

### 수치 예측

## 선형 회귀
   
어떤 변수에 다른 변수들이 주는 영향력을 선형적으로 분석하는 대표적인 방법
선형 회귀 분석을 위해서는 우선 `선형 회귀 모델`을 만들어야 한다.
여기서 모델은 수학 식으로 표현되는 함수를 의미하는데, 영향을 주는 변수와 영향을 받는 변수로 구성되어있다.
영향을 주는 변수는 `독립 변수` 또는 `설명 변수`등이 있고,
영향을 받는 변수는 `종속 변수` 또는 `반응 변수`등이 있다.

종속 변수가 1개 일 때의 선형 회귀 모델은 `단변량 선형 회귀 모델`이라고 하고 
2개 이상일 때는 `다변량 선형 회귀 모델`이라고 한다.

따라서 종속 변수가 1개이고 독립 변수가 2개 이상인 선형 회귀 모델은 `단변량 다중 선형 회귀 모델`이라고 하며
종속 변수와 독립 변수 모두 2개 이상일 때를 `다변량 다중 선형 회귀 모델`이라고 한다.
***
## 손실 함수, 경사 하강법

`손실 함수` : 손실 함수란 신경망이 학습할 수 있도록 해주는 지표이다. 머신러닝 모델의 출력값과
사용자가 원하는 출력값의 차이, 즉 오차를 말한다. 이 손실 함수 값이 최소화되도록 하는 가중치와 편향을
찾는 것이 바로 학습이다. 손실 함수로 `평균 제곱 오차`나 `교차 엔트로피 오차`를 사용한다.


*평균 제곱 오차*

계산이 간편하여 가장 많이 사용되는 손실 함수이다. 기본적으로 모델의 출력 값과 사용자가 원하는 출력 값
사이의 거리 차이를 오차로 사용한다. 그러나 오차를 계산할때 단순히 거리 차이를 합산하여 평균내게 되면,
거리가 음수로 나왔을 때 합산된 오차가 실제 오차보다 줄어드는 경우가 생긴다. 이러한 이유 때문에 각 거리
차이를 제곱하여 합산한 후에 평균을 낸다.

\*거리 차이를 제곱하면 좋은 점은, 거리 차이가 작은 데이터와 큰 데이터 오차의 차이가 더욱 커잔다는 점이다. 이렇게 되면 어느 부분에서 오차가 두드러지는지 확실하게 알 수 있다는 장점이 있다.\*

*교차 엔트로피 오차*

기본적으로 분류 문제에서 one-hot encoding했을 경우에만 사용할 수 있는 오차 계산법이다.
교차 엔트로피 오차는 정답일 때의 모델 값에 자연로그를 계산하는 식이 된다. 
만약 정답이 1이라고 했을 때, 정답에 근접하는 경우에는 오차가 0에 거의 수렴해간다.
그러나 0에 가까워지면, 정답에 멀어지면 멀어질수록 오차가 기하급수적으로 증가한다.

손실 함수의 목적 : 머신러닝 모델의 최종적인 목적은 높은 정확도를 끌어내는 매개변수(가중치, 편향)를 찾는 것이다. 
신경망 학습에서는 최적의 매개변수를 탐색할 때 손실함수의 값을 가능한 한 작게 하는 매개변수 값을 찾는다. 
이 때, 매개변수의 미분(기울기)을 계산하고, 그 미분 값을 토대로 매개변수 값을 갱신하는 과정을 반복한다. 

 - 주요한 점은, 정확도와는 달리 손실 함수는 매개변수의 변화에 따라 연속적으로 변화한다는 점이다. 
손실 함수와는 달리 정확도는 매개변수의 변화에 둔감하고, 또한 변화가 있다하여도 불연속적으로 변화하기 때문에 미분을 할 수 없다. 미분이 되지 않으면 최적화를 할 수 없으므로 정확도가 아닌 손실 함수를 지표로 삼아 학습을 해나가는 것이다. 


`경사 하강법` : 해당 함수의 최소값 위치를 찾기 위해 비용 함수(Cost Function)의 그레디언트 반대 방향으로 정의한 step size를 가지고 조금씩 움직여 가면서 최적의 파라미터를 찾으려는 방법이다.
여기서 그레디언트는 파라미터에 대해 편미분한 벡터를 의미하며 이 파라미터를 반복적으로 조금씩 움직이는 것이 관건이 된다.
머신 러닝에서는 가장 간단한 모델인 선형 회귀(Linear Regression) 를 예를 들고 있다.
선형 회귀에서는 이 cost를 최소화 하기 위해 아래와 같은 두줄의 코드를 작성 할 수 있다.
```python
optimizer = tf.train.GradientDescentOptimizer(learning_rate=0.01)
train = optimizer.minimize(cost)
```
### 이진 분류

## 퍼셉트론

`퍼셉트론` : 퍼셉트론은 다수의 트레이닝 데이터를 이용하여 일종의 지도 학습을 수행하는 알고리즘입니다.
트레이닝 데이터에는 데이터의 특성값에 대응되는 실제 결과값을 가지고 있어야합니다.
퍼셉트론은 단순하게 입력층,중간층,출력층으로 나타낼 수 있습니다.
여기서 중간층은 노드 또는 뉴런이라고 부르며, 입력층은 다른 노드의 출력값이 입력값으로 입력되는 것이고,
출력층은 이 노드의 출력값이 다른 노드로 전달되는 층이라고 생각하면 된다.
이와 같이 중간층이 하나의 노드로 구성되어 중간층과 출력층의 구분이 없는 구조를 단순 또는 단층 퍼셉트론이라
부르며, 중간층을 구성하는 노드가 여러 개이고, 이러한 중간층이 다수로 구성되어 있는 구조를 `다층 퍼셉트론`이라 부릅니다.

## 다층 퍼셉트론

`다층퍼셉트론` : 이미지에 무엇이 있는지 알아내기 위해서는 입력과 출력 간의 매우 복잡한 관계와 이를 위해서는 패턴이 많은 특성(feature)들 사이의 관계를 통해서 특정 지어지는 가능성을 고려해야합니다. 이런 경우에는, 선형 모델의 정확도는 낮을 것입니다. 우리는 한 개 이상의 은닉층(hidden layer)을 함께 사용해서 더 일반적인 함수들을 이용한 모델을 만들 수 있습니다. 이를 구현하는 가장 쉬운 방법은 각 층 위에 다른 층들을 쌓는 것입니다. 각 층의 결과는 그 위의 층의 입력으로 연결되는데, 이는 마지막 출력층까지 반복됩니다. 이런 아키텍쳐는 일반적으로 “다층 퍼셉트론(multilayer perceptron)”이라고 불립니다.

 ## 로지스틱 회귀
 
`로지스틱 회귀` : 먼저 로지스틱 회귀는 선형 회귀 분석과는 다르게 결과가 \*범주형\*일 때 사용한다.
로지스틱 회귀는 분류하려는 범주가 2가지 범주로 나눠진 경우에 적용된다.
로지스틱 회귀는 선형 회귀와는 다른 방법으로 모델을 구축하는데, 그 이유는 선형 회귀에서의 연속적인 숫자인 Y값은 그 값 자체로 의미를 갖지만, 범주형 변수는 의미를 갖지 않는다. 0과 1사이에 중간 범주가 없고 0과 1을 바꿔도 큰 상관이 없다.

## Sigmoid Function

`Sigmoid Function` : 미분이 되지 않는 지점에서 사용되는 것이 SIgmoid함수이다. 즉 계단형식의 함수를 미분이 가능하도록 곡선화를 해주는 함수이다.
1과 0사이를 부드럽게 이어 준다.
기울기에 따라 계단함수와 비슷해진다.
특징은 x가 어떤값이어도 바로 1혹은 0으로 값을 얻어낼수 있다는 것이다. 



