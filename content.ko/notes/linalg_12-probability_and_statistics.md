---
title: "선형 대수: 확률과 통계"
date: "2025-04-14T22:23:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra", "probability", "statistics"]
---

### 표본 공간

동전 또는 주사위를 던지거나 카드 게임에서 카드를 한 장 뽑는 것처럼, 나올 수 있는 결과가 정해져 있고 무한히 반복할 수 있는 과정을 실험 (experiment)이라고 한다.

표본 공간 (sample space)은 실험을 통해 나올 수 있는 모든 결과를 나타내는 집합을 뜻한다. 동전을 한 번 던지는 실험에서 동전이 옆면으로 서게 되는 경우가 없다고 가정하면, 이 실험에서 나올 수 있는 결과는 '앞면'과 '뒷면' 뿐이다. '앞면'이 나오는 경우와 '뒷면'이 나오는 경우를 각각 \(H\)와 \(T\)라고 하면, 표본 공간 \(\Omega = \{ H, T \}\)이다. 또한, 동전을 한 번 던져서 앞면이 나온 경우 (\(\{H\}\))처럼 표본 공간의 부분 집합을 나타내는 상황을 사건 (event)이라고 한다.

### 확률 함수

어떤 사건이 일어날 가능성이 얼마나 큰지를 나타내기 위해, 각각의 사건이 그 사건이 일어날 확률에 대응하는 확률 함수 (probability function)을 정의한다.

> 표본 공간 \(\Omega\)의 사건 \(A\)에 대해 \(P(A) \in [0, 1]\)인 확률 함수 \(P\)는 다음 조건을 만족한다.
>
> 1. \(P(\Omega) = 1\)
> 2. \(A_1, A_2, \cdots\)가 동시에 발생할 수 없는 사건 (disjoint event)일 때, \(P(A_1 \cup A_2 \cup \cdots) = P(A_1) + P(A_2) + \cdots\)

### 조건부 확률

주사위를 한 번 던져 어떤 눈이 나오는지 확인하는 실험에서, 주사위를 한 번 던졌는데 홀수의 눈이 나오는 사건을 \(A\), 주사위를 한 번 던졌는데 \(3\)의 배수의 눈이 나오는 사건을 \(B\)라고 하자. 두 사건에 대한 확률 \(P(A) = \frac{3}{6} = \frac{1}{2}\)이고 \(P(B) = \frac{2}{6} = \frac{1}{3}\)임을 쉽게 알 수 있다. 그런데 만약 "주사위를 한 번 던져서 홀수의 눈이 나왔을 때, 이 눈이 \(3\)의 배수일 확률"이 무엇인지 알고 싶다면 어떻게 해야 할까?

> **조건부 확률 (conditional probability):** 사건 \(A\)가 발생했을 때 \(A\)와 관련된 또다른 사건 \(B\)가 발생할 확률을 \(A\)에 대한 \(B\)의 조건부 확률 \(P(B | A)\)이라고 하며, 다음과 같이 정의한다.

$$
P(B | A) = \frac{P(A \cap B)}{P(A)}, \ P(A) > 0
$$

주사위를 한 번 던졌는데 이 눈이 홀수이면서 \(3\)의 배수일 확률 \(P(A \cap B) = \frac{1}{6}\)이므로, \(P(B | A) = \frac{1}{3}\)이다.

### 확률에 대한 관점

확률 (probability)이라는 개념은 사건의 빈도를 측정하기 위해 정립되었는데, 확률은 빈도주의적 관점 (frequentist probability)과 베이지안 (베이즈) 관점 (Bayesian probability)이라는 두 가지 관점으로 바라볼 수 있다.

빈도주의적 관점에서는 동전이나 주사위를 던지거나 카드 게임에서 카드를 한 장 뽑는 것과 같이, 어떤 실험을 무한히 반복하면 특정 사건이 일어날 확률이 \(p\)라는 값에 수렴할 것이라는 전제를 바탕으로 다음 실험의 결과를 예측한다.

베이지안 관점에서는 "환자가 병에 걸렸을 확률이 \(40\%\)"라고 말하는 의사와 같이 무한히 반복할 수 없는 실험에 대한 확률을 "믿음의 정도 (a degree of belief)"로 보고, 실험의 결과에 따라 확률을 계속해서 갱신한다.

---

### 확률 변수

확률 변수 (random variable)은 무작위한 사건에 따라 값이 달라지는 변수를 뜻한다. 스칼라 형태의 확률 변수 \(x\)에 대해 \(x\)가 가질 수 있는 값은 \(x_1\)와 같이 나타내고, 벡터 형태의 확률 변수 \(\mathbf{x}\)에 대해 \(\mathbf{x}\)가 가질 수 있는 값은 \(x\)와 같이 나타낸다.

이산 확률 변수 (discrete random variable)은 확률 변수가 가질 수 있는 값의 개수가 유한한 확률 변수를 뜻하며, 연속 확률 변수 (continuous random variable)은 확률 변수가 가질 수 있는 값의 개수가 무한하여 그 값을 실수 형태로 나타낼 수 있는 확률 변수를 뜻한다.

### 확률 분포

> 확률 분포 (probability distribution)는 하나 또는 여러 개의 확률 변수가 어떤 값을 가질 확률을 나타내는 함수를 뜻한다.

