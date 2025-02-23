---
title: "연립 일차 방정식"
date: "2024-02-17T23:43:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra", "linalg", "numpy"]
---

### 행의 관점과 열의 관점

연립 일차 방정식은 행의 관점 (row picture)와 열의 관점 (column picture), 두 개의 관점으로 바라볼 수 있다.

$$
\begin{equation}
    \begin{cases}
        3x + 2y = 12 \\
        x - 2y = -4
    \end{cases}
\end{equation}
$$

주어진 연립 일차 방정식을 행의 관점으로, 각 방정식을 한 줄씩 살펴보면, 두 직선 \(3x + 2y = 12\)와 \(x - 2y = -4\)의 교점이 바로 연립 일차 방정식의 해라는 것을 알 수 있다.

이제 열의 관점으로 살펴보면, 두 벡터의 선형 결합, 다시 말하면 \((3, 1)\)의 \(x\)배에 해당하는 벡터와 \((2, -2)\)의 \(y\)배에 해당하는 벡터의 합이 \((12, -4)\)가 되는 \(x\)와 \(y\)를 통해 연립 일차 방정식의 해를 구할 수 있다.

$$
\begin{bmatrix}
    3 \\ 
    1
\end{bmatrix} x +
\begin{bmatrix}
    2 \\ 
    -2
\end{bmatrix} y =
\begin{bmatrix}
    12 \\ 
    -4
\end{bmatrix}
$$

미지수가 3개 이상인 연립 일차 방정식도 마찬가지로 행의 관점과 열의 관점으로 바라볼 수 있다.

$$
\begin{equation}
    \begin{cases}
        2x + y + z = 8 \\
        x + 2y + z = 6 \\
        x + y + 2z = 2
    \end{cases}
\end{equation}
$$

$$
\begin{bmatrix}
    2 \\ 
    1 \\
    1
\end{bmatrix} x +
\begin{bmatrix}
    1 \\ 
    2 \\
    1
\end{bmatrix} y +
\begin{bmatrix}
    1 \\ 
    1 \\
    2
\end{bmatrix} z =
\begin{bmatrix}
    8 \\ 
    6 \\
    2
\end{bmatrix}
$$

### 소거법과 대입법

연립 일차 방정식을 푸는 대표적인 방법에는 소거법 (elimination method)과 대입법 (substitution method)이 있다.

대입법은 일차 방정식을 하나 선택하고 다른 일차 방정식에 대입하여 미지수를 소거하는 방법을 뜻한다.

소거법은 가감법이라고도 하며, 주어진 연립 방정식에서 미지수를 하나씩 소거해나가며 해를 찾는다.

$$
\begin{equation}
    \begin{cases}
        3x + 2y = 12 \\
        x - 2y = -4
    \end{cases}
\end{equation}
$$

$$
\begin{equation}
\rightarrow
    \begin{cases}
        3x + 2y = 12 \\
        8y = 24
    \end{cases}
\end{equation}
$$

미지수를 소거할 때는 한 일차 방정식을 다른 일차 방정식에 더하거나 빼는 과정을 거치는데, 이 과정을 반복하다 보면 연립 일차 방정식의 미지수 계수를 행렬로 표현했을 때 아래와 같은 상삼각 행렬 (upper triangular matrix, \(U\))가 만들어지게 된다. 

$$
\begin{bmatrix}
    3 & 2 \\ 
    1 & -2
\end{bmatrix}
\rightarrow
\begin{bmatrix}
    3 & 2 \\ 
    0 & 8
\end{bmatrix} 
$$

그 다음에는 상삼각 행렬의 맨 아래에서부터 시작해서 위쪽 방향으로, 즉 \(y\)의 값을 먼저 구하고 \(y\)를 통해 \(x\)의 값을 찾는 후방 대입법 (back substition)을 통해 연립 일차 방정식의 해를 구할 수 있다.

### 계수 행렬을 이용한 소거법

연립 일차 방정식의 계수 행렬 중, 다른 미지수의 소거를 담당하는 0이 아닌 성분을 피봇 (pivot)이라고 한다.

