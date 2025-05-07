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
> \(\text{Naive Gaussian Elimination for } A\mathbf{x} = b\)
>
> \(\textbf{Require: } A \ (M \times N \text{ Matrix})\)  
> \(\textbf{Require: } b \ (M \times 1 \text{ Matrix})\)  
> 
> \(\textbf{for} \ c \in \{1, 2, \cdots, M - 1\} \ \textbf{do}\)  
> \(\ \ \ \ \textbf{for} \ r \in \{c + 1, \cdots, N\} \ \textbf{do}\)  
> \(\ \ \ \ \ \ \ \ m \leftarrow \frac{A_{rc}}{A_{cc}}\)  
> 
> \(\ \ \ \ \ \ \ \ \textbf{for} \ k \in \{c, \cdots, M\} \ \textbf{do}\)  
> \(\ \ \ \ \ \ \ \ \ \ \ \ A_{rk} \leftarrow A_{rk} - m \cdot A_{ck}\)  
> \(\ \ \ \ \ \ \ \ \textbf{end for}\)  
>
> \(\ \ \ \ \ \ \ \ b_{r1} \leftarrow A_{r1} - m \cdot A_{c1}\)  
> \(\ \ \ \ \textbf{end for}\)  
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
> \(\text{Backward Substitution for } A\mathbf{x} = b\)
>
>
> \(\textbf{Require: } A \ (M \times N \text{ Matrix})\)  
> \(\textbf{Require: } b \ (M \times 1 \text{ Matrix})\)  
> 
> \(\mathbf{x}_{M1} \leftarrow \frac{b_{M1}}{A_{MM}}\)
>
> \(\textbf{for} \ r \in \{M - 1, M - 2, \cdots, 1\} \ \textbf{do}\)  
> \(\ \ \ \ sum \leftarrow 0\)  
>
> \(\ \ \ \ \textbf{for} \ c \in \{r + 1, \cdots, N\} \ \textbf{do}\)  
> \(\ \ \ \ \ \ \ \ sum \leftarrow sum + A_{rc} \cdot \mathbf{x}_{c1}\)  
> \(\ \ \ \ \textbf{end for}\)  
>  
> \(\ \ \ \ \mathbf{x}_{r1} \leftarrow \frac{(b_{r1})}{A_{rr}}\)

```python
M: int = len(A)
N: int = len(A[0])

# 마지막 행에 해당하는 미지수의 값을 계산
x[M - 1][0] = b[M - 1][0] / A[M - 1][M - 1]

# `U`의 `r`-번째 행 (마지막 행을 제외하고 역순으로 순회)
for r in range(M - 2, -1, -1):
    # `r`-번째 행의 피봇 성분을 제외한 나머지 성분의 합
    sum: float = 0

    # 미지수를 하나씩 대입해서 나머지 성분의 합 계산
    for c in range(r + 1, N):
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

---

### 띠 행렬

(추가 예정)

### 노름과 조건수

(추가 예정)

### \(LU\) 분해

(추가 예정)

---

### 양의 정부호 행렬

(추가 예정)

### 숄레스키 분해

(추가 예정)

---

### 반복법과 전처리 행렬

(추가 예정)

### 가우스–자이델 방법

(추가 예정)

### 공액 경사법

(추가 예정)

---

### 참고 문헌

- [G. Strang, "Introduction to Linear Algebra," 5th ed. Wellesley-Cambridge Press, Wellesley, MA, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
- [J. F. Epperson, "An Introduction to Numerical Methods and Analysis," 2nd ed. John Wiley & Sons, Inc., 2013.](https://www.jfepperson.org/2edition-web/)