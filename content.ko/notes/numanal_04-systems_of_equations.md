---
title: "수치 해석: 연립 방정식의 해"
date: "2025-05-06T20:55:00+09:00"
hideReply: true
math: true
tags: ["numerical-analysis"]
---

### 가우스 소거법

선형 대수에서 \(A\mathbf{x} = b\) 형태의 연립 일차 방정식 (systems of linear equations, linear systems)의 해 \(\mathbf{x} = A^{-1}b\)를 구하는 가장 기초적인 방법은 가우스 소거법 (Gaussian elimination)을 이용하는 것이다.

가우스 소거법은 첨가 행렬 (augmented matrix) \(\begin{bmatrix} A \ | \ b \end{bmatrix}\)에 아래와 같은 기본 행 연산 (elementary row operation)을 한 번 이상 적용하여 \(\begin{bmatrix} U \ | \ c \end{bmatrix}\) 형태로 만들고 \(U\mathbf{x} = c\)의 해를 구하는 방법이다.

> 1. \(i\)번째 행에 \(j\)번째 행의 \(k\)배만큼을 더한다.
> 2. \(i\)번째 행을 \(k\)배로 만든다.
> 3. \(i\)번째 행과 \(j\)번째 행을 서로 교환한다.

예를 들어, 다음과 같은 연립 일차 방정식이 있다고 하자.

$$
\begin{equation}
    \begin{cases}
        4x + 2y - z = 5 \\
        x + 4y + z = 12 \\
        2x - y + 4z = 12 \\
    \end{cases}
\end{equation}
$$

주어진 연립 방정식을 계수 행렬과 벡터를 이용해 \(A\mathbf{x} = b\) 형태로 표현하면

$$
\begin{bmatrix}
    4 & 2 & -1 \\ 
    1 & 4 & 1 \\
    2 & -1 & 4
\end{bmatrix}
\begin{bmatrix}
    x \\ 
    y \\
    z
\end{bmatrix}
= \begin{bmatrix}
    5 \\ 
    12 \\
    12
\end{bmatrix}
$$

$$
\therefore \begin{bmatrix} A \ | \ b \end{bmatrix} =
\begin{bmatrix}
    4 & 2 & -1 & | & 5 \\ 
    1 & 4 & 1 & | & 12 \\
    2 & -1 & 4 & | & 12
\end{bmatrix}
$$

이제 첨가 행렬 \(\begin{bmatrix} A \ | \ b \end{bmatrix}\)에 기본 행 연산을 적용하여 \(A\)를 상삼각 행렬 \(U\)로 만들어보자.

> 1. \(A\)의 첫 번째 열에서 피봇 (주대각) 성분 아래의 모든 성분을 \(0\)으로 만들기 위해, 두 번째 행에서 첫 번째 행의 \(\frac{1}{4}\)배를 뺀 다음, 세 번째 행에서 첫 번째 행의 \(\frac{1}{2}\)배를 뺀다.

$$
\begin{bmatrix}
    4 & 2 & -1 & | & 5 \\ 
    1 & 4 & 1 & | & 12 \\
    2 & -1 & 4 & | & 12
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    4 & 2 & -1 & | & 5 \\ 
    0 & \frac{7}{2} & \frac{5}{4} & | & \frac{43}{4} \\
    2 & -1 & 4 & | & 12
\end{bmatrix}
$$

$$
\rightarrow \begin{bmatrix}
    4 & 2 & -1 & | & 5 \\ 
    0 & \frac{7}{2} & \frac{5}{4} & | & \frac{43}{4} \\
    0 & -2 & \frac{9}{2} & | & \frac{19}{2}
\end{bmatrix}
$$

> 2. 같은 방법으로 \(A\)의 두 번째 열에서 피봇 (주대각) 성분 아래의 모든 성분을 \(0\)으로 만든다.

$$
\rightarrow \begin{bmatrix}
    4 & 2 & -1 & | & 5 \\ 
    0 & \frac{7}{2} & \frac{5}{4} & | & \frac{43}{4} \\
    0 & 0 & \frac{73}{14} & | & \frac{219}{14}
