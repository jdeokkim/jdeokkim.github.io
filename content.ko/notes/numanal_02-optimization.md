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

(추가 예정)

### 참고 문헌

- [G. B. Thomas, Jr., J. R. Hass, C. E. Heil, M. D. Weir, "Thomas' Calculus," 14th ed. Pearson Education, 2021.](#)
- [G. Strang, "Linear Algebra and Learning from Data," Wellesley-Cambridge Press, 2019.](https://math.mit.edu/~gs/learningfromdata/)