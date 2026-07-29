# Day 05 - Attention (Scaled Dot-Product Attention)

## 목표

오늘은 Transformer의 Attention에서 왜 **√dₖ(Scaled Attention)** 로 나누는지 학습하고, 직접 실험을 통해 확인하였다.

논문(Attention Is All You Need)의 주장

> Query와 Key의 각 성분이 평균 0, 분산 1이라면  
> **Q·Kᵀ(내적)의 분산은 dₖ가 된다.**

따라서 dₖ가 커질수록 점수가 지나치게 커지므로

\[
\frac{QK^T}{\sqrt{d_k}}
\]

로 나누어 분산을 일정하게 유지한다.

---

# 실험 1 : q·k의 분산 확인

## 목적

차원(dₖ)이 커질수록 q·k의 분산이 실제로 dₖ에 비례하는지 확인한다.

## 결과

- dₖ가 증가할수록 q·k의 분산도 거의 비례하여 증가하였다.
- 논문의 주장(분산 = dₖ)과 거의 일치하였다.

### 생성 결과

- mission2-분산.png

---

# 실험 2 : Softmax 포화 확인

## 목적

내적값을 √dₖ로 나누지 않았을 때 Softmax가 어떻게 변하는지 확인한다.

## 결과

- dₖ가 커질수록 Softmax 출력이 1에 가까워졌다.
- Attention이 한 위치에만 집중되었다.
- 나머지 위치의 가중치는 거의 0이 되었다.

### 생성 결과

- mission2-포화.png

---

# TODO

## TODO 1

### 문제

dₖ를 4배 키우면 q·k의 분산은 몇 배가 될까?

### 답

**4배**

---

## TODO 2

### 문제

나누지 않으면 무엇이 문제인가?

### 답

> 나누지 않으면 dₖ가 커질수록 q·k의 분산이 증가하여 Softmax가 포화되고, Attention이 한 위치에만 집중되어 다른 위치의 기울기가 거의 0이 되어 학습이 어려워진다.

---

# 오늘 배운 내용

- Attention은 Query와 Key의 유사도를 내적으로 계산한다.
- 내적의 분산은 차원(dₖ)에 비례하여 증가한다.
- 점수가 너무 커지면 Softmax가 포화된다.
- Softmax가 포화되면 한 위치에만 Attention이 집중된다.
- 다른 위치의 Gradient가 거의 0이 되어 학습이 잘 이루어지지 않는다.
- 이를 방지하기 위해 Transformer는 √dₖ로 나누는 Scaled Dot-Product Attention을 사용한다.

---

# 핵심 정리

- q·k의 분산 ≈ dₖ
- dₖ가 커질수록 Softmax가 포화된다.
- 포화를 막기 위해 √dₖ로 나눈다.
- 이것이 **Scaled Dot-Product Attention**이다.