\end{bmatrix}
$$

> 3. \(A\)를 상삼각 행렬 \(U\)로 만들었으므로, 세 번째 행부터 시작해 \(\mathbf{x}\)를 구한다.

$$
\frac{73}{14}z = \frac{219}{14} \ \therefore z = 3
$$

$$
\frac{7}{2}y + \frac{5}{4}z = \frac{43}{4} \ \therefore y = 2
$$

$$
4x + 2y - z = 5 \ \therefore x = 1
$$

---

> \(\textbf{Algorithm 1: }\)  
> \(\text{Naive Gaussian Elimination}\)
>
> \(\textbf{Require: } A \ (n \times n \text{ Matrix})\)  
> \(\textbf{Require: } b \ (n \times 1 \text{ Matrix})\)  
> 
> \(\textbf{for} \ c \in \{1, \cdots, n - 1\} \ \textbf{do}\)  
> \(\ \ \textbf{for} \ r \in \{c + 1, \cdots, n\} \ \textbf{do}\)  
> \(\ \ \ \ m \leftarrow \frac{A_{rc}}{A_{cc}}\)  
> 
> \(\ \ \ \ \textbf{for} \ k \in \{c, \cdots, n\} \ \textbf{do}\)  
> \(\ \ \ \ \ \ A_{rk} \leftarrow A_{rk} - m \cdot A_{ck}\)  
> \(\ \ \ \ \textbf{end for}\)  
>
> \(\ \ \ \ b_{r1} \leftarrow A_{r1} - m \cdot A_{c1}\)  
> \(\ \ \textbf{end for}\)  
> \(\textbf{end for}\)  

```python
# `A`의 `c`-번째 열
for c in range(len(A[0]) - 1):
    # `A`의 `c`-번째 피봇 행을 제외한 나머지 `r`-번째 행
    for r in range(c + 1, len(A)): 
        # 피봇 행에 곱할 값 `m`을 계산한다.
        m: float = A[r][c] / A[c][c]

        # NOTE: `range(c, ...)`를 `range(c + 1, ...)`로 변경하면
        # 피봇 성분 아래의 나머지 성분을 `0`으로 만드는 불필요한
        # 계산을 생략할 수 있다.
        for k in range(c, len(A[0])):
            # `A`의 `r`-번째 행에서 `c`-번째 피봇 행의 `m`배를 뺀다.
            A[r][k] -= m * A[c][k]

        # `b`에도 같은 연산을 적용한다.
        b[r][0] -= m * b[c][0]
```

```
[
    [4, 2, -1], 
    [0.0, 3.5, 1.25], 
    [0.0, 0.0, 5.214285714285714]
]
```

---

> \(\textbf{Algorithm 2: }\)  
> \(\text{Backward Substitution}\)
>
>
> \(\textbf{Require: } A \ (n \times n \text{ Matrix})\)  
> \(\textbf{Require: } b \ (n \times 1 \text{ Matrix})\)  
> 
> \(\mathbf{x}_{n1} \leftarrow \frac{b_{n1}}{A_{nn}}\)
>
> \(\textbf{for} \ r \in \{n - 1, \cdots, 1\} \ \textbf{do}\)  
> \(\ \ sum \leftarrow 0\)  
>
> \(\ \ \textbf{for} \ c \in \{r + 1, \cdots, n\} \ \textbf{do}\)  
> \(\ \ \ \ sum \leftarrow sum + A_{rc} \cdot \mathbf{x}_{c1}\)  
> \(\ \ \textbf{end for}\)  
>  
> \(\ \ \mathbf{x}_{r1} \leftarrow \frac{(b_{r1})}{A_{rr}}\)  
> \(\textbf{end for}\)  