예를 들면, 아래와 같은 형태의 계수 행렬에서 피봇은 \(a_{11}\), \(a_{22}\), \(a_{33}\), 그리고 \(a_{44}\)이다.

$$
\begin{bmatrix}
    a_{11} & a_{12} & a_{13} & a_{14} \\ 
    0      & a_{22} & a_{23} & a_{24} \\
    0      &      0 & a_{33} & a_{34} \\
    0      &      0 &      0 & a_{44}
\end{bmatrix}
$$

\(n\)개의 미지수를 가진 연립 일차 방정식의 해를 찾기 위해서는 총 \(n\)개의 피봇이 필요한데, 계수 행렬을 통해 피봇을 찾는 방법은 다음과 같다. 

1. 첫 번째 미지수의 계수를 피봇으로 간주하고, 이 성분이 속한 열의 다른 모든 성분을 0으로 만든다.
2. 두 번째 미지수의 계수를 피봇으로 간주하고, 이 성분이 속한 열의 다른 모든 성분을 0으로 만든다.
3. 이 과정을 총 \(n\)번 반복하여 \(n\)개의 피봇을 찾고, 계수 행렬이 상삼각 행렬 형태가 되도록 한다.
4. 후방 대입법을 통해 각 미지수의 값을 찾고, 연립 일차 방정식의 해를 구한다.

$$
\begin{bmatrix}
    ? & ? & ? & ? \\ 
    ? & ? & ? & ? \\
    ? & ? & ? & ? \\
    ? & ? & ? & ?
\end{bmatrix}
\rightarrow
\begin{bmatrix}
    ? & ? & ? & ? \\ 
    0 & ? & ? & ? \\
    0 & 0 & ? & ? \\
    0 & 0 & 0 & ?
\end{bmatrix}
$$

즉, 소거법은 \(Ax = b\) 형태의 연립 일차 방정식을 \(Ux = c\)의 상삼각 형태로 변환하는 과정이다. 

### 역행렬

정사각 행렬 (square matrix) \(A\)의 곱셈의 역원 (multiplicative **inverse**, reciprocal)이 되는, 즉 \(AB = BA = I\)를 만족하는 단 하나의 행렬 \(B\)가 존재할 때 \(A\)를 가역행렬 (invertible matrix, non-singular matrix)이라고 한다. 또한, \(B\)를 \(A\)의 역행렬 (inverse matrix)라 하며 \(A^{-1}\)과 같이 나타낸다.

\(A\)의 역행렬이 존재하지 않을 경우, \(A\)를 비가역행렬 (non-invertible matrix, singular matrix)라고 한다.

\(n \times n\) 행렬 \(A\)의 역행렬이 존재하기 위한 필요충분조건은 다음과 같다. (단, \(n > 0\))

1. \(A\)의 피봇 개수가 \(n\)개이다.
2. \(Ax = 0\)의 해는 \(x = 0\) 단 하나이다.
3. \(Ax = b\)의 해는 \(x = A^{-1}b\) 단 하나이다.

(추가 예정)

### 역행렬의 성질

> 1. \(A A{-1} = A^{-1} A = I\)
> 2. \((A^{-1})^{-1} = A\)
> 3. \((AB)^{-1} = B^{-1}A^{-1}\)
> 4. \((A^{T})^{-1} = (A^{-1})^T\)

### 기본 행렬

단위 행렬 (identity matrix) \(I\)에 아래 연산 중 단 하나만을 수행하여 만들어지는 행렬을 기본 행렬 (elementary matrix)이라 하며, 기본 행렬을 만들기 위해 수행한 연산을 기본 행 연산 (elementary row operation)이라고 한다.

> 1. \(i\)번째 행에 \(j\)번째 행의 \(k\)배만큼을 더한다.

$$
E_{23}(k) = \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 1 & k \\
    0 & 0 & 1 \\
\end{bmatrix}
$$

$$
E_{23}(k) \begin{bmatrix}
    1 \\
    2 \\
    3
\end{bmatrix} =
\begin{bmatrix}
    1 \\
    2 + 3k \\
    3
