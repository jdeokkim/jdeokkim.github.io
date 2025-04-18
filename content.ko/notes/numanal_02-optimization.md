---
title: "수치 해석: 최적화 이론"
date: "2025-04-17T11:05:00+09:00"
hideReply: true
math: true
tags: ["machine-learning", "multivariable-calculus", "numanal", "numerical-analysis", "optimization", "unconstrained-optimization"]
---

수학에서 최적화 (optimization)이란 함수 \(f(x_1, x_2, \cdots, x_n)\)의 최댓값 또는 최솟값을 찾는 과정을 뜻한다. 기계 학습 (machine learning)에서는 극값을 찾고자 하는 함수 \(f\)를 주로 목적 함수 (objective function, criterion)이라고 하며, 극솟값만을 찾는 경우 \(f\)를 손실 함수 (loss function, cost function)이라고 하기도 한다. 

### \(argmax\)와 \(argmin\)

> \(argmax \ f(x)\)와 \(argmin \ f(x)\)는 각각 \(f(x)\)를 최댓값 또는 최솟값으로 만드는 \(x\)를 가리킨다.

예를 들면, \(f(x) = (x - 1)^2\)는 \(x = 1\)일 때 최솟값 \(f(1)\)을 가지므로, \(argmax \ f(x) = 1\)이다.

### 다변수 미적분학