```python
n: int = len(A)

# 마지막 행에 해당하는 미지수의 값을 계산
x[n - 1][0] = b[n - 1][0] / A[n - 1][n - 1]

# `U`의 `r`-번째 행 (마지막 행을 제외하고 역순으로 순회)
for r in range(n - 2, -1, -1):
    # `r`-번째 행의 피봇 성분을 제외한 나머지 성분의 합
    sum: float = 0

    # 미지수를 하나씩 대입해서 나머지 성분의 합 계산
    for c in range(r + 1, n):
        sum += A[r][c] * x[c][0]

    # 나머지 성분의 합을 우변으로 옮기고,
    # `r`-번째 행에 대응하는 미지수의 값을 계산
    x[r][0] = (b[r][0] - sum) / A[r][r]

```

```
[
    [1.0], 
    [2.0], 
    [3.0]
]
```

---

### 부분 피봇팅

(추가 예정)

### \(LU\) 분해

(추가 예정)

---

### 띠 행렬

행렬 중에서도 대부분의 성분이 \(0\)인 특별한 형태의 행렬을 희소 행렬 (sparse matrix)이라고 하는데, **희소 행렬 중에서도 \(0\)이 아닌 성분이 주대각 성분에 밀집한 것을 띠 행렬 (band matrix)라고 한다.**

> \(m \times n\) 크기의 띠 행렬 \(B_w\)는 \(i \in [1, m]\), \(j \in [1, n]\)와 스칼라 상수 \(w\)에 대해 \(|i - j| > w\)를 만족하는 \(B_w\)의 성분 \(b_{ij}\)가 \(0\)인 희소 행렬로, 이때 \(w\)를 \(B_w\)의 반-대역폭 (half-bandwidth)이라고 한다.

$$
B_{w = 1} = \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1 \\
\end{bmatrix}
$$

$$
B_{w = 2} = \begin{bmatrix}
    1 & 2 & 0 & 0 & 0 \\
    2 & 1 & 2 & 0 & 0 \\
    0 & 2 & 1 & 2 & 0 \\
    0 & 0 & 2 & 1 & 2 \\
    0 & 0 & 0 & 2 & 1 \\
\end{bmatrix}
$$

띠 행렬은 각 열의 피봇 성분 아래에 위치한 \(0\)이 아닌 성분의 개수가 항상 \(w - 1\)개임이 보장되므로, 띠 행렬에 가우스 소거법을 적용할 때의 연산 횟수는 밀집 행렬에 가우스 소거법을 적용할 때의 연산 횟수보다 매우 적어진다.

> 밀집 행렬에 가우스 소거법을 적용했을 때의 연산 횟수는 다음과 같으며, 시간 복잡도는 \(O(n^3)\)이다.

$$
\frac{n(n + 1)(2n + 1)}{6} - \frac{n(n + 1)}{2}
$$

$$
= \frac{n^3 - n}{3}
$$

> 띠 행렬에 가우스 소거법을 적용했을 때의 연산 횟수는 다음과 같으며, 시간 복잡도는 \(O(w^2 n)\)이다.

$$
\frac{w(w - 1)(3n - 2w + 1)}{3}
$$

### 노름의 정의

\(\mathbb{R}^n\)의 벡터 \(\mathbf{x}\)의 크기 (size) \(||\mathbf{x}||\)는 \(\mathbf{x}\)의 길이 (length) \(\sqrt{\mathbf{x} \cdot \mathbf{x}} = \sqrt{{x_1}^2 + {x_2}^2 + \dots}\)로 정의할 수 있는데, 그렇다면 행렬의 크기도 정의할 수 있을까?

> **벡터의 노름 (norm):** 벡터 공간 \(\mathbb{R}^n\)의 원소 \(\mathbf{x}\)의 노름 \(||\mathbf{x}||\)은 아래 조건을 모두 만족하는 \([0, \infty]\) 사이의 값이다.
>
> 1. \(\mathbf{x} \ne 0\)인 모든 \(\mathbf{x}\)에 대해, \(||\mathbf{x}|| > 0\)
> 2. \(||\mathbf{x} + \mathbf{y}|| \le ||\mathbf{x}|| + ||\mathbf{y}||\)
> 3. 스칼라 상수 \(c\)에 대해, \(||c\mathbf{x}|| = |c| \ ||\mathbf{x}||\)

