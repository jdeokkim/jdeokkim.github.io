---
title: "벡터와 행렬"
date: "2024-02-16T21:56:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra", "linalg", "numpy"]
---

## 벡터

벡터는 영 벡터 (zero vector), 두 벡터 사이의 덧셈, 그리고 벡터에 대한 스칼라 곱셈 (scalar multiplication) 연산이 정의된, 벡터 공간 (vector space)의 원소를 뜻하며, \( n \)개의 수로 이루어진 \( n \)차원의 벡터는 아래와 같이 하나의 열 (column)로 나타낼 수 있다.

$$
\mathbfit{v} = 
(v_1, v_2) =
\begin{bmatrix}
    v_1 \\ 
    v_2
\end{bmatrix},
\mathbfit{w} = 
(w_1, w_2) =
\begin{bmatrix}
    w_1 \\ 
    w_2
\end{bmatrix}
$$

### 영 벡터

영 벡터의 모든 원소은 \(0\)이다.

$$
\mathbfit{0} = 
(0, \dots) =
\begin{bmatrix}
    0 \\ 
    \vdots
\end{bmatrix}
$$

### 벡터의 기본 연산

벡터의 기본 연산에는 두 벡터 사이의 덧셈과 벡터에 대한 스칼라 곱셈이 있다.

$$
\mathbfit{v + w} = 
\begin{bmatrix}
    v_1 + w_1 \\ 
    v_2 + w_2
\end{bmatrix},
\mathbfit{cv} = 
\begin{bmatrix}
    c \cdot v_1 \\ 
    c \cdot v_2
\end{bmatrix}
$$

### 선형 결합

모든 벡터는 \(cv + dw\) 형태의 선형 결합 (linear combination)으로 나타낼 수 있으며, 특히 3차원 공간에서는 \(cu + dv + ew\) 형태의 선형 결합이 원점 (origin)을 지나는 선, 면 또는 공간이 된다. 

### 벡터의 내적

두 벡터 \(v\)와 \(w\)의 내적 (dot product, inner product) \(v \cdot w\)는 아래와 같이 정의된다.

$$
v \cdot w = w \cdot v = v_1 w_1 + v_2 w_2
$$

또한, 벡터 \(v\)의 길이 (length) \(||v||\)는 \(v \cdot v\)의 제곱근 (square root)으로 정의된다.

$$
||v|| = \sqrt{v \cdot v} = \sqrt{{v_1}^2 + {v_2}^2 + \dots}
$$

이때, 길이가 \(1\)인 벡터를 단위 벡터 (unit vector)라고 한다.

### 두 벡터 사이의 각도

중심이 원점이고 반지름이 1인 원 (unit circle) 위에 단위 벡터 \(u_1 = (cos \ \alpha, sin \ \alpha)\)와 \(u_2 = (cos \ \beta, sin \ \beta)\)가 존재하고, \(u_1\)와 \(u_2\) 사이의 각도를 \(\theta\)라고 할 때,

$$
u_1 \cdot u_2 = cos \ \alpha \ cos \ \beta + sin \ \alpha \ sin \ \beta = cos (\beta - \alpha)
$$

이므로, 영 벡터가 아닌 임의의 두 벡터 \(v\)와 \(w\)에 대해

$$
\frac{v \cdot w}{||v|| \ ||w||} = cos \ \theta
$$

가 성립한다.

### 코시–슈바르츠 부등식

\(| cos \ \theta | \le 1\)이므로, \(v \cdot w\)를 통해 코시–슈바르츠 부등식 (Cauchy–Schwarz–Buniakowsky inequality)을 유도할 수 있다.

$$
|v \cdot w| \le ||v|| \ ||w||
$$

## 행렬

3차원 공간에 단위 벡터 \(u = (1, 0, 0)\), \(v = (0, 1, 0)\), \(w = (0, 0, 1)\)가 존재한다고 가정하자. 그러면 모든 벡터는 \(u\), \(v\)와 \(w\)의 선형 결합으로 나타낼 수 있다.

$$
x_1 
\begin{bmatrix}
    1 \\ 
    0 \\
    0
\end{bmatrix} + 
x_2
\begin{bmatrix}
    0 \\ 
    1 \\
    0
\end{bmatrix} +
x_3
\begin{bmatrix}
    0 \\ 
    0 \\
    1
\end{bmatrix}
$$

이러한 선형 결합을 행렬 (matrix)로 나타내면 다음과 같다.

$$
\begin{bmatrix}
    1 \ 0 \ 0 \\ 
    0 \ 1 \ 0 \\
    0 \ 0 \ 1
\end{bmatrix}
\begin{bmatrix}
    x_1 \\ 
    x_2 \\
    x_3
\end{bmatrix} =
Ax = b
$$

---

## 참고 문헌

- [G. Strang, “Introduction to Linear Algebra,” 5th ed. Wellesley-Cambridge Press, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
