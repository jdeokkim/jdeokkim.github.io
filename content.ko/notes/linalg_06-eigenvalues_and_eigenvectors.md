---
title: "선형 대수: 고유값과 고유 벡터"
date: "2025-03-30T22:04:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra"]
---

### 고유벡터의 정의

정사각 행렬 \(A\)와 벡터 \(x\)의 곱 \(Ax\)에서 \(A\)는 주어진 벡터 \(x\)를 또다른 벡터 \(Ax\)로 바꿔주는 선형 함수 (linear function)의 역할을 한다. 대부분의 경우, \(Ax\)는 \(x\)와 전혀 다른 방향을 가리킨다. **하지만 일부 벡터는 \(A\)를 곱하더라도 그 방향이 변하지 않는데, 이러한 벡터를 고유벡터 (eigenvector (eye-gən-vector))라고 한다.**

고유 벡터 \(x\)에 \(A\)를 곱했을 때 방향이 변하지 않는다는 것은 스칼라 값 \(\lambda\)에 대해 \(x\)가 \(Ax = \lambda x\)를 만족한다는 것이다. 다시 말하면, \(x\)에 \(A\)를 곱했을 때 그 값이 \(x\)의 \(\lambda\)배가 되는 \(x\)와 \(\lambda\)가 존재한다는 것이다.

> \(A = I\)일 때, 모든 벡터는 \(I\)에 대한 고유 벡터이다. 즉, \(x \ne 0\)인 임의의 벡터 \(x\)에 \(I\)를 곱하면 항상 \(x\)의 \(\lambda = 1\)배가 된다.

### 고유값 구하기

> 행렬 \(A\)의 고유값 (eigenvalue (eye-gən-value)) \(\lambda\)는 \(x \ne 0\)인 임의의 벡터 \(x\)에 대해 \(Ax = \lambda x\)를 만족하는 스칼라 값이다.

예를 들어, 다음과 같은 \(2 \times 2\) 행렬 \(A\)가 있다고 하자.

$$
A = \begin{bmatrix}
-3 & 2 \\
-2 & 1
\end{bmatrix}
$$

\(Ax = \lambda x\)를 만족하는 \(\lambda\)를 찾기 위해서는 \(Ax = \lambda x\)의 해를 구하면 되는데, \((A - \lambda I)x = 0\)에서 \(x \ne 0\)이므로 \(A - \lambda I\)는 비가역 행렬이고 \(|A - \lambda I| = 0\)이다.

> 정사각 행렬 \(A\)와 \(x \ne 0\)인 임의의 벡터 \(x\)에 대해 \(|A - \lambda I| = 0\)를 만족하는 스칼라 값 \(\lambda\)는 \(A\)의 고유값이다.

$$
A - \lambda I = \begin{bmatrix}
-3 - \lambda & 2 \\
-2 & 1 - \lambda
\end{bmatrix}
$$

$$
det \ (A - \lambda I) = (-3 - \lambda)(1 - \lambda) + 4
$$

> \(det \ (A - \lambda I) = 0\)를 전개하여 얻을 수 있는 \(\lambda\)에 대한 방정식을 \(A\)의 특성 방정식 (characteristic equation)이라고 한다.

또한, **\(n \times n\) 크기의 정사각 행렬 \(A\)에 대해 \(det \ (A - \lambda I)\)는 \(n\)차 다항식으로 나타낼 수 있으므로 \(\lambda\)의 개수는 최대 \(n\)개라는 것을 알 수 있다.**

$$
= {\lambda}^2 + 2\lambda + 1
$$

$$
\therefore \lambda = -1
$$

이제 \(\lambda\)를 이용해 \(A\)에 대한 고유벡터를 구해보자.

$$
(A + I)x = 0
$$

$$
\begin{bmatrix}
-2 & 2 \\
-2 & 2
\end{bmatrix}x = 0
$$

$$
\therefore x = c\begin{bmatrix}
1 \\
1
\end{bmatrix} \ (c \ne 0)
$$

> \(A\)가 비가역 행렬이라면 \(A\)의 고유값 중 하나는 반드시 \(\lambda = 0\)이다.