\end{bmatrix}
$$

> 2. \(i\)번째 행을 \(k\)배로 만든다.

$$
E_{3}(k) = \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & k \\
\end{bmatrix}
$$

$$
E_{3}(k) \begin{bmatrix}
    1 \\
    2 \\
    3
\end{bmatrix} =
\begin{bmatrix}
    1 \\
    2 \\
    3k
\end{bmatrix}
$$

> 3. \(i\)번째 행과 \(j\)번째 행을 서로 교환한다.

$$
E_{23} = \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 0 & 1 \\
    0 & 1 & 0 \\
\end{bmatrix}
$$

$$
E_{23} \begin{bmatrix}
    1 \\
    2 \\
    3
\end{bmatrix} =
\begin{bmatrix}
    1 \\
    3 \\
    2
\end{bmatrix}
$$

### 첨가 행렬

연립 일차 방정식 \(Ax = b\)에서 행렬 \(A\)의 오른쪽에 새로운 열 \(b\)를 추가하여 만들어지는 행렬을 첨가 행렬 (augmented matrix)라고 한다.

$$
A = \begin{bmatrix}
    2 & 1 & 1 \\
    1 & 2 & 1 \\
    1 & 1 & 2 \\
\end{bmatrix}, 
b = \begin{bmatrix}
    8 \\
    6 \\
    2 \\
\end{bmatrix}
$$

$$
[A \ b] = \begin{bmatrix}
    2 & 1 & 1 & | & 8 \\
    1 & 2 & 1 & | & 6 \\
    1 & 1 & 2 & | & 2 \\
\end{bmatrix}
$$

### Gauss–Jordan 소거법

연립 일차 방정식 \(Ax = b\)의 해 \(x = A^{-1}b\)를 구하기 위해서는 \(A^{-1}\)이 필요하다. 

Gauss–Jordan 소거법 (Gauss–Jordan elimination)의 핵심은 첨가 행렬 \([A \ I]\)에 기본 행 연산을 적용하여 \([I \ A^{-1}]\) 형태로 만드는 것이다.

예를 들면, \(A\)와 \(b\)가 아래와 같을 때,

$$
A = \begin{bmatrix}
    1 & 1 & 1 \\
    1 & 2 & 2 \\
    1 & 2 & 3 \\
\end{bmatrix},
b = \begin{bmatrix}
    3 \\
    5 \\
    6 \\
\end{bmatrix}
$$

먼저 \([A \ I]\)에 기본 행 연산을 수행하여 (\(A\)에 수행한 연산을 \(I\) 에도 똑같이 수행!) \(A\)를 상삼각 행렬 \(U\) 형태로 만든다. 여기까지의 과정을 Gauss 소거법 (Gaussian elimination)이라고 한다.

$$
[A \ I] = \begin{bmatrix}
    1 & 1 & 1 & | & 1 & 0 & 0 \\
    1 & 2 & 2 & | & 0 & 1 & 0 \\
    1 & 2 & 3 & | & 0 & 0 & 1 \\
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    1 & 1 & 1 & | & 1 & 0 & 0 \\
    0 & 1 & 1 & | & -1 & 1 & 0 \\
    1 & 2 & 3 & | & 0 & 0 & 1 \\
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    1 & 1 & 1 & | & 1 & 0 & 0 \\
    0 & 1 & 1 & | & -1 & 1 & 0 \\
    0 & 1 & 2 & | & -1 & 0 & 1 \\
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    1 & 1 & 1 & | & 1 & 0 & 0 \\
    0 & 1 & 1 & | & -1 & 1 & 0 \\
    0 & 0 & 1 & | & 0 & -1 & 1 \\
\end{bmatrix}
$$

Gauss–Jordan 소거법에서는 \(U\)를 기약 행사다리꼴 (reduced row echelon form, RREF) 형태를 거쳐 \(I\)로 만드는 과정을 추가적으로 수행한다.

