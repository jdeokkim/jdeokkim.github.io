---
title: "선형 대수: 확률과 통계"
date: "2025-04-14T22:23:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra", "linalg", "probability", "statistics"]
---

### 확률에 대한 관점

확률 (probability)이라는 개념은 사건의 빈도를 측정하기 위해 정립되었는데, 확률은 빈도주의적 관점 (frequentist probability)과 베이지안 (베이즈) 관점 (Bayesian probability)이라는 두 가지 관점으로 바라볼 수 있다.

빈도주의적 관점에서는 동전이나 주사위를 던지거나 카드 게임에서 카드를 한 장 뽑는 것과 같이, 어떤 실험을 무한히 반복하면 특정 사건이 일어날 확률이 \(p\)라는 값에 수렴할 것이라는 전제를 바탕으로 다음 실험의 결과를 예측한다.

베이지안 관점에서는 "환자가 병에 걸렸을 확률이 \(40\%\)"라고 말하는 의사와 같이 무한히 반복할 수 없는 실험에 대한 확률을 "믿음의 정도 (a degree of belief)"로 보고, 실험의 결과에 따라 확률을 계속해서 갱신한다.

### 확률 변수

확률 변수 (random variable)은 무작위한 사건에 따라 값이 달라지는 변수를 뜻한다. 스칼라 형태의 확률 변수 \(x\)에 대해 \(x\)가 가질 수 있는 값은 \(x_1\)와 같이 나타내고, 벡터 형태의 확률 변수 \(\mathbf{x}\)에 대해 \(\mathbf{x}\)가 가질 수 있는 값은 \(x\)와 같이 나타낸다.

이산 확률 변수 (discrete random variable)은 확률 변수가 가질 수 있는 값의 개수가 유한한 확률 변수를 뜻하며, 연속 확률 변수 (continuous random variable)은 확률 변수가 가질 수 있는 값의 개수가 무한하여, 값을 실수 형태로 나타낼 수 있는 확률 변수를 뜻한다.

### 확률 분포

> 확률 분포 (probability distribution)는 하나 또는 여러 개의 확률 변수가 어떤 값을 가질 확률을 나타내는 함수를 뜻한다.

확률 질량 함수 (probability mass function, PMF) \(P(\text{x})\)는 이산 확률 변수 \(\text{x}\)에 대한 확률 분포를 뜻하며, \(\text{x}\)의 값이 \(x\)가 될 확률은 \(P(\text{x} = x)\)와 같이 나타낸다. 예를 들면, 주사위를 한 번 던질 때 나올 수 있는 값 \(\text{x} \in \{1, 2, 3, 4, 5, 6\}\)에 대한 확률 질량 함수 \(P(\text{x} = x) = \frac{1}{6}\)이다.

> 이산 확률 변수 \(\text{x}\)의 확률 질량 함수 \(P\)는 아래 조건을 모두 만족한다.
>
> 1. \(P\)의 정의역은 \(\text{x}\)가 가질 수 있는 모든 값이다.
> 2. \(\forall x \in \text{x}\)에 대해, \(0 \le P(x) \le 1\)이다.
> 3. \(\sum_{x \in \text{x}} P(x) = 1\)

확률 밀도 함수 (probability density function) \(p(x)\)는 연속 확률 변수 \(\text{x}\)에 대한 확률 분포를 뜻하며, 확률 질량 함수와는 달리 어떤 값을 가질 확률을 직접적으로 제공하지는 않는다. 그 대신, \(p(x) dx\)는 \(\text{x}\)의 값이 \(x\)와 \(x + dx\) 사이에 위치할 확률을 제공한다.

> 연속 확률 변수 \(\text{x}\)의 확률 밀도 함수 \(p\)는 아래 조건을 모두 만족한다.
>
> 1. \(P\)의 정의역은 \(\text{x}\)가 가질 수 있는 모든 값이다.
> 2. \(\forall x \in \text{x}\)에 대해, \(p(x) \ge 0\)이다.
> 3. \(\int p(x) dx = 1\)

---

### 참고 문헌

- [G. Strang, "Introduction to Linear Algebra," 5th ed. Wellesley-Cambridge Press, Wellesley, MA, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
- [I. Goodfellow, Y. Bengio, A. Courville, "Deep Learning," MIT Press, 2016.](https://www.deeplearningbook.org/)