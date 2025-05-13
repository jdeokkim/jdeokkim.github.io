---
title: "선형 대수: 행렬식"
date: "2025-03-28T21:04:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra"]
---

### 행렬식의 정의

> 정사각 행렬 \(A\)의 행렬식 (determinant)은 역행렬 \(A^{-1}\)의 존재 여부를 알려주는 하나의 값으로, \(det \ A\) 또는 \(|A|\)로 나타낸다.

**\(A\)가 비가역 행렬이라면 \(A\)의 행렬식은 \(0\)이다.** \(A\)가 가역 행렬인 경우, \(A^{-1}\)의 행렬식 \(det \ A^{-1} = \frac{1}{det \ A}\)가 된다. 또한, 크래머 공식 (Cramer's Rule)을 이용하면 \(2 \times 2\)나 \(3 \times 3\) 크기의 정사각 행렬에 대한 역행렬을 쉽게 구할 수 있다.

### 행렬식의 특성

행렬식의 주요 특성을 이용해 \(det \ A = |A|\)를 계산하는 방법에 대해 알아보자.

> 1. \(det \ I = 1\)

$$
|I| =
\begin{vmatrix}
1 & 0 \\
0 & 1 \\
\end{vmatrix} =
\begin{vmatrix}
1 & 0 & 0 \\ 
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{vmatrix} = 1
$$

> 2. \(A\)의 행을 \(n\)번 교환하여 행렬 \(PA\)를 만들었을 때, \(|PA| = (-1)^n \cdot |A|\)

$$
\begin{vmatrix}
c & d \\
a & b \\
\end{vmatrix} = -
\begin{vmatrix}
a & b \\
c & d \\
\end{vmatrix}
$$

> 3. **\(A\)의 행 중 하나에 수행한 연산은 \(A\)의 행렬식에도 똑같이 적용된다.** 

예를 들어, \(A\)의 첫 번째 행을 \(t\)배로 만들면, 행렬식도 \(t\)배가 된다.

$$
\begin{vmatrix}
ta & tb \\
c & d \\
\end{vmatrix} =
t\begin{vmatrix}
a & b \\
c & d \\
\end{vmatrix}
$$

또한, \(A\)에 두 번째 행에 \({\begin{bmatrix}1 \\ 2\end{bmatrix}}^T\)를 더하면, 행렬식은 다음과 같다.

$$
\begin{vmatrix}
a & b \\
c + 1 & d + 2 \\
\end{vmatrix} =
\begin{vmatrix}
a & b \\
c & d \\
\end{vmatrix} +
\begin{vmatrix}
a & b \\
1 & 2 \\
\end{vmatrix}
$$

---

> 4. \(A\)의 두 행의 성분이 모두 같으면, \(|A| = 0\)이다.

$$
A = \begin{bmatrix}
a & b \\
a & b \\
\end{bmatrix}
$$

**증명:** \(A\)의 첫 번째 행과 두 번째 행을 교환해 만들어지는 행렬 \(PA\)의 행렬식 \(|PA| = -|A|\)이다. 그런데 \(A = PA\)이므로 \(det \ A = det \ PA = -det \ A\)이다. 따라서 \(|A| = -|A|\)이므로 \(det \ A = 0\)이다.

> 5. \(A\)의 한 행의 \(k\)배를 다른 행에서 빼서 만들어진 행렬 \(A'\)의 행렬식 \(|A'| = |A|\)이다.

$$
A = \begin{bmatrix}
a & b \\
c & d \\
\end{bmatrix},
A' = \begin{bmatrix}
a & b \\
c - ka & d - kb \\
\end{bmatrix}
$$

**증명:** 행렬식의 세 번째 특성과 네 번째 특성에 따라, \(det \ A' = det \ A\)가 된다.

$$
\begin{vmatrix}
a & b \\
c - ka & d - kb \\
\end{vmatrix} =
|A| + -k
\begin{vmatrix}
a & b \\
a & b \\
\end{vmatrix}
= |A|
$$

행렬식의 다섯 번째 특성은 \(A\)에 소거법을 적용하여 상삼각 행렬 \(U\)로 만들더라도 행렬식의 절댓값은 변하지 않는다는 것을 뜻한다. 이때 행렬식의 부호는 \(A\)에 적용한 행 교환 연산의 횟수에 따라 달라지므로, \(|A| = \pm |U|\)이다.

> 6. \(A\)의 한 행의 모든 성분이 \(0\)이라면, \(det \ A = 0\)이다.

$$
\begin{vmatrix}
a & b \\
0 & 0 \\
\end{vmatrix} = 0
$$

> 7. \(A\)가 \(n \times n\) 크기의 삼각 행렬이라면, \(det A = a_{11} a_{22} \cdots a_{nn}\)이다.

**증명:** \(A\)에 소거법을 적용해 \(A\)를 대각 행렬 \(D\)로 만들면, 행렬식의 다섯 번째 특성에 의해 \(|A| = |D|\)이다. 이 상태에서 행렬식의 첫 번째 특성과 세 번째 특성을 이용하면 \(|A| = a_{11} a_{22} \cdots a_{nn} \ |I|\)임을 알 수 있다.

> 8. \(det \ A \ne 0\)이면 \(A\)는 가역 행렬, \(det \ A = 0\)이면 \(A\)는 비가역 행렬이다.

**증명:** \(A\)가 가역 행렬이라면 \(A\)에 소거법을 적용해 \(A\)를 상삼각 행렬 \(U\)로 만들었을 때 대각 성분에 \(0\)이 아닌 피봇이 존재하므로, \(|A| = |U| \ne 0\)이다.

> 9. \(|AB|\) = \(|A||B|\)

**증명:** \(k = \frac{|AB|}{|B|} (|B| \ne 0\)\)라고 할 때, \(k\)는 행렬식의 첫 번째, 두 번째 및 세 번째 특성을 모두 만족하므로 \(k = \frac{|AB|}{|B|} = |A|\)이다.

행렬식의 아홉 번째 특성은 \(|A||A^{-1}| = |I| = 1\), 즉 \(|A^{-1}| = \frac{1}{|A|}\)임을 뜻한다.

> 10. \(det \ A = det \ A^T\)

### \(2 \times 2\) 행렬의 행렬식

\(2 \times 2\) 크기의 정사각 행렬 \(A = \begin{bmatrix}a & b \\ c & d\end{bmatrix}\)의 행렬식은 다음과 같이 구할 수 있다.

$$
\begin{vmatrix}
a & b \\ 
c & d
\end{vmatrix} =
\begin{vmatrix}
a & 0 \\ 
c & d
\end{vmatrix} +
\begin{vmatrix}
0 & b \\ 
c & d
\end{vmatrix}
$$

$$
= \begin{vmatrix}
a & 0 \\ 
c & 0
\end{vmatrix} +
\begin{vmatrix}
a & 0 \\ 
0 & d
\end{vmatrix}
$$

$$
+ 
\begin{vmatrix}
0 & b \\ 
c & 0
\end{vmatrix} +
\begin{vmatrix}
0 & b \\ 
0 & d
\end{vmatrix}
$$

$$
= \begin{vmatrix}
a & 0 \\ 
0 & 0
\end{vmatrix} +
\begin{vmatrix}
a & 0 \\ 
0 & d
\end{vmatrix}
$$

$$
+ 
\begin{vmatrix}
0 & b \\ 
c & 0
\end{vmatrix} +
\begin{vmatrix}
0 & b \\ 
0 & 0
\end{vmatrix}
$$

$$
= ad - 
\begin{vmatrix}
c & 0 \\ 
0 & b
\end{vmatrix}
$$

$$
= ad - bc
$$

> \(|A| = ad - bc\)

---

### 여인자 전개

\(3 \times 3\) 크기의 정사각 행렬은 \(2 \times 2\) 크기의 정사각 행렬에 대한 행렬식을 통해 계산할 수 있다.

$$
A = \begin{vmatrix}
a_{11} & a_{12} & a_{13} \\ 
a_{21} & a_{22} & a_{23} \\ 
a_{31} & a_{32} & a_{33} 
\end{vmatrix}
= \begin{vmatrix}
a_{11} & 0 & 0 \\ 
0 & a_{22} & a_{23} \\ 
0 & a_{32} & a_{33} 
\end{vmatrix}
$$

$$
+
\begin{vmatrix}
0 & a_{12} & 0 \\ 
a_{21} & 0 & a_{23} \\ 
a_{31} & 0 & a_{33} 
\end{vmatrix}
$$

$$
+
\begin{vmatrix}
0 & 0 & a_{13} \\ 
a_{21} & a_{22} & 0 \\ 
a_{31} & a_{32} & 0
\end{vmatrix}
$$

$$
= a_{11}(a_{22}a_{33} - a_{23}a_{32})
$$

$$
+
 \ a_{12}(a_{23}a_{31} - a_{21}a_{33})
$$

$$
+
 \ a_{13}(a_{21}a_{32} - a_{22}a_{31})
$$

> \(A\)의 제 \(i\)행과 제 \(j\)열을 제외하여 만들어지는 \(2 \times 2\) 행렬 \(M_{ij}\)을 \(A\)의 소행렬 (minor)이라 하고, \(C_{ij} = (-1)^{i + j} |M_{ij}|\)를 \(A\)의 여인자 (cofactor)라고 한다.

예를 들면, 위 식에서 \(C_{11} = |M_{11}| = (a_{22}a_{33} - a_{23}a_{32})\)이고, \(C_{12} = -|M_{12}| = -(a_{21}a_{33} - a_{23}a_{31})\)이다.

\(n \times n\) 크기의 정사각 행렬 \(A\)의 행렬식을 여인자를 이용해 나타내면 다음과 같다.

> \(det \ A = |A| = \sum_{k = 1}^{n}a_{ik}C_{ik}\), 이때 \(\sum_{k = 1}^{n}a_{ik}C_{ik}\)를 \(A\)의 \(i\)행에 대한 여인자 전개 (cofactor expansion)라고 한다.

> \(det \ A = |A| = \sum_{k = 1}^{n}a_{kj}C_{kj}\), 이때 \(\sum_{k = 1}^{n}a_{kj}C_{kj}\)를 \(A\)의 \(j\)열에 대한 여인자 전개 (cofactor expansion)라고 한다.

### 크래머 공식

이제 소거법 대신 행렬식만을 이용해 \(Ax = b\)의 해 \(x = A^{-1}b\)를 구하는 방법에 대해 살펴보자.

> **크래머 공식:** \(|A| \ne 0\)이라면, \(Ax = b\)의 해 \(x = A^{-1}b\)의 각 성분 \(x_i = \frac{det B_i}{det A}\)이다. (단, \(B_i\)는 \(A\)의 \(j\)번째 열을 \(b\)로 대체한 행렬)

크래머 공식을 이용하여 연립 방정식의 해를 계산하는 과정은 다음과 같다.

$$
\begin{equation}
    \begin{cases}
        -2x + 3y - z = 1 \\
        x + 2y - z = 4 \\
        -2x - y + z = -3
    \end{cases}
\end{equation}
$$

1. 연립 방정식을 \(Ax = b\) 형태로 나타내면

$$
A = \begin{bmatrix}
    -2 & 3 & -1 \\
    1 & 2 & -1 \\
    -2 & -1 & 1
\end{bmatrix}, \ 
b = \begin{bmatrix}
    1 \\
    4 \\
    -3
\end{bmatrix}
$$

$$
A 
\begin{bmatrix}
    x_1 \\
    x_2 \\
    x_3
\end{bmatrix} = b
$$

2. \(det \ A\) 계산하기

$$
|A| = \begin{vmatrix}
    -2 & 3 & -1 \\
    1 & 2 & -1 \\
    -2 & -1 & 1
\end{vmatrix}
$$

$$
= -2 * (2 - 1) - 3 * (1 - 2) + (-1) * (-1 + 4)
$$

$$
= -2 + 3 -3 = -2
$$

3. \(det \ B_1\), \(det \ B_2\)와 \(det \ B_3\) 계산하기

$$
det \ B_1 = -4, det \ B_2 = -6, det \ B_3 = -8
$$

4. \(x\)의 각 성분 계산하기

$$
x = \begin{bmatrix}
    \frac{-4}{-2} = 2\\
    \frac{-6}{-2} = 3\\
    \frac{-8}{-2} = 4
\end{bmatrix}
$$

---

### 참고 문헌

- [G. Strang, "Introduction to Linear Algebra," 5th ed. Wellesley-Cambridge Press, Wellesley, MA, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
