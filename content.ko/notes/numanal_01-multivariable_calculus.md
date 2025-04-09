---
title: "수치 해석: 다변수 미적분학"
date: "2025-04-05T23:49:00+09:00"
hideReply: true
math: true
tags: ["calculus", "multivariable-calculus", "numanal", "numerical-analysis"]
---

### 다변수 함수

다변수 함수 (multivariable function)는 정의역 (domain)과 치역 (range)이 모두 실수인 \(1\)-변수 함수와 달리, 정의역이 \(n \ (n > 1)\)개 실수의 순서쌍이고 치역이 실수인 함수이다. 

> \(n\)개 실수의 순서쌍 \((x_1, x_2, \cdots, x_n)\)들의 집합 \(D\)를 정의역으로 가지는 다변수 함수 \(f\)는 정의역의 모든 원소를 단 하나의 실수 \(w = f(x_1, x_2, \cdots, f_n)\)에 대응시키는 규칙이다.
>
> 이때, \(x_1, x_2, \cdots, x_n\)을 \(f\)의 독립 변수 (independent variable, input variable)이라고 하며, \(w\)를 \(f\)의 종속 변수 (dependent variable, output variable)라고 한다.

![다변수 함수의 등고선 그래프](/images/notes/numanal_01-multivariable_calculus/contour_plot.png)

### 유계 영역

실수 집합에 대한 구간과 마찬가지로, \(2\)-변수 함수가 나타내는 영역은 열린 영역 (open region)일 수도 있고 닫힌 영역 (closed region)일 수도 있다.

> 평면 상에서 영역 \(R\)의 한 점 \(P(x_0, y_0)\)이 \(R\)에 완전히 포함되는 원판의 중심이 될 수 있을 때, \(P\)를 영역 \(R\)의 내부 점 (interior point)이라고 하며, \(P\)를 중심으로 하는 원판이 영역 \(R\)의 내부 점과 외부에 있는 점까지 포함할 경우 \(P\)를 경계 점 (boundary point)라고 한다.

내부 점과 경계 점의 개념은 단위 원판 (unit disk) \(x^2 + y^2 < 1\)과 \(x^2 + y^2 \le 1\)이 나타내는 부등식 영역을 통해 쉽게 이해할 수 있다. \(x^2 + y^2 < 1\)은 내부 점으로만 이루어진 열린 영역을 나타내고, \(x^2 + y^2 \le 1\)은 내부 점과 경계 점을 모두 포함하는 닫힌 영역을 나타낸다.

![단위 원판의 내부 점과 경계점](/images/notes/numanal_01-multivariable_calculus/boundary.png)

> 평면 상에서 유한한 반지름을 가지는 원판 안에 포함되는 영역을 유계 영역 (bounded region)이라고 한다.

예를 들면, 선분, 다각형, 원 등은 유계 영역이지만 직선, 평면, 좌표축이나 무한 구간에서 정의된 함수의 그래프는 유계 영역이 아니다.

### 극한과 연속

\(2\)-변수 함수의 극한을 이해할 때 주의할 점은, 독립 변수가 단 하나인 \(1\)-변수 함수에서의 극한의 정의와 달리 **\((x, y)\)가 주어진 점에 접근할 때 왼쪽 방향과 오른쪽 방향 외에도 모든 방향에서 접근할 수 있다는 것이다.** 이 부분을 제외한 나머지 내용은 \(1\)-변수 함수에 대한 엡실론-델타 논법 (epsilon-delta argument)과 동일하다.

"\(f(x, y)\)와 극한값 \(L\) 사이의 거리 \(|f(x, y) - L|\)를 \(\epsilon\) 미만으로 줄일 수 있니? \(\rightarrow\) \(f(x, y)\)와 주어진 점 사이의 거리가 \(\delta\)로 충분히 작으면 된다!" 

> **엡실론-델타 논법 (\(2\)-변수 함수):** 함수 \(f\)에 정의역에 속하는 임의의 점 \((x, y)\)와 실수 \(\epsilon \ (\epsilon > 0)\)에 대하여, 아래 조건을 만족하는 \(\delta \ (\delta > 0)\)이 존재한다면 \((x, y)\)가 \((x_0, y_0)\)에 접근할 때 \(f\)의 극한은 \(L\)에 접근한다고 한다. 

$$
0 < \sqrt{(x - x^0)^2 + (y - y_0)^2} < \delta \rightarrow |f(x, y) - L| < \epsilon
$$

