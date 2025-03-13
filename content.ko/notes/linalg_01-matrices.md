---
title: "벡터와 행렬"
date: "2024-02-16T21:56:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra", "linalg", "numpy"]
---

### 벡터의 정의

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

영 벡터의 모든 성분 (entry, element)은 \(0\)이다.

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

### Cauchy–Schwarz 부등식

\(| cos \ \theta | \le 1\)이므로, \(v \cdot w\)를 통해 코시–슈바르츠 부등식 (Cauchy–Schwarz–Buniakowsky inequality)을 유도할 수 있다.

$$
|v \cdot w| \le ||v|| \ ||w||
$$

---

## 행렬의 정의

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
    1 & 0 & 0 \\ 
    0 & 1 & 0 \\
    0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
    x_1 \\ 
    x_2 \\
    x_3
\end{bmatrix} =
Ax = b
$$

### 행렬의 성분 표기법

행렬의 각 성분을 가리킬 때는 행 번호 (row index)와 열 번호 (column index)를 이용하기도 하는데, 예를 들어 \(a_{ij}\)는 \(i\)번째 행 (\(y\) 좌표...?)과 \(j\)번째 열 (\(x\) 좌표...?)에 위치한 성분을 뜻한다.

$$
A = 
\begin{bmatrix}
    a_{11} & a_{12} & a_{13} \\
    a_{21} & a_{22} & a_{23} \\
\end{bmatrix}
$$

행의 개수가 \(m\)개이고 열의 개수가 \(n\)인 행렬을 \(m \times n\) 행렬이라고 하며, \(m \times n\)을 행렬의 크기 (size)라고 한다.

### 단위 행렬과 영 행렬

행렬의 성분 중에서 \(i = j\)인 \(a_{ij}\)를 주대각 성분 (main diagonal entry)이라고 한다.

단위 행렬 (identity matrix)은 아래와 같이 주대각 성분이 \(1\)이고 나머지 성분이 모두 \(0\)인 행렬을 가리키며,

