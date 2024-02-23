---
title: 'AWQ: Activation-aware Weight Quantization for LLM Compression and Accelertaion'
layout: post
date: 2024-02-23 03:48:19Z
created: 2024-02-23 02:09:43Z
categories: Quantization
tags:
  - [ FPGA, SoC, quantization ]
use_math: true
latitude: 37.56653500
longitude: 126.97796920
altitude: 0.0000
---

ref : [AWQ: Activation-aware Weight Quantization for LLM Compression and Accelertaion](https://arxiv.org/abs/2306.00978)

# Intorduction
- transformer를 기반으로 하는 LLM은 근래 많은 사용을 겸하고 있지만 데이터셋 자체의 방대한 크기와 용량으로 인해 Edge Device에서의 사용이 어려운 상태이다.
- 이에 대안으로 Low-bit Quantization 을 수행하여 사용한다.
	- QAT : high training cost로 인해서 사용하기 어렵다
	- PTQ : 수행하는 경우 Accuracy degradation이 너무 크게 발생하여 효과가 부족하다.
	- GPTQ : GPTQ의 경우 ==2계의 정보를 사용==해서 최대한 양자화 에러를 해소하려고 한다.
		- 하지만 이 또한 generalist model에서는 문제가 발생할 수 있다.
			- distorting learned feature
			- over-fit calibration issue
# AWQ: Activation-aware Weight Quantization
## 2.1 Improving LLM Quantization by Preserving 1% Salient Weight
- LLM의 filter 의 모든 weight가 동등하게 중요도를 가지고 있는 것이 아님에 중점을 두었다.
- 중요한 weight 를 *salient weight*라고 칭하며 이 salient weight 는 quantization을 배제한 채(remaining at FP16)로 그대로 사용한다. 
- 그렇다면 salient weight 인지 어떻게 판단할 것인가?
	1. *activation magnitude*가 큰 경우
	2. L~2~-norm의 값이 큰 경우
	&rarr; 2번의 경우 성능(quantizatized performance)에 불리하다.
	따라서 주로 1번의 방법을 선택해서 중요도를 나타낸다.
### 한계점
- FP16으로 quantization하지 않는 것이 아니라 다른 방법으로 보존하는 방법을 알면 좋음

## 2.2 Protecting Salient Weights by Activation-aware Scaling
![Screenshot 2024-02-23 at 12.47.48.jpg](../../_resources/Screenshot%202024-02-23%20at%2012.47.48.jpg)

- quantization error 를 줄이는 방법으로 per-channel scaling 를 사용하면 hw inefficiency issue를 줄일 수 있다.
$
Q(w) = \Delta\cdot Round(w/\Delta), \Delta = max(|w|)/2^{N-1}
$
의 기존 수식에서 weight 에 ==scale factor s==를 곱하고 input activation을 s로 나누어 준다. 그러면 아래와 같은 수식을 유도할 수 있다.

$
Q(w\cdot s)\cdot x/s = \Delta'\cdot Round(ws/\Delta) \cdot x \cdot 1/s
$

1. 이 때 $\Delta'$는 quantizatio  scaler로 기존의 $\Delta$와 차이점은 weight 의 하나의 element만 s 를 곱한 다음 사용한다는 차이가 있다.
2. 즉, 미미한 차이를 가지므로 $\Delta' = \Delta$를 만족한다. 
3. 결국 scale factor s 를 곱하기 전과 비교한 상대오차는 $\Delta' / \Delta \cdot 1/s$ 로 표현할 수 있다.
4.  s > 1 을 선택한다면 오차가 작아지는 것을 확인할 수 있다.
5. 그렇다면 s가 크면 무조건 오차가 작아지니까 좋은 것이 아닐까?
6. 정작 s 가 너무 커지게 되면 $\Delta'$ 가 같이 증가하게 되고 2에서 말한  $\Delta' = \Delta$ 이 성립할 수 없어진다.
7. 따라서 적당한 s 를 선택하는 것이 좋다. 

### How to set adequate s
- idea: s를 이용하는 식을 통해 미분해서 구하자
- s에 관한 식이 미분 불가능한 성질을 가지고 있어서 해당 방법은 사용할 수 없다.
&rarr; approx. gradient 방법을 선택해서 수행한다.
$
s = sx^\alpha, \alpha^* = arg min L(sx^\alpha)
$
이 식에서 $\alpha$를 찾기 위해서 fast-grid search 라는 방법을 사용하여 구한다.
또한, Clipping method를 통해서 MSE error를 줄일 수 있다.
	-  clipping 수행 시 $\Delta'$를 줄일 수 있으므로 위의 3번 식에서 분자가 줄어든다.
## Advantages
- regression이나 backpropagation을 사용하지 않는다.
-  calibration set에 의존성이 매우 낮다.
	-  average magnitude per channel 을 사용하므로 
	-  이를 통해서 over-fitting의 문제도 해결할 수 있다.
-  최종적으로 quantization 함에 있어 데이터양이 적어도 가능하다.

# Opinion
op) ==salient weight를 fp16이 아닌 비교적 높은 precision의 방법으로 quantization 하는 것은 어떨까?==

그렇게 하려면 salient weight를 감지하고 변환하는 알고리즘 필요할 것