> \((x, y)\)가 \((x_0, y_0)\)에 접근할 때 \(f\)의 극한은 \(L\)이라면, 다음과 같이 표현한다.

$$
\lim_{(x, y) \rightarrow (x_0, y_0)} f(x, y) = L
$$

\(2\)-변수 함수의 극한을 정의하였으므로 이제 연속성을 정의한다.

> 함수 \(f(x, y)\)가 점 \((x_0, y_0)\)에서 정의되고, \((x, y)\)가 \((x_0, y_0)\)에 접근할 때 \(f\)의 극한 \(L = f(x_0, y_0)\)일 때, \(f(x, y)\)는 점 \((x_0, y_0)\)에서 연속이다.

### 편도함수

![다변수 함수의 접선](/images/notes/numanal_01-multivariable_calculus/tangent_line.png)

> 점 \((x_0, y_0)\)에서 \(x\)에 대한 함수 \(f(x, y)\)의 편미분계수 (partial derivative)는 극한이 존재할 경우 다음과 같다.

$$
\frac{\partial f}{\partial x}(x_0, y_0) = \lim_{h \rightarrow 0}\frac{f(x_0 + h, y_0) - f(x_0, y_0)}{h}
$$

> 또한, 점 \((x_0, y_0)\)에서 \(y\)에 대한 함수 \(f(x, y)\)의 편미분계수는 극한이 존재할 경우 다음과 같다.

$$
\frac{\partial f}{\partial y}(x_0, y_0) = \lim_{h \rightarrow 0}\frac{f(x_0, y_0 + h) - f(x_0, y_0)}{h}
$$

**점 \((x_0, y_0)\)에서 \(x\)에 대한 함수 \(f(x, y)\)의 편미분계수는 \(x = x_0\)에서 \(x\)에 대한 \(1\)-변수 함수 \(f(x, y_0)\)의 미분계수와 같다.** 마찬가지로, 점 \((x_0, y_0)\)에서 \(y\)에 대한 함수 \(f(x, y)\)의 편미분계수는 \(y = x_0\)에서 \(y\)에 대한 \(1\)-변수 함수 \(f(x_0, y)\)의 미분계수와 같다. 편미분계수와 미분계수의 구별을 위해, 편미분계수는 미분계수의 \(d\) 대신 \(\partial\) (partial, round(-ed d))기호를 사용한다.

편미분계수가 존재하는 모든 점들의 집합을 정의역으로 하는 편도함수는 다변수 함수의 독립 변수 중에 하나를 선택하고 나머지 변수들은 상수 취급하여 계산한, 단 하나의 독립 변수에 대한 도함수를 뜻하며, 보통 \(\frac{\partial f}{\partial x}\), \(\frac{\partial z}{\partial x}\), 또는 \(f_x\)와 같이 나타낸다.

### 클레로의 정리

함수 \(f(x, y)\)를 두 번 미분하면 \(2\)계 편도함수를 얻을 수 있다. 예를 들면, \(f\)를 \(y\)에 대해 먼저 미분하고 다시 \(x\)에 대해 미분하여 얻은 \(2\)계 편도함수는 아래와 같이 나타낸다.

$$
\frac{\partial}{\partial x}(\frac{\partial f}{\partial y}) = \frac{\partial^2 f}{\partial x \partial y} = f_{xy}
$$

