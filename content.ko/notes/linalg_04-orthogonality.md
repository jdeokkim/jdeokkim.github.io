---
title: "선형 대수: 직교성"
date: "2025-03-28T18:09:00+09:00"
hideReply: true
math: true
tags: ["linear-algebra", "linalg", "numpy"]
---

### 부분 공간 사이의 직교 관계

두 벡터 \(v\)와 \(w\)가 직교 (orthogonal) 관계에 있다는 것은 \(v\)와 \(w\)의 내적이 \(0\), 즉 \(v \cdot w = v^T w = 0\)이라는 것을 뜻한다.

벡터 공간 (부분 공간)도 벡터와 마찬가지로 직교 관계를 정의할 수 있다.

> 벡터 공간 \(V\)와 \(W\)에서, \(V\)의 모든 벡터 \(v\)와 \(W\)의 모든 벡터 \(w\)에 대해 \(v^T w = 0\)일 때, \(V\)와 \(W\)는 직교 관계에 있다. 이때, **\(V\)와 \(W\)가 서로 만나는 지점은 영 벡터 단 하나뿐이다.**

따라서 두 벡터 공간의 직교 관계는 두 평면의 수직 (perpendicular) 관계와 달리, **영 벡터 외에는 어떠한 지점도 공유하지 않는다.**

이제 [네 개의 주요 부분 공간]({{< ref "linalg_03-vector_spaces.md" >}})에 대해 다시 생각해보자. \(Ax = b\)에서 \(N(A)\)는 \(Ax = 0\)을 만족하는 모든 \(x\)가 속한 공간이고, \(C(A^T)\)는 \(A\)의 모든 행과 \(y\)의 선형 결합 \(A^Ty\)이 속한 공간이다. 그런데 \(x^T(A^Ty) = (Ax)^Ty = 0\)이므로, \(N(A)\)와 \(C(A^T)\)는 직교 관계임을 알 수 있다. 마찬가지로 \(N(A^T)\)와 \(C(A)\)도 직교 관계에 있다.

> \(N(A)\)와 \(C(A^T)\), 그리고 (N(A^T)\)와 \(C(A)\)는 직교 관계에 있다.

### 정사영

(추가 예정)

### 정규 직교 기저

(추가 예정)

### Gram–Schmidt 과정

(추가 예정)

---

### 참고 문헌

- [G. Strang, "Introduction to Linear Algebra," 5th ed. Wellesley-Cambridge Press, 2016.](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)