$$
I = 
\begin{bmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1
\end{bmatrix}
$$

모든 성분이 \(0\)인 행렬은 영 행렬 (zero matrix, null matrix)이라고 한다.

$$
O = 
\begin{bmatrix}
    0 & 0 & 0 & 0 & 0 \\
    0 & 0 & 0 & 0 & 0 \\
    0 & 0 & 0 & 0 & 0 \\
    0 & 0 & 0 & 0 & 0 \\
    0 & 0 & 0 & 0 & 0
\end{bmatrix}
$$

### 행렬 연산

크기가 같은 두 행렬은 서로 더하거나 뺄 수 있다.

$$
A = \begin{bmatrix}
1 & 2 \\
0 & 1 \\
\end{bmatrix},
B = \begin{bmatrix}
2 & 3 \\
0 & 1 \\
\end{bmatrix},
A + B = \begin{bmatrix}
3 & 5 \\
0 & 2 \\
\end{bmatrix}
$$

벡터와 마찬가지로, 행렬의 모든 성분에 상수 \(c\)를 곱하는 스칼라 곱셈 연산을 수행할 수도 있다.

$$
cA = \begin{bmatrix}
c & 2c \\
0 & c \\
\end{bmatrix}
$$

### 전치 행렬

주대각선을 기준으로 행렬 \(A\)의 행과 열을 교환하여 (~~주대각선을 기준으로 종이를 접듯이 행렬을 뒤집어서~~) 만들어지는 행렬을 \(A\)의 전치 행렬 (transpose)라고 한다.

$$
A = \begin{bmatrix}
0 & 1 & 2 \\
3 & 2 & 1 \\
\end{bmatrix},
A^T = \begin{bmatrix}
0 & 3 \\
1 & 2 \\
2 & 1 \\
\end{bmatrix}
$$

행렬 \(A\)와 \(B\)의 전치 행렬에 대한 성질은 다음과 같다.

> 1. \((cA)^T = cA^T\)
> 2. \((A^T)^T = A\)
> 3. \((A + B)^T = A^T + B^T\)
> 4. \((AB)^T = B^T A^T\)

### 행렬의 대각합

행렬 \(A\)의 대각합 (trace) \(tr(A)\)은 \(A\)의 모든 주대각 성분의 합을 뜻한다.

$$
tr(A) = \sum_{k=1}^{n}{a_{kk}} = 1 + 1 = 2
$$

### 행렬 곱셈

\(m \times n\) 행렬 \(A\)와 \(n \times p\) 행렬 \(B\)의 곱 \(AB\)은 \(m \times p\) 행렬이 되는데, \(AB\)의 각 성분은 \(A\)의 각 행의 성분과 \(B\)의 각 열의 성분을 내적하여 구할 수 있다. (단, \(1 \le i \le m, \ 1 \le j \le p\))

$$
AB = [c_{ij}]_{m \times p} \ \text{where} \ c_{ij} = a_{i1} b_{1j} + a_{i2} b_{2j} + \dots + a_{ip} b_{pj} = \sum_{k=1}^{p}{a_{ik}b_{kj}}
$$

예를 들면, 행렬 \(A\)와 \(B\)가 다음과 같을 때,

$$
A = \begin{bmatrix}
1 & 2 & 3 \\
3 & 2 & 1 \\
\end{bmatrix},
B = \begin{bmatrix}
1 & -1 \\
-1 & 1 \\
1 & -1
\end{bmatrix}
$$

$$
AB_{11} = \begin{bmatrix}
1 & 2 & 3
\end{bmatrix} *
\begin{bmatrix}
1  \\
-1 \\
1  \\
\end{bmatrix} = 2
$$

$$
AB_{12} = \begin{bmatrix}
1 & 2 & 3
\end{bmatrix} *
\begin{bmatrix}
-1  \\
1 \\
-1  \\
\end{bmatrix} = -2
$$

$$
AB_{21} = \begin{bmatrix}
3 & 2 & 1
\end{bmatrix} *
\begin{bmatrix}
1  \\
-1 \\
1  \\
\end{bmatrix} = 2
$$

$$
AB_{22} = \begin{bmatrix}
3 & 2 & 1
\end{bmatrix} *
\begin{bmatrix}
-1  \\
1 \\
-1  \\
\end{bmatrix} = -2
$$

따라서 \(AB\)는 다음과 같은 \(2 \times 2\) 행렬이다.

$$
AB = \begin{bmatrix} 
2 & -2 \\
2 & -2
\end{bmatrix}
$$

행렬 곱셈에서는 행렬의 덧셈 및 뺄셈과 마찬가지로 결합 (associative law) 및 분배 법칙 (distributive law)이 성립하지만, **교환 법칙 (commutative law)은 성립하지 않는다.**

> 1. \(AB \ne BA\)
> 2. \(A(BC) = (AB)C\)
> 3. \(A(B + C) = AB + AC\)
> 4. \((A + B)C = AC + BC\)
> 5. \(A = IA = AI\)

### 블록 행렬

아래와 같은 \(2 \times 2\) 행렬 \(A\)와 \(4 \times 4\) 행렬 \(B\)가 있다고 하자. 

$$
A = \begin{bmatrix}
  1 & 2 \\
  2 & 1
\end{bmatrix},
B = \begin{bmatrix}
  1 & 2 & 1 & 2 \\
  2 & 1 & 2 & 1 \\
  1 & 2 & 1 & 2 \\
  2 & 1 & 2 & 1
\end{bmatrix}
$$

\(B\)를 \(2 \times 2\)의 행렬 단위로 나누면 \(A\)로 표현할 수 있는데, 이때 \(A\)를 블록 행렬 (block matrix)이라고 한다.

$$
B = \begin{bmatrix}
  A & A \\
  A & A
\end{bmatrix}
$$

행렬을 그 행렬보다 더 작은 행렬 단위인 블록으로 나누어 표현하는 방법은 크기가 큰 행렬을 다룰 때 유용하게 사용할 수 있다.

---

### 참고 문헌

- [G. Strang, “Introduction to Linear Algebra,” 5th ed. Wellesley-Cambridge Press, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