\(2\)계 편도함수 \(\frac{\partial^2 f}{\partial x \partial y}\)와 \(\frac{\partial^2 f}{\partial y \partial x}\)가 항상 같은 것은 아닌데, **클레로의 정리 (Clairaut's theorem)에 의하면 두 \(2\)계 편도함수가 같기 위해서는 \(f\), \(f_x\), \(f_y\), \(f_{xy}\)와 \(f_{yx}\)가 모두 연속이어야 한다.**

> **클레로의 정리:** 함수 \(f\)와 도함수 \(f_x\), \(f_y\), \(f_{xy}\)와 \(f_{yx}\)가 점 \((a, b)\)를 포함하는 열린 영역에서 정의되고 \((a, b)\)에서 모두 연속이면 다음이 성립한다.

$$
f_{xy}(a, b) = f_{yx}(a, b)
$$

### 미분 가능성

> 함수 \(z = f(x, y)\)에서 \(f_x(x_0, y_0)\)과 \(f_y(x_0, y_0)\)이 존재하고 \(\Delta z\)가 아래 방정식을 만족하면, \(f\)는 \((x_0, y_0)\)에서 미분 가능하다. (단, \(\Delta x \rightarrow 0\)이고 \(\Delta y \rightarrow 0\)일 때 \(\epsilon_1 \rightarrow 0\)이고 \(\epsilon_2 \rightarrow 0\))

$$
\Delta z = f_x(x_0, y_0)\Delta x + f_y(x_0, y_0)\Delta y + \epsilon_1 \Delta x + \epsilon_2 \Delta_y
$$

(추가 예정)

### 연쇄 법칙

\(1\)-변수 함수 \(y = f(u)\)와 \(u = g(x)\)로 이루어진 합성 함수 \(f \circ g\)의 도함수 \((f \circ g)'\)는 아래와 같이 연쇄 법칙 (chain rule)을 이용하여 구할 수 있는데, 여기서 \(u\)는 중간 변수 (intermediate variable)이고 \(x\)는 독립 변수이다. 

$$
(f \circ g)'(x) = f'(g(x)) \cdot g'(x)
$$

$$
\frac{dy}{dx} = \frac{dy}{du} \cdot \frac{du}{dx}
$$

**합성 함수가 여러 개의 중간 변수와 독립 변수를 가지더라도, 연쇄 법칙을 이용하면 (편)도함수를 쉽게 계산할 수 있다.** 예를 들어, 독립 변수 \(t\)와 중간 변수 \(x = x(t)\), \(y = y(t)\)로 이루어진 합성 함수의 도함수를 구해보자.

> \(2\)-변수 함수 \(w = f(x, y)\)가 미분 가능하고 \(t\)에 대한 두 함수 \(x = x(t)\), \(y = y(t)\)가 미분 가능할 때, \(w = f(x(t), y(t))\)의 도함수는 다음과 같다.

$$
\frac{dw}{dt} = f_x(x(t), y(t))x'(t) + f_y(x(t), y(t))y'(t)
$$

$$
\frac{dw}{dt} = \frac{\partial f}{\partial x} \frac{dx}{dt} + \frac{\partial f}{\partial y} \frac{dy}{dt}
$$

중간 변수가 \(x = x(t)\), \(y = y(t)\), \(z = z(t)\)로 하나 더 늘어나더라도, \(z\)에 대한 항을 하나만 더 추가해주면 하나의 독립 변수 \(t\)와 세 중간 변수 \(x\), \(y\)와 \(z\)에 대한 공식을 얻을 수 있다.

$$
\frac{dw}{dt} = \frac{\partial f}{\partial x} \frac{dx}{dt} + \frac{\partial f}{\partial y} \frac{dy}{dt} + \frac{\partial f}{\partial z} \frac{dz}{dt}
$$

독립 변수의 개수가 하나 더 늘어나면 공식은 어떻게 바뀔까? 두 독립 변수 \(r\), \(s\)와 세 중간 변수 \(x = g(r, s)\), \(y = h(r, s)\), \(z = k(r, s)\)로 이루어진 함수 \(w = f(x, y, z)\)의 편도함수 \(\frac{dw}{dr}\)와 \(\frac{dw}{ds}\)는 아래와 같이 구할 수 있다.

$$
\frac{dw}{dr} = \frac{\partial f}{\partial x} \frac{dx}{dr} + \frac{\partial f}{\partial y} \frac{dy}{dr} + \frac{\partial f}{\partial x} \frac{dz}{dr}
$$

$$
\frac{dw}{ds} = \frac{\partial f}{\partial x} \frac{dx}{ds} + \frac{\partial f}{\partial y} \frac{dy}{ds} + \frac{\partial f}{\partial x} \frac{dz}{ds}
$$

일반적으로, 여러 개의 중간 변수와 독립 변수를 가지는 합성 함수의 (편)도함수는 각각의 중간 변수에 대한 \(w\)의 편도함수로 이루어진 벡터 \((\frac{\partial w}{\partial x}, \frac{\partial w}{\partial y}, \cdots)\)와 각각의 독립 변수에 대한 중간 변수의 편도함수로 이루어진 벡터 \((\frac{\partial x}{\partial p}, \frac{\partial y}{\partial p}, \cdots)\)의 내적으로 볼 수 있다.

---

### 참고 문헌

- [G. B. Thomas, Jr., J. R. Hass, C. E. Heil, M. D. Weir, "Thomas' Calculus," 14th ed. Pearson Education, 2021.](#)
- [G. Strang, "Linear Algebra and Learning from Data," Wellesley-Cambridge Press, 2019.](https://math.mit.edu/~gs/learningfromdata/)