벡터의 크기는 다음과 같이 다양한 형태의 노름으로 정의할 수 있다.

> 벡터 \(\mathbf{x} = (x_1, \cdots, x_n)\)의 \(L^1\) 노름 \(\| \mathbf{x} \|_1 = \sum_{i=1}^{n} |x_i|\)이다.

> 벡터 \(\mathbf{x} = (x_1, \cdots, x_n)\)의 \(L^2\) 노름 \(\| \mathbf{x} \|_2 = \sqrt{(\sum_{i=1}^{n} (x_i)^2)}\)이다.

> 벡터 \(\mathbf{x} = (x_1, \cdots, x_n)\)의 \(L^\infty\) 노름 \(\| \mathbf{x} \|_\infty = \max(|x_1|, \cdots, |x_n|)\)이다.

### 행렬의 노름

노름의 개념을 일반화하여, 행렬의 노름도 정의해보자. 

> 행렬 \(A\), \(B\)에 대해, \(A\)의 노름 \(||A||\)와 \(B\)의 노름 \(||B||\)는 아래 조건을 모두 만족한다.
>
> 1. \(||A|| \ge 0\)
> 2. \(||A + B|| \le ||A|| + ||B||\)
> 3. 스칼라 상수 \(c\)에 대해, \(||cA|| = |c| \ ||A||\)
> 4. 벡터 \(\mathbf{x}\)에 대해, \(||A\mathbf{x}|| \le ||A|| \ ||\mathbf{x}||\)
> 5. \(||AB|| \le ||A|| + ||B||\)

행렬의 노름에 대한 조건을 살펴보면 기존 벡터의 노름에 대한 조건에서 네 번째 조건과 다섯 번째 조건이 새로 추가된 것을 알 수 있는데, 이를 통해 \(||A||\)가 \(\mathbf{x}\)와 \(B\)의 크기를 조절하는 역할을 한다는 것을 알 수 있다.

> 행렬 \(A\)의 노름 \(||A||\)는 \(\frac{||A\mathbf{x}||}{||\mathbf{x}||}\)의 최댓값이다.

$$
||A|| = \max_{\mathbf{x} \ne 0} \frac{||A\mathbf{x}||}{||\mathbf{x}||}
$$

### 조건수 

(추가 예정)

---

### 양의 정부호 행렬

(추가 예정)

### 숄레스키 분해

(추가 예정)

---

### 직접법과 반복법

