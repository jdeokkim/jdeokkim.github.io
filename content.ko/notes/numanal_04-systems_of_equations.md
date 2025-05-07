---
title: "수치 해석: 연립 방정식의 풀이"
date: "2025-05-06T20:55:00+09:00"
hideReply: true
math: true
tags: ["numerical-analysis"]
---

### 가우스 소거법

선형 대수에서 \(Ax = b\) 형태의 연립 일차 방정식 (systems of linear equations, linear systems)의 해 \(x = A^{-1}b\)를 구하는 가장 기초적인 방법은 가우스 소거법 (Gaussian elimination)을 이용하는 것이다.

가우스 소거법은 첨가 행렬 (augmented matrix) \(\begin{bmatrix} A \ | \ b \end{bmatrix}\)에 아래와 같은 기본 행 연산 (elementary row operation)을 한 번 이상 적용하여 \(\begin{bmatrix} U \ | \ c \end{bmatrix}\) 형태로 만들고 \(Ux = c\)의 해를 구하는 방법이다.

> 1. \(i\)번째 행에 \(j\)번째 행의 \(k\)배만큼을 더한다.
> 2. \(i\)번째 행을 \(k\)배로 만든다.
> 3. \(i\)번째 행과 \(j\)번째 행을 서로 교환한다.

먼저, 첨가 행렬에 기본 행 연산을 적용하여 주어진 행렬 \(A\)를 상삼각행렬 형태 \(U\)로 변환하는 알고리즘을 구현해보자.

(추가 예정)

### 부분 피봇팅

(추가 예정)

---

### 희소 행렬

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