확률 질량 함수 (probability mass function, PMF) \(P(\text{x})\)는 이산 확률 변수 \(\text{x}\)에 대한 확률 분포를 뜻하며, \(\text{x}\)의 값이 \(x\)가 될 확률을 \(P(\text{x} = x)\)와 같이 나타낸다. 예를 들면, 주사위를 한 번 던질 때 나올 수 있는 값 \(\text{x} \in \{1, 2, 3, 4, 5, 6\}\)에 대한 확률 질량 함수 \(P(\text{x} = x) = \frac{1}{6}\)이다.

> 이산 확률 변수 \(\text{x}\)의 확률 질량 함수 \(P\)는 아래 조건을 모두 만족한다.
>
> 1. \(P\)의 정의역은 \(\text{x}\)가 가질 수 있는 모든 값이다.
> 2. \(\forall x \in \text{x}\)에 대해, \(0 \le P(x) \le 1\)이다.
> 3. \(\sum_{x \in \text{x}} P(x) = 1\)

확률 밀도 함수 (probability density function) \(p(x)\)는 연속 확률 변수 \(\text{x}\)에 대한 확률 분포를 뜻하며, \(\text{x}\)의 값이 \([a, b]\)에 위치할 확률을 \(p(a \le \text{x} \le b)\)와 같이 나타낸다.

확률 밀도 함수는 \(\text{x}\)의 값이 특정 구간에 속할 확률을 제공하지만, 확률 질량 함수와 달리 \(\text{x}\)가 특정한 값이 될 확률은 제공하지 않음에 유의해야 한다.

> 연속 확률 변수 \(\text{x}\)의 확률 밀도 함수 \(p\)는 아래 조건을 모두 만족한다.
>
> 1. \(P\)의 정의역은 \(\text{x}\)가 가질 수 있는 모든 값이다.
> 2. \(\forall x \in \text{x}\)에 대해, \(p(x) \ge 0\)이다.
> 3. \(\int p(x) dx = 1\)

### 기댓값과 분산

> 확률 변수 \(\text{x}\)의 기댓값 (expected value)은 \(\text{x}\)가 가질 수 있는 값의 평균을 뜻하며, 이산 확률 변수의 기댓값과 연속 확률 변수의 기댓값은 각각 \(\mathbb{E}_{\mathbf{x} \sim P}[\text{x}]\)와 \(\mathbb{E}_{\mathbf{x} \sim p}[\text{x}]\)로 나타낸다.

기댓값의 정의를 조금 더 확장하면, \(\mathbb{E}[f(x)]\)는 확률 분포의 모든 값 \(x\)을 정의역으로 하는 함수 \(f(x)\)의 함숫값들의 평균을 뜻한다.

$$
\mathbb{E}_{\mathbf{x} \sim P}[\text{x}] = \sum_{x} x \cdot P(x)
$$

$$
\mathbb{E}_{\mathbf{x} \sim P}[f(x)] = \sum_{x} f(x) \cdot P(x)
$$

> 확률 분포의 모든 값 \(x\)을 정의역으로 하는 함수 \(f(x)\)에 대해, \(\mathbb{E}[(f(x) - \mathbb{E}[f(x)])^2]\)를 확률 변수 \(\text{x}\)의 분산 (covariance)이라고 한다.

$$
\mu = \mathbb{E}[f(x)], \ \sigma^2 = \mathbb{E}[(f(x) - \mu)^2]
$$

분산은 \(f(x)\)가 기댓값 \(\mathbb{E}[f(x)]\)과 얼마나 차이가 나는지를 거리의 제곱 (squared distance) 형태로 표현한 것으로, 이때 \(\sigma\)를 표준 편차 (standard deviation)라고 한다.

### 결합 확률과 공분산

이제 하나의 실험 대신 여러 개의 실험을 동시에 수행한다고 가정하자. 예를 들면, 주사위 \(2\)개를 동시에 던지고 각각의 결과를 확인해보는 두 개의 실험을 생각해볼 수 있다. \(n\)개의 실험을 수행하면 기댓값도 \(n\)개가 되며, \(n\)개 성분을 가진 벡터로 나타낼 수 있다.

**\(n\)개의 실험에 대한 공분산 (covariance)이란 각 실험의 확률 변수가 서로 어떠한 선형 관계가 있는지를 나타내는 값으로, 다음과 같이 정의된다.**

> 확률 분포 \(P_1(\text{x})\)의 모든 값 \(x\)을 정의역으로 하는 함수 \(f(x)\)와 확률 분포 \(P_2(\text{y})\)의 모든 값 \(y\)을 정의역으로 하는 함수 \(g(y)\)에 대해, \(\mathbb{E}[(f(x) - \mathbb{E}[f(x)])(g(y) - \mathbb{E}[g(y)])]\)를 확률 변수 \(\text{x}\)와 \(\text{y}\)의 공분산이라고 한다.

$$
\sigma_{\text{x} \text{y}} = \mathbb{E}[(f(x) - \mu_{\text{x}})(g(y) - \mu_{\text{y}})]
$$

> 아래와 같은 \(2 \times 2\)의 대칭 행렬 \(V\)를 확률 변수 \(\text{x}\)와 \(\text{y}\)의 공분산 행렬 (covariance matrix)이라고 한다.

$$
V = \begin{bmatrix}
    (\sigma_1)^2 & \sigma_1 \sigma_2 \\
    \sigma_1 \sigma_2 & (\sigma_2)^2
\end{bmatrix}
$$

---

### 참고 문헌

- [G. Strang, "Introduction to Linear Algebra," 5th ed. Wellesley-Cambridge Press, Wellesley, MA, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
- [I. Goodfellow, Y. Bengio, A. Courville, "Deep Learning," MIT Press, 2016.](https://www.deeplearningbook.org/)