---
title: "벡터 공간"
date: "2024-02-23T23:54:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra", "linalg", "numpy"]
---

### 벡터 공간의 정의

집합 \(V\) (단, \(V \ne \emptyset\))의 두 원소 \(x\)와 \(y\)에 대해 \(x + y\)와 \(cx\)가 정의되고 \(x\)와 \(y\)가 아래 8가지 법칙을 만족할 때, \(V\)를 벡터 공간 (vector space)이라고 한다.

> 1. \(x + y = y + x\)
> 2. \((x + y) + z = x + (y + z)\)
> 3. \(x + (-x) = (-x) + x = 0\)을 만족하는 원소 \(\mathbf{0}\)이 벡터 공간에 단 하나만 존재한다.
> 4. \(x + (-x) = 0\)을 만족하는 원소 \(-x\)가 벡터 공간에 단 하나만 존재한다.
> 5. \(1x = x\)
> 6. \((c_1c_2)x = c_1(c_2x)\)
> 7. \(c(x + y) = cx + cy\)
> 8. \((c_1 + c_2)x = c_1x + c_2x\)

벡터 공간의 종류에는 \(n\)개의 성분을 가진 모든 열 벡터 (column vector)의 집합을 나타내는 \(R^n\), 행렬의 집합을 나타내는 \(M\), 실수 함수 (real function)의 집합을 나타내는 \(F\), 그리고 집합의 원소가 영 벡터 (zero vector) 단 하나인 \(Z\) 등이 있다.

예를 들면, \(\begin{bmatrix}1.25 \\ 5\end{bmatrix}\)는 \(R^2\)의 원소이고, \(\mathbf{0}\)은 \(Z\)의 원소이다.

### 부분 공간

\(R^n\)이 \(n\)차원의 공간이라고 생각해보자. 그러면 \(R^3\)은 \(3\)차원의 공간이 되는데, 이제 \(R^3\)에서 영 벡터 \((0, 0, 0)\)를 지나는 무수히 많은 직선 또는 평면 중에 하나를 생각해보자. 이 직선 또는 평면은 \(R^3\)의 모든 원소를 포함하지는 않지만 \(R^n\)의 공간 중 일부가 된다.

이처럼 벡터 공간 \(V\)의 부분 집합 \(W\) (단, \(W \ne \emptyset\))가 \(V\)와 마찬가지로 영 벡터를 포함하고, \(W\)의 두 원소 \(x\)와 \(y\)에 대해 \(x + y\)와 \(cx\)가 정의되어 있을 때, \(W\)를 \(V\)의 부분 공간 (subspace)라고 한다.

### 열 공간

연립 일차 방정식 \(Ax = b\)를 [열의 관점으로 다시 보면]({{< ref "linalg_02-linear_equations.md" >}}) \(Ax\)는 \(A\)의 각 열에 대한 선형 결합을 뜻하므로, \(Ax = b\)의 해를 구한다는 것은 \(b\)를 \(Ax\) 형태의 선형 결합으로 나타내는 것이다.

이때, \(A\)의 각 열에 대한 모든 선형 결합 \(Ax\)가 속한 부분 공간을 열 공간 (column space) \(C(A)\)라고 한다. 

예를 들어, \(\begin{bmatrix}0 & 1 \\ 3 & 4 \\ 3 & 2\end{bmatrix}\)의 열 공간은 \(\begin{bmatrix}0 \\ 3 \\ 3\end{bmatrix}\)과 \(\begin{bmatrix}1 \\ 4 \\ 2\end{bmatrix}\)의 모든 선형 결합이 포함된 평면으로 나타낼 수 있다.

![열 공간의 기하학적 표현](/images/notes/linalg_03-vector_spaces/column_space.png)

### 부분 공간의 "생성"

벡터 공간 \(V\)에서 부분 집합 \(S = \{x_1, x_2, \cdots, x_k\}\)를 임의로 선택하면, \(x_1, x_2, x_3, \cdots, x_k\)로 만들어지는 모든 선형 결합의 집합 \(SS = \{c_1x_1 + c_2x_2 + \cdots + c_kx_k \ | \ c_1, c_2, \cdots, c_k \in R\}\)는 부분 공간이 되는데, 이처럼 \(S\)의 선형 결합을 통해 부분 공간 \(SS\)를 만드는 것을 "생성" (span)이라고 한다.

---

## 참고 문헌

- [G. Strang, “Introduction to Linear Algebra,” 5th ed. Wellesley-Cambridge Press, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