**증명:** \(A\)가 가역 행렬이고 \(A\)의 고유값 중 하나가 \(\lambda = 0\)이라고 가정하자. \(x \ne 0\)인 임의의 벡터 \(x\)에 대해 \(Ax = \lambda x\)를 만족하는 \(\lambda = 0\)이므로 \(Ax = 0\)이다. \(A\)는 가역 행렬이므로 \(Ax = 0\)는 자명한 해 \(x = 0\)만을 가지는데, \(Ax = \lambda x\)에서 \(x \ne 0\)이라고 하였으므로 모순이 발생한다. 따라서 \(A\)가 비가역 행렬이라면 \(A\)는 반드시 \(\lambda = 0\)의 고유값을 가진다.

### 고유값의 성질

> \(n \times n\) 크기의 정사각 행렬 \(A\)의 고유값 \({\lambda}_1, {\lambda}_2, \cdots, {\lambda}_n\)에 대해 다음이 성립한다.
>
> 1. \(|A| = \Pi_{k = 1}^{n} \lambda_{k} = \lambda_{1}\cdots\lambda_{n}\)
> 2. \(tr(A) = \sum_{k=1}^{n}a_{kk} = \sum_{k=1}^{n}{\lambda}_{k}\)

---

### 행렬의 대각화

\(x\)가 고유벡터라면, \(Ax = \lambda x\), \(A^n x = {\lambda}^n x\), \(A^{-1}x = {\lambda}^{-1} x\)이므로 행렬 \(A\)의 \(n\)제곱을 매우 쉽게 계산할 수 있다.  

$$
A^{-1} Ax = \lambda A^{-1} x
$$

$$
A^{-1} x = \frac{1}{\lambda} A^{-1} Ax = \frac{1}{\lambda} x
$$

또한, \(A\)의 고유벡터를 이용하면 \(A\)를 "대각화된 (diagonalized)" 행렬 \(\Lambda\)로 만들 수 있다.

> \(n \times n\) 크기의 행렬 \(A\)가 \(n\)개의 선형 독립인 고유벡터 \(x_1, x_2, \cdots, x_n\)을 가질 때, \(A\)의 고유벡터를 하나의 행렬 \(X\)에 모아 고유벡터 행렬 (eigenvector matrix)을 만들었다고 하자. 
>
> 이때 \(X^{-1}AX\)를 \(A\)의 고유값 행렬 (eigenvalue matrix)이라고 하며, \(\Lambda\)로 나타낸다.

예를 들면, \(A = \begin{bmatrix}1 & 5 \\ 0 & 6\end{bmatrix}\)일 때 \(|A - \lambda I| = 0\)에서

$$
A - \lambda I = \begin{bmatrix}
1 - \lambda & 5 \\
0 & 6 - \lambda
\end{bmatrix}
$$

$$
|A - \lambda I| = (1 - \lambda)(6 - \lambda) = 0
$$

$$
\therefore \lambda = 1, 6
$$

\((A - I) x = 0\)에서 \(x_1 = \begin{bmatrix}1 \\ 0\end{bmatrix}\)이고 \((A - 6I) x = 0\)에서 \(x_2 = \begin{bmatrix}1 \\ 1\end{bmatrix}\)이므로, 고유벡터 행렬 \(X = \begin{bmatrix}1 & 1 \\ 0 & 1\end{bmatrix}\)이다. 

또한, \(X^{-1} = \frac{1}{ad - bc} \begin{bmatrix}d & -b \\ -c & a\end{bmatrix} = \begin{bmatrix}1 & -1 \\ 0 & 1\end{bmatrix}\)이므로

$$
\Lambda = X^{-1}AX =
\begin{bmatrix}1 & 0 \\ 0 & 6\end{bmatrix}
$$

\(A\)를 고유벡터 행렬 \(X\)와 고유값 행렬 \(\Lambda\)로 다시 표현하면 \(A = X\Lambda X^{-1}\)이므로, \(A^2 = X\Lambda X^{-1} X\Lambda X^{-1} = X\Lambda^2 X^{-1}\)가 된다.