[테일러 정리 (Taylor's theorem)]({{< ref "numanal_00-taylor_series.md" >}})에 의하면, \(f\), \(f'\)와 \(f''\)가 모두 연속이고 미분 가능하면 \(f(\alpha)\)를 다음과 같이 \(2\)계 테일러 다항식 (Taylor polynomial of order \(2\))으로 근사하여 나타낼 수 있다.

$$
f(\alpha) \approx f(\alpha_0) + \frac{f'(\alpha_0)}{1!} (\alpha - \alpha_0) + \frac{f''(\alpha_0)}{2!} (\alpha - \alpha_0)^2
$$

\(\alpha - \alpha_0 = \Delta x\)라고 하면, \(\alpha = \alpha_0 + \Delta x\)인데, 이 식을 \(2\)계 테일러 다항식에 대입하면

$$
f(\alpha_0 + \Delta x) \approx f(\alpha_0) + \frac{f'(\alpha_0)}{1!} \Delta x + \frac{f''(\alpha_0)}{2!} (\Delta x)^2
$$

**마지막으로, \(\alpha_0\)에 \(x\)를 대입하면 \(f(x + \Delta x)\)에 대한 \(2\)계 테일러 다항식을 얻는다.**

$$
f(x + \Delta x) \approx f(x) + \frac{f'(x)}{1!} \Delta x + \frac{f''(x)}{2!} (\Delta x)^2
$$

\(n\)-변수 함수 \(f(x) = f(x_1, \cdots, f_n)\)에 대한 테일러 다항식도 같은 방법으로 유도할 수 있는데, 여기서 \(\nabla f\)는 \(f\)의 기울기 벡터 (gradient)를 열 벡터 형태 (\(\begin{bmatrix} \frac{\partial f}{\partial x_1} & \cdots & \frac{\partial f}{\partial x_n}\end{bmatrix}^T\))로 나타낸 것이고, \(H_f\)는 \(f\)의 헤시안 행렬 (Hessian matrix)이다.

$$
f(x + \Delta x) \approx f(x) + (\Delta x)^T \nabla f + \frac{1}{2!} (\Delta x)^T H_f (\Delta x)
$$

마지막으로, \(m\)개의 다변수 함수로 정의되는 벡터 함수 \(f = (f_1, \cdots, f_m)\)과 \(n\)개의 변수 \(x_1, \cdots, x_n\)에 대한 \(f\)의 근사식은 다음과 같다.

$$
f(x + \Delta x) \approx f(x) + J(x) \Delta x
$$

**여기서 \(J(x)\)는 함수 \(f_1, \cdots, f_m\)에 대한 기울기 벡터 \(\nabla f_1, \cdots, \nabla f_n\)를 모두 포함하는 행렬로, 야코비 행렬 (Jacobian matrix)라고 한다.**

$$
J(x) = \begin{bmatrix}
(\nabla f_1)^T \\
\vdots \\
(\nabla f_m)^T
\end{bmatrix}
$$

---

### 볼록 함수

\(f(x) = f(x_1, \cdots, x_n)\)의 최적화 문제를 풀기 위해서는 볼록 함수 (convex function)라는 개념을 알아야 한다.

> 벡터 공간 \(K\)의 두 원소 \(x\), \(y\)와 \(0 \ge \lambda \ge 1\)가 \(\lambda x + (1 - \lambda) y \in K\)를 만족하면, \(K\)를 볼록 집합 (convex set)이라고 한다.

볼록 집합의 정의를 통해 알 수 있는 것은 두 점 \(x\)와 \(y\)가 볼록 집합의 원소라면 \(x\)와 \(y\)를 잇는 모든 선분에 속하는 원소도 볼록 집합에 포함된다는 것이다.

> 함수 \(f\)의 두 점 \(x\), \(y\)와 \(0 \ge \lambda \ge 1\)에 대해, 아래 조건을 만족하는 \(f\)를 볼록 함수라고 한다.

$$
f(\lambda x + (1 - \lambda) y) \le \lambda f(x) + (1 - \lambda) f(y)
$$

> 또한, 아래 조건을 만족하는 \(f\)를 엄격한 볼록 함수 (strictly convex function)이라고 한다.

$$
f(\lambda x + (1 - \lambda) y) < \lambda f(x) + (1 - \lambda) f(y)
$$

\(f\)가 볼록 함수가 되려면, \(f\) 위의 두 점 \(x\)와 \(y\)를 잇는 할선 (secant)이 항상 \(f\)의 그래프 위에 있어야 한다는 것이다. 따라서 \(y = x^2\)는 볼록 함수이지만 \(y = -x^2\)는 볼록 함수가 아니다.

> 엄격한 볼록 함수 \(f\)의 정의역 \(x\)가 볼록 집합 \(K\)의 원소일 때, \(f\)는 단 하나의 최솟값을 가진다.

### \(L^p\) 노름

벡터, 행렬이나 함수의 크기를 측정하는 방법을 노름 (norm)이라고 한다. 벡터의 노름은 주로 길이 (length) \(|v| = \sqrt{v \cdot v} = \sqrt{{v_1}^2 + {v_2}^2 + \dots}\)를 통해 정의되는데, 벡터의 길이 외에도 벡터의 크기를 나타낼 수 있는 다른 방법이 존재한다.

> 벡터 \(x\)의 \(L^1\) 노름 \(\| \mathbf{x} \|_1 = \sum_{i=1}^{n} |x_i|\)이다.

> 벡터 \(x\)의 \(L^2\) 노름 \(\| \mathbf{x} \|_2 = \sqrt{(\sum_{i=1}^{n} (x_i)^2)}\)이다.

> 벡터 \(x\)의 \(L^\infty\) 노름 \(\| \mathbf{x} \|_\infty = max(|x_1|, |x_2|)\)이다.

### 뉴턴–랩슨 방법

뉴턴–랩슨 방법 (Newton–Raphson method)은 방정식 \(f(x) = 0\)의 해를 구하거나 볼록 함수 \(f(x)\)의 최솟값을 찾기 위해 사용할 수 있는 대표적인 방법 중 하나로, \(f(x)\)가 \(x^* = argmin \ f(x)\)에서 최솟값을 가지면 \(\nabla f(x) = \mathbf{0}\)임을 이용한다.

먼저, \(f(x)\)에서 한 점 \(x_k\)을 임의로 선택한 다음, \(x_{k + 1}\)을 \(x_k\)보다 \(x^*\)에 더 가까운 점이라고 하자. \(x_{k + 1}\)이 \(argmin \ f(x)\)에 가까워진다는 것은 \(x_{k + 1}\)에서의 기울기 벡터 \(\nabla f(x_{k + 1})\)이 \(\mathbf{0}\)에 가까워진다는 것을 뜻한다.

이제 \(\nabla f(x_{k + 1})\)를 선형 근사식 (linear approximation)으로 나타내면 \(\nabla f(x_{k + 1}) \approx \nabla f(x_k) + H_f(x_k) (x_{k + 1} - x_k)\)가 되는데, 

(추가 예정)

### 참고 문헌

- [G. B. Thomas, Jr., J. R. Hass, C. E. Heil, M. D. Weir, "Thomas' Calculus," 14th ed. Pearson Education, 2021.](#)
- [G. Strang, "Linear Algebra and Learning from Data," Wellesley-Cambridge Press, 2019.](https://math.mit.edu/~gs/learningfromdata/)