---
title: "논문 리뷰: How to Read a Paper"
date: "2024-03-27T09:21:00+09:00"
hideReply: true
math: true
tags: ["literature-review", "research-paper"]
---

### 논문을 읽어야 하는 이유

1. **대학원생이나 연구원에게 논문을 읽는 능력은 필수적**
2. 교과서나 강의 내용에는 없는 최신 기술 습득 가능
3. 나의 관심 분야에 대한 연구 동향 파악

---

### 논문 저자의 목표

- 새로운 문제 또는 기존 문제의 해법 제시
- 기존 해법이 가진 문제점 지적
- 해법의 구현부 개선 방법 설명

### 논문 독자의 목표

- **잘 모르는 분야 또는 문제에 대한 지식 습득**
- 문제 해결을 위한 새로운 방법 학습
- 연구 과정 및 논문 작성 방법 공부
- 동료 평가 (peer review) 수행
- 서베이 (survey) 논문 작성

### 주요 학술지 (컴퓨터 그래픽스)

- ACM ToG (Transactions on Graphics)
- IEEE TVCG (Transactions on Visualization and Computer Graphics)
- SIGGRAPH
- Eurographics
- EGSR, HPG, I3D, etc.

---

### 논문을 읽는 방법

1. **1회독 (5-10분):** 논문을 빠르게 훑어보며 내용을 간략하게만 이해한다.
2. **2회독 (30-60분):** 그림이나 그래프를 살펴보고, 논문 배경을 이해하기 위해 필요한 참고 문헌은 따로 표시해놓는다.
3. **3회독:** 내가 논문 저자라고 생각하고, 저자와 똑같은 가정 하에 방정식과 알고리즘 등의 수식을 직접 유도해본다.

### 논문의 1회독 과정

아래 단계를 5-10분 동안 차례대로 수행한다.

1. 논문의 제목 (title), 초록 (abstract)과 서론 (introduction)을 꼼꼼히 읽는다.
2. 논문의 각 표제를 읽어보되, 세부 내용이나 그림 등은 모두 건너뛴다.
3. 결론을 바로 읽고, 참고 문헌 부분을 훑어보며 이미 읽어본 논문이 몇 개 정도 되는지 확인해본다.

---

> 1회독이 끝나면, 아래 질문에 답할 수 있어야 한다.
> 
> - **Category:** 이 논문의 종류는 무엇인가?
> - **Context:** 이 연구와 관련된 다른 논문은 무엇인가? 그리고 문제 해결을 위해 사용된 배경 지식은 무엇인가?
> - **Correctness:** 논문에서 기술한 가정 (assumption)에 문제가 없는가?
> - **Contributions:** 이 연구가 새롭게 기여하는 내용은 무엇인가?
> - **Clarity:** 논문이 이해하기 쉽게 잘 작성되었는가?

---

그 다음에는 앞에서 얻은 정보를 바탕으로, 이 논문을 계속 읽을지 말지를 결정해야 한다. 논문에서 다루는 주제가 나의 관심 분야와 관련이 없거나, 내가 잘 모르는 분야의 주제거나, 논문의 가정에 문제가 있는 경우, 논문을 더 이상 읽지 않는 것이 좋을 수도 있다.

### 논문의 2회독 과정

1회독 때보다 꼼꼼히, 약 1시간 정도 읽되, 증명이나 알고리즘 등의 세부 내용은 무시하고 넘어간다.

1. 그림 (figure), 다이어그램 (diagram)이나 그래프 (graph) 등을 유심히 확인한다.
2. 그래프의 경우 각 축에 레이블 (label)이 제대로 작성되어 있는지, 결과가 통계학적으로 유의미한지 관찰해본다.
3. 논문의 배경 지식을 이해하기 위해 참고 문헌에서 해당 논문과 관련성이 높은 논문을 표시해둔다.

컴퓨터 그래픽스 분야의 논문은 보통 논문 제목과 저자 목록이 위치한 첫 부분에 기존 연구 결과와 논문의 연구 결과를 비교하는 "티저 (teaser)" 그림을 넣는 경우가 많은데, 이러한 "티저" 그림은 논문의 연구 결과가 어떤 문제를 얼마나 잘 해결하는지를 보여주고 논문이 독자의 기억에 오래 남도록 한다.

2회독 과정이 끝나면, 독자는 논문의 핵심 내용을 대략적으로 이해할 수 있게 되고, 지금까지 이해한 내용과 이를 뒷받침하는 증거를 다른 사람에게 설명할 수 있게 된다.

### 논문의 3회독 과정

**논문의 모든 내용을 완전히, 그리고 제대로 이해하기 위해서는 논문을 최소 3번 이상은 읽어봐야 한다.** 3회독의 핵심은 논문의 저자와 똑같은 가정을 가지고 증명, 방정식과 알고리즘 등의 연구 내용을 직접 유도해보는 것이다. 이렇게 재현해본 연구 내용을 논문의 실제 연구 내용과 비교해보면, 해당 연구가 왜 기존 연구에 비해 새롭고 혁신적인지를 알 수 있게 된다.

3회독을 성공적으로 마치기 위해서는 논문을 매우 꼼꼼하게 읽어야 한다. 특히, 논문을 읽을 때는 알고리즘의 입력과 출력, 사용된 기호의 의미, 작동 원리에 대해 모두 알아야 하고, 연구에 적힌 가정에 대해 비판적으로 생각해보아야 한다. 이러한 과정은 처음에는 4-5시간 정도 걸릴 수도 있지만, 여러 논문을 계속 읽다 보면 약 1시간 정도로 단축할 수 있다.

3회독이 끝나고 난 이후에는 논문에 적힌 모든 내용을 논문을 보지 않고 처음부터 끝까지 요약해서 정리할 수 있어야 하며, 기존 연구와 비교했을 때 논문에서 다루는 연구의 강점과 약점이 무엇인지도 설명할 수 있어야 한다.

---

### 참고 문헌

- [M. McGuire, "How to Read a Realistic Rendering Paper," CS888, University of Waterloo, Sep. 2019.](https://morgan3d.github.io/advanced-ray-tracing-course/reading-research.pdf)
- [S. Keshav, "How to Read a Paper,"  ACM SIGCOMM Computer Communication Review, vol. 37, no. 3, Jul. 2007.](http://ccr.sigcomm.org/online/files/p83-keshavA.pdf)