따라서 아래 수식은 모두 동일한 의미를 가진다.

> 1. \(AX = X\Lambda\)
> 2. \(X^{-1}AX = \Lambda\)
> 3. \(A = X\Lambda X^{-1}\)

### 고유값과 관련된 성질

> 1. 행렬 \(A\)의 고유값 \(\lambda_1, \lambda_2, \cdots, \lambda_n\)이 모두 다른 값이라면, \(A\)는 대각화 가능한 행렬이다.

**증명:** \(A\)의 고유값 \(\lambda_1, \lambda_2, \cdots, \lambda_n\)이 모두 다르다는 것은 \(A\)의 고유벡터 \(x_1, x_2, \cdots, x_n\)가 모두 선형 독립이라는 것을 뜻하므로, 고유벡터 행렬 \(X\)는 가역 행렬이다. 따라서 \(X^{-1}\)이 존재하므로 \(A\)는 대각화 가능하다.

> 2. 고유벡터 행렬 \(X\)의 열 순서는 고유값 행렬 \(\Lambda\)의 열 순서에도 영향을 미친다. 예를 들어, \(X\)의 열 순서를 \(\begin{bmatrix}1 & 1 \\ 1 & 0\end{bmatrix}\)로 변경하면,

$$
\begin{bmatrix}
    0 & 1 \\ 
    1 & -1
\end{bmatrix}
\begin{bmatrix}
    1 & 5 \\ 
    0 & 6
\end{bmatrix}
\begin{bmatrix}
    1 & 1 \\ 
    1 & 0
\end{bmatrix}
= \begin{bmatrix}
    6 & 0 \\ 
    0 & 1
\end{bmatrix}
$$

### 닮은 행렬

> \(A = X\Lambda X^{-1}\)에서 고유값 행렬 \(\Lambda\)를 고정시키고 고유벡터 행렬 \(X\)만을 변경하여 얻을 수 있는, \(\Lambda\)가 같은 모든 행렬 \(A_1, A_2, \cdots\)을 서로 닮았다 (similar)고 한다.

이제 닮음 (similarity)이라는 개념을 조금 더 확장해보자.

> 행렬 \(A\), \(C\)와 가역 행렬 \(B\)에 대해 \(A = BCB^{-1}\)라면, \(A\)와 \(C\)를 서로 닮았다고 하며, **\(A\)와 \(C\)는 서로 같은 고유값을 가진다.**

\(B\)가 가역 행렬이기만 하면 닮음이라는 개념을 정의할 수 있으며, \(C\)가 꼭 대각 행렬일 필요는 없다.

--- 

### 대칭 행렬

> 대칭 행렬 (symmetric matrix) \(S\)는 \(S = S^T\)의 성질을 만족하는 \(n \times n\) 크기의 정사각 행렬을 뜻한다.

\(S\)와 \(S^T\)를 대각화하면 각각 \(S = X \Lambda X^{-1}\)와 \(S^T = (X^{-1})^T \Lambda X^T\)를 얻을 수 있는데, 만약 \(X\)가 직교 행렬이라면 \(X^{-1} = X^T\)이고 \(X^T X = I\)이므로, \(X\)의 고유벡터들이 모두 직교함을 알 수 있다.

고유값과 고유 벡터에 대한 대칭 행렬의 두 가지 성질에 대해 알아보자.

> 1. 대칭 행렬의 모든 고유값은 실수 (real number)이다.
> 2. 대칭 행렬의 모든 고유벡터는 정규 직교 벡터로 만들 수 있다.

\(\Lambda\)가 모든 고유값이 실수인 고유값 행렬, \(Q\)가 모든 열이 정규 직교 벡터인 고유벡터 행렬이라고 하면 다음이 성립한다.

> **스펙트럼 정리 (spectral theorem):** 모든 대칭 행렬 \(S\)는 \(S = Q\Lambda Q^T = Q\Lambda Q^{-1}\) 형태로 분해할 수 있다.

### 양의 정부호 행렬

> 대칭 행렬 \(S\)의 모든 고유값이 양수라면, \(S\)를 양의 정부호 (positive definite) 행렬이라고 한다.

\(S\)가 양의 정부호 행렬인지 알 수 있는 가장 직관적인 방법은 \(S\)에 대한 특성 방정식 \(|S - \lambda I| = 0\)를 직접 풀어서 고유값을 확인해보는 것이지만, 방정식을 푸는 과정이 번거롭다는 단점이 있다.

이제 특성 방정식을 풀지 않고도 \(2 \times 2\) 크기의 대칭 행렬 \(S = \begin{bmatrix}a & b \\ b & c\end{bmatrix}\)가 양의 정부호 행렬인지 확인할 수 있는 몇 가지 방법을 알아보자.

> 1. \(S\)의 모든 고유값이 양수일 필요충분조건은 \((a > 0) \land (ac - b^2 > 0)\)이다.

**증명:** \(S\)의 고유값 \(\lambda_1\)과 \(\lambda_2\)의 곱은 \(det \ S = ac - b^2\)와 같으므로 \(|S| > 0\)이어야 한다. 또한, \(\lambda_1 + \lambda_2 = tr(S)\)이므로 \(a + c > 0\)이어야 한다. 따라서 \(a > 0\)이다.

> 2. \(S\)의 모든 고유값이 양수일 필요충분조건은 \(S\)의 모든 피봇이 양수인 경우이다.

**증명:** \(S\)를 소거법으로 정리하면 \(S\)의 피봇은 \(a\)와 \(c - \frac{b}{a}b = \frac{ac - b^2}{a}\)가 된다. 그런데 첫 번째 방법에 의해 \(a > 0\)이고 \(ac - b^2 > 0\)이므로 \(S\)의 모든 피봇이 양수이면 \(S\)는 양의 정부호 행렬이고, 역도 성립한다.

**여기서 알 수 있는 중요한 사실은 대칭 행렬의 모든 고유값이 양수이면 모든 피봇도 양수라는 것이다.**

> 3. **에너지-기반 정의 (energy-based definition):** \(x \ne 0\)인 모든 벡터 \(x\)에 대해 \(S\)가 \(x^T Sx > 0\)을 만족하면, \(S\)는 양의 정부호 행렬이다. 여기서 \(x^T Sx\)는 에너지 (energy)라고도 한다. 

$$
x^T Sx = \begin{bmatrix}
x & y
\end{bmatrix}
\begin{bmatrix}
a & b \\
b & c
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

$$
= ax^2 + 2bxy + cy^2 > 0
$$

> 4. 대칭 행렬 \(S\)와 \(T\)가 양의 정부호 행렬이라면, \(S + T\)도 양의 정부호 행렬이다.

**증명:** \(S + T\)가 양의 정부호 행렬이라면 세 번째 방법에 의해 \(x^T (S + T) x > 0\)이어야 하는데, \(x^T (S + T) x = x^T Sx + x^T Tx\)이다. 그런데 \(x \ne 0\)일 때 \(x^T Sx > 0\)이고 \(x^T Tx > 0\)이므로 \(x^T (S + T) x > 0\)이다. 따라서 \(S + T\)는 양의 정부호 행렬이다.

> 5. 행렬 \(A\)의 모든 열이 선형 독립이라면, \(S = A^T A\)는 양의 정부호 행렬이다.

### 양의 준정부호 행렬

> 대칭 행렬 \(S\)의 모든 고유값이 \(0\)보다 크거나 같은 실수이거나, \(x \ne 0\)인 모든 벡터 \(x\)에 대해 \(S\)가 \(x^T Sx \ge 0\)인 경우 \(S\)를 양의 준정부호 (positive semidefinite) 행렬이라고 한다.

예를 들면, \(S = \begin{bmatrix}1 & 2 \\ 2 & 4\end{bmatrix}\)의 고유값은 \(\lambda_1 = 5\), \(\lambda_2 = 0\)이므로 양의 준정부호 행렬이다.

---

### 참고 문헌

- [G. Strang, "Introduction to Linear Algebra," 5th ed. Wellesley-Cambridge Press, Wellesley, MA, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
