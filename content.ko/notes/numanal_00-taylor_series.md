---
title: "수치 해석: 테일러 정리"
date: "2025-04-05T12:49:00+09:00"
hideReply: true
math: true
tags: ["calculus", "numanal", "numerical-analysis", "taylor-series"]
---

테일러 정리 (Taylor's theorem)는 복잡한 형태의 비선형 함수 (nonlinear function)를 다항식의 무한 급수 (infinite series) 형태로 근사 (approximate)할 수 있게 해주며, 수치 해석 (numerical analysis)와 딥 러닝 (deep learning)을 이해하기 위해 반드시 알아야 하는 수학적 개념이다.

### 수열의 극한

> 수열 (sequence) \({a_n}\)은 \(a_1, a_2, \cdots, a_n\)와 같이 순서가 정해진 수를 나열한 것이다.

수열을 이루는 각각의 수를 수열의 항 (term)이라고 하는데, 예를 들어 \(a_10\)은 수열에서 \(10\)번째로 나타나는 수 또는 수열의 \(10\)번째 항을 뜻한다.

\(a_1, a_2, \cdots, a_n, \cdots\)처럼 수열의 항을 무한히 나열한 것을 무한 수열 (infinite sequence)라고 하는데, **무한 수열은 정의역이 양의 정수이고 공역이 실수 또는 복소수인 \(f(n) = a_n\) 형태의 함수로 볼 수 있다.**

무한 수열 중에는 \(n\)이 증가함에 따라 \(a_n\)이 특정 값에 수렴 (converge)하는 수열도 있고, \(a_n\)이 무한히 커지거나 작아지는, 즉 \(a_n\)이 발산 (diverge)하는 수열도 있다. 수열의 극한에 대한 내용을 엄밀하게 정의하면 다음과 같다.

> 임의의 \(\epsilon > 0\)에 대해 \(n > N \Rightarrow |a_n - L| < \epsilon\)을 만족하는 정수 \(N\)이 존재하는 수열 \({a_n}\)는 극한 \(L\)에 수렴 (converge)하며, 그렇지 않은 수열은 발산 (diverge)한다.
>
> \({a_n}\)이 \(L\)에 수렴할 때, 다음과 같이 나타낸다.

$$
\lim_{n \rightarrow \infty} a_n = L
$$

> 또한, \({a_n}\)이 양의 무한대 또는 음의 무한대로 발산할 때, 다음과 같이 나타낸다.

$$
\lim_{n \rightarrow \infty} a_n = \infty 
$$

$$
\lim_{n \rightarrow \infty} a_n = -\infty 
$$

### 무한 급수

> 무한 수열의 각 항을 더한 합 \(\sum_{k = 1}^{\infty} a_n = a_1 + a_2 + \cdots\)을 무한 급수 (infinite series)라고 한다.

무한 급수에서 첫 번째 항부터 \(n\)번째 항까지의 합 \(s_n = a_1 + a_2 + \cdots + a_n\)을 \(n\)번째 부분 합 (\(n\)-th partial sum)이라고 한다.

> 상수 \(a \ne 0\)와 \(r\)에 대해, 아래와 같은 형태를 가진 무한 급수를 기하 급수 (geometric series) 또는 등비 급수라고 하며, \(a\)와 \(r\)을 각각 초기 항과 공비 (ratio)라고 한다.

$$
\sum_{k = 1}^{\infty} ar^{n - 1} = a + ar + ar^2 + \cdots
$$

기하 급수는 \(|r|\)에 따라 수렴 여부가 달라지는데, 기하 급수의 수렴 여부를 확인해보기 위해 급수의 부분 합을 이용해보자.

$$
s_n = a + ar + \cdots + ar^{n - 1}
$$

$$
rs_n = ar + ar^2 + \cdots + ar^n
$$

$$
(1 - r)s_n = a - ar^n = a(1 - r^n) 
$$

$$
\therefore s_n = \frac{a(1 - r^n)}{1 - r} (r \ne 1)
$$

따라서 \(|r| < 1\)일 때 기하 급수의 극한을 얻을 수 있다.

> \(|r| > 1\)이면 기하 급수 \(\sum_{k = 1}^{\infty} ar^{n - 1}\)는 발산하며, \(|r| < 1\)이면 기하 급수는 극한 \(L\)을 가진다.

$$
L = \frac{a}{1 - r}
$$

### 거듭제곱 급수

수로 이루어진 무한 급수가 아닌, 다항식의 항으로 이루어진 무한 급수를 거듭제곱 급수 (power series) 또는 멱급수라고 한다.

> 아래와 같은 형태의 무한 급수를 \(x = a\)를 중심 (center)으로 하는 거듭제곱 급수라고 하며, 상수 \(c_0, c_1, \cdots\)를 \(n\)번째 계수 (coefficient)라고 한다.

$$
\sum_{n = 0}^{\infty} c_n (x - a)^n = c_0 + c_1(x - a) + c_2(x - a)^2 + \cdots
$$

이제 다음과 같은 거듭제곱 급수를 생각해보자.

$$
\sum_{n = 0}^{\infty} x^n = 1 + x + x^2 + \cdots
$$

이 거듭제곱 급수는 기하 급수이기도 하므로, \(|x| < 1\)일 때 \(\frac{1}{1 - x}\)로 수렴한다.

$$
\frac{1}{x - 1} = 1 + x + x^2 + \cdots (|x| < 1)
$$

**여기서 알 수 있는 중요한 사실은, \(\frac{1}{1 - x}\)를 단순히 극한으로 보는 것이 아니라, 하나의 함수로 볼 수도 있다는 것이다.** 그러면 거듭제곱 급수의 부분 합 \(1 + x + x^2 + \cdots + x^n\)은 \(\frac{1}{1 - x}\)를 근사적으로 나타낸 함수라고 생각할 수 있다.

$$
f(x) = \frac{1}{x - 1} = 1 + x + x^2 + \cdots (|x| < 1)
$$

### 테일러 급수

테일러 급수 (Taylor series)를 이용하면 \(f(x) = \frac{1}{1 - x}\) 형태의 함수 외에도, **무한 번 미분 가능한 일반적인 함수에 대한 거듭제곱 급수를 만들 수 있다.**

> \(x = a\)가 속한 구간에서 \(f\)가 무한 번 미분 가능할 때, \(x = a\)에서의 테일러 급수 (Taylor series)를 다음과 같이 정의한다. 
>
> 또한, \(x = 0\)에서의 테일러 급수를 \(f\)의 매크로린 급수 (Maclaurin series)라고 한다.

$$
\sum_{k = 0}^{\infty} \frac{f^{(k)}(a)}{k!}(x - a)^k =
$$

$$
f(a) + \frac{f'(a)}{1!}(x - a)^1 + \cdots
$$

테일러 급수의 \(n\)번째 부분 합은 \(n\)계 테일러 다항식 (Taylor polynomial of order \(n\))이라고도 한다.

> \(x = a\)가 속한 구간에서 \(f\)가 \(k\)번 미분 가능할 때, \(x = a\)에서 \(f\)의 \(n\)계 테일러 다항식 \(P_n(x)\)를 다음과 같이 정의한다.
>
> (단, \(k = 1, 2, \cdots, N\)이고, \(0 \le k \le N\))

$$
P_n(x) = f(a) + \frac{f'(a)}{1!}(x - a) + \cdots +
$$

$$
\frac{f^{(n)}(a)}{n!}(x - a)^n
$$

이제 몇 가지 일반적인 함수들을 테일러 (매크로린) 급수로 나타내보자.

- \(f(x) = e^x\)의 테일러 급수

$$
f(0) + \frac{f'(0)}{1!}x + \frac{f''(0)}{2!}x^2 + \cdots
$$

$$
= 1 + \frac{1}{1!}x + \frac{1}{2!}x^2 + \cdots
$$

$$
= 1 + x + \frac{x^2}{2!} + \cdots
$$

- \(f(x) = sin \ x\)의 테일러 급수

$$
f(0) + \frac{f'(0)}{1!}x + \frac{f''(0)}{2!}x^2 + \cdots
$$

$$
= \sum_{k = 0}^{\infty} \frac{(-1)^k}{(2k + 1)!}x^{2k + 1}
$$

- \(f(x) = cos \ x\)의 테일러 급수

$$
f(0) + \frac{f'(0)}{1!}x + \frac{f''(0)}{2!}x^2 + \cdots
$$

$$
= \sum_{k = 0}^{\infty} \frac{(-1)^k}{(2k)!}x^{2k}
$$

### 테일러 정리

\(n\)계 테일러 다항식을 이용해 \(f(x)\)를 근사적으로 나타낸다는 것은 곧 **테일러 급수에서 \(n + 1\)번째 항부터 시작하는 나머지 부분 \(R_n(x)\)의 합이 테일러 다항식과 실제 \(f(x)\) 사이의 오차 (error)를 나타낸다는 것을 뜻한다.**

$$
f(x) = P_n(x) + R_n(x)
$$

$$
= (f(0) + \frac{f'(0)}{1!}x + \cdots + \frac{f^{(n)}(0)}{n!}x^n) \ +
$$

$$
(\frac{f^(n + 1)(0)}{n!}x^{n + 1}) + \cdots
$$

(추가 예정)

---

### 참고 문헌

- [G. B. Thomas, Jr., J. R. Hass, C. E. Heil, M. D. Weir, "Thomas' Calculus," 14th ed. Pearson Education, 2021.](#)
- [G. Strang, "Linear Algebra and Learning from Data," Wellesley-Cambridge Press, 2019.](https://math.mit.edu/~gs/learningfromdata/)