$$
\rightarrow \begin{bmatrix}
    1 & 0 & 0 & | & 2 & -1 & 0 \\
    0 & 1 & 1 & | & -1 & 1 & 0 \\
    0 & 0 & 1 & | & 0 & -1 & 1 \\
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    1 & 0 & 0 & | & 2 & -1 & 0 \\
    0 & 1 & 0 & | & -1 & 2 & -1 \\
    0 & 0 & 1 & | & 0 & -1 & 1 \\
\end{bmatrix} = [I \ A^{-1}]
$$

따라서 \(Ax = b\)의 해 \(x = A^{-1}b\)는

$$
A^{-1}b = \begin{bmatrix}
    2 & -1 & 0 \\
    -1 & 2 & -1 \\
    0 & -1 & 1 \\
\end{bmatrix}
\begin{bmatrix}
    3 \\
    5 \\
    6 \\
\end{bmatrix}
= \begin{bmatrix}
    1 \\
    1 \\
    1 \\
\end{bmatrix}
$$

즉, \(x = y = z = 1\)이다.

### \(LU\) 분해 (\(A = LU\))

\(LU\) 분해 (\(LU\) decomposition)이란 가역 행렬 \(A\)를 상삼각 행렬과 하삼각 행렬 (lower triangular matrix)의 곱 \(LU\)로 분해하는 과정을 뜻하며, Gauss 소거법을 첨가 행렬 없이 행렬의 곱으로만 나타낸 것이다.

\(A\)를 \(LU\) 분해하기 위해서는 \(A = IA\)에서부터 시작해 \(A\)에 기본 행 연산을 수행할 때마다 그 연산에 대응하는 기본 행렬의 역행렬을 \(I\)에 곱해주는 과정을 \(A = LU\) 형태가 될 때까지 반복하면 된다.

$$
A = IA = 
\begin{bmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
    1 & 1 & 1 \\
    1 & 2 & 2 \\
    1 & 2 & 3 \\
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    1 & 0 & 0 \\
    1 & 1 & 0 \\
    0 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
    1 & 1 & 1 \\
    0 & 1 & 1 \\
    1 & 2 & 3 \\
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    1 & 0 & 0 \\
    1 & 1 & 0 \\
    1 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
    1 & 1 & 1 \\
    0 & 1 & 1 \\
    0 & 1 & 2 \\
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    1 & 0 & 0 \\
    1 & 1 & 0 \\
    1 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
    1 & 1 & 1 \\
    0 & 1 & 1 \\
    0 & 1 & 2 \\
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    1 & 0 & 0 \\
    1 & 1 & 0 \\
    1 & 1 & 1 \\
\end{bmatrix}
\begin{bmatrix}
    1 & 1 & 1 \\
    0 & 1 & 1 \\
    0 & 0 & 1 \\
\end{bmatrix} = LU
$$

\(LU\) 분해는 \(Ax = b\)의 해를 수치 해석 (numerical analysis)적으로 계산할 때 자주 사용되며, 그 과정은 다음과 같다.

> 1. **분해 (factor):** \(A\)를 \(A = LU\)로 분해하면 \(Ax = LUx = b\)가 되는데, 이때 \(Ux = c\)라고 하자.
> 2. **계산 (solve):** \(Lc = b\)를 먼저 계산하고, 그 다음에 \(Ux = c\)를 계산하여 \(x\)를 찾는다.

### \(A = LDU\)

\(U\)의 주대각 성분, 즉 피봇 중에 \(1\)이 아닌 것이 존재할 경우에는 \(U\)를 대각 행렬 \(D\)와 또다른 상삼각 행렬 \(U\)의 곱인 \(DU\)로 나타낼 수 있다.

$$
U = IU = \begin{bmatrix}
    1 & 0 \\
    0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
    2 & 8 \\
    0 & 5 \\
\end{bmatrix}
$$

$$
= \begin{bmatrix}
    2 & 0 \\
    0 & 5 \\
\end{bmatrix}
\begin{bmatrix}
    1 & 4 \\
    0 & 1 \\
\end{bmatrix} = DU
$$

---

## 참고 문헌

- [G. Strang, “Introduction to Linear Algebra,” 5th ed. Wellesley-Cambridge Press, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