가우스 소거법, \(LU\) 분해와 크래머 법칙 (Cramer's Rule) 등은 연립 방정식 \(A\mathbf{x} = b\)의 계수 행렬 \(A\)에 기본 행 연산을 적용하거나 \(A\)의 행렬식을 이용해 연립 방정식의 정확한 해 \(\mathbf{x} = A^{-1}b\)를 구하는데, 이러한 방법을 직접법 (direct method)이라고 한다.

그런데 계수 행렬이 크기가 매우 큰 희소 행렬일 경우에는 각 성분에 접근하고 행 교환과 피봇팅 등의 연산을 수행하는 과정에서 메모리 공간에 불연속적으로 접근하는 경우가 많기 때문에 CPU에서 캐시 미스 (cache miss)가 발생하게 되고, 연립 방정식의 해를 빠르게 구하기가 어려워지게 된다.

반복법 (iterative method)은 계수 행렬 \(A\)를 \(A = S - T\)와 같이 \(S\)가 더 간단한 형태가 되도록 두 행렬로 나누고, \(A\mathbf{x} = b\)를 \(S\mathbf{x}_{k + 1} = T\mathbf{x}_k + b\)로 나타낸 다음, 정확한 해 \(\mathbf{x}\)를 구하는 대신 해의 근삿값 \(\mathbf{x}_k\)을 구하는 방법이다.

### 반복법의 수렴 조건

(추가 예정)

---

### 야코비 방법

반복법을 이용해 \(A\mathbf{x} = b\)의 해의 근삿값을 구하는 과정을 간단히 살펴보자.

> 1. \(\mathbf{x}_0\)을 임의의 벡터 (\(\mathbf{0}\)?)로 초기화한다.

$$
A = \begin{bmatrix}
    4 & 2 & -1 \\ 
    1 & 4 & 1 \\
    2 & -1 & 4
\end{bmatrix}, \
b = \begin{bmatrix}
    5 \\ 
    12 \\
    12
\end{bmatrix}
$$

$$
A\mathbf{x}_0 = A
\begin{bmatrix}
    0 \\ 
    0 \\
    0
\end{bmatrix} = b
$$

> 2. \(A\)를 \(S - T\) 형태로 나눈다. 이때 \(S\)는 전처리 행렬 (preconditioner)이라고 하며, \(A\)보다 더 간단한 형태의 행렬이어야 한다.

$$
A = S - T
$$

$$
= \begin{bmatrix}
    4 & 0 & 0 \\ 
    0 & 4 & 0 \\
    0 & 0 & 4
\end{bmatrix} - 
\begin{bmatrix}
    0 & -2 & 1 \\ 
    -1 & 0 & -1 \\
    -2 & 1 & 0
\end{bmatrix}
$$

> 3. \(S\mathbf{x}_{1} = T\mathbf{x}_{0} + b\)을 풀어 \(\mathbf{x}_{1}\)을 얻는다.

$$
\begin{bmatrix}
    4x_1 & 0 & 0 \\ 
    0 & 4y_1 & 0 \\
    0 & 0 & 4z_1
\end{bmatrix} =
\begin{bmatrix}
    5 \\ 
    12 \\
    12
\end{bmatrix}
$$

$$
\therefore \mathbf{x}_{1} = \begin{bmatrix}
    \frac{5}{4} \\ 
    3 \\
    3
\end{bmatrix}
$$

> 4. \(S\mathbf{x}_{2} = T\mathbf{x}_{1} + b\)을 풀어 \(\mathbf{x}_{2}\)를 얻는다.

$$
\begin{bmatrix}
    4x_2 & 0 & 0 \\ 
    0 & 4y_2 & 0 \\
    0 & 0 & 4z_2
\end{bmatrix} =
\begin{bmatrix}
    2 \\ 
    \frac{31}{4} \\
    \frac{25}{2}
\end{bmatrix}
$$

$$
\therefore \mathbf{x}_{2} = \begin{bmatrix}
    \frac{1}{2} \\ 
    \frac{31}{16} \\
    \frac{25}{8}
\end{bmatrix}
$$

> 5. \(\mathbf{x}_{k + 1} - \mathbf{x}_{k}\) 또는 \(b - A\mathbf{x}_{k}\)가 \(0\)에 충분히 가까워질 때까지 반복한다.

$$
k \rightarrow \infty \Rightarrow \mathbf{x}_{k} = \mathbf{x}
$$

위 과정과 같이, \(A\)의 주대각 성분으로 만든 대각 행렬 \(D\)를 \(A\)의 전처리 행렬 \(S\)로 사용하는 방법을 야코비 방법 (Jacobi's method)이라고 한다.

### 가우스–자이델 방법

가우스–자이델 방법 (Gauss–Seidel method)에서는 \(A\)의 주대각선을 포함한 하삼각행렬 \(L\)을 \(A\)의 전처리 행렬 \(S\)로 사용한다.

$$
A = S - T
$$

$$
= \begin{bmatrix}
    4 & 0 & 0 \\ 
    1 & 4 & 0 \\
    2 & -1 & 4
\end{bmatrix} - 
\begin{bmatrix}
    0 & -2 & 1 \\ 
    0 & 0 & -1 \\
    0 & 0 & 0
\end{bmatrix}
$$

(추가 예정)

---

### 공액 경사법

(추가 예정)

---

### 참고 문헌

- [G. Strang, "Introduction to Linear Algebra," 5th ed. Wellesley-Cambridge Press, Wellesley, MA, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
- [J. F. Epperson, "An Introduction to Numerical Methods and Analysis," 2nd ed. John Wiley & Sons, Inc., 2013.](https://www.jfepperson.org/2edition-web/)