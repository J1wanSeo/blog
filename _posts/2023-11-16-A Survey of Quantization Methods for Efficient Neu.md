---
title: A Survey of Quantization Methods for Efficient Neural Network Inference
latitude: 37.24108640
longitude: 127.17755370
altitude: 0.0000
tags:
  - quantization
layout: post
date:   2023-11-16 14:57:45 +0900
categories: DNN
---

[[TOC]]


&nbsp;  
ref.  
[A Survey of Quantization Methods for Efficient Neural Network Inference](https://arxiv.org/pdf/2103.13630.pdf)

* * *

0.  # abstract
    

- AI의 발전과 함께 CNN과 같은 Neural Network의 사용이 증가하고 있다.
    - Restrained Circumstance나 Hardware가 restricted된 상황에서의 computational resource의 부족을 야기한다.
    - quantization has been arisen as reducing computational resources.
    - normally representing floating points as 4-bit or less value could reduce memory footprint by a factor of 16x.

1.  # Introduction
    
2.  # general history of quant.
    
    ![8a5bc709283aa11bafea6d25d13ad5fb.png](../../_resources/8a5bc709283aa11bafea6d25d13ad5fb.png)  
    ![8828f1f8ea538f080df5853a258ab5c5.png](../../_resources/8828f1f8ea538f080df5853a258ab5c5.png)
    
    1.  Quant가 디지털 프로세싱 영역에서도 중요해지고 있다.
    2.  foward error 와 backward error
        1.  foward error: x → y 일 때, y\*-y
        2.  backward error: y\* → x+ dx, dx
    3.  Quant 이후에 quant. model 과 non-quant. model 사이의 구조가 크게 달라질 수 있지만, 성능에서는 매우 좋은 효과를 가짐
3.  # concepts of quant.
    
4.  ## quant는 l(x,y,theta)에서 input x,y를 제외한 theta(fp)를 quant하여 사용함으로서 size를 축소하는 것
    
5.  ## uniform quant
    
    ```
    1.  Q = Int(r/S) - Z 
    2.  `S = b - a / 2^(bits) - 1: 가지고 있는 bit의 구간 사이즈`
    ```
    

![49500297e06b7ebad553587f6f9dda29.png](../../_resources/49500297e06b7ebad553587f6f9dda29.png)

3.  ## symmetric/asymmetric quant.
    
    1.  S를 설정할 때 b,a 의 값을 a = -b 로 설정하는 경우 symm. 아닌 경우 asymm.
    2.  act. func 를 지나면 parameter > 0 이므로 asymm.을 수행해야 한다. 이 때에는 Zero-point 를 0으로 지정
4.  ## Static quant. VS Dynamic quant.
    
    1.  clipping range를 언제 지정하는가에 따라 구분할 수 있음
    2.  static quant.의 경우 range를 미리 지정한 값( error를 최소화할 수 있도록 설계 MSE/entropy 등 사용)
5.  ## Quant. Granularity(granular : 그래놀라의 뜻 - 알갱이)
    

- range를 어떻게 설정하고 quant를 진행하는 지가 정확도에 영향을 미치므로, range를 정하는 방법에 대해 생각해 보겠다.

![186622868311c4a5a788d4f5c30e8aa2.png](../../_resources/186622868311c4a5a788d4f5c30e8aa2.png)  
a) Layerwise Quantization

- 하나의 Layer 안에 존재하는 convolution filter들의 weight들을 모두 고려하여 범주를 계산한다.

b) Groupwise Quantization

- 하나의 Layer 안에 존재하는 filter들을 그룹화 하여 range를 계산한다.
- 이 경우 parameter의 값이 다양할수록 유용하다. ex) Q-BERT의 transformer
- 계산량이 많아진다는 것이 단점이다.

==c) Channelwise Quantization==

- each filter 마다 range를 정하여 사용한다.

d) sub-channelwise Quantization

6.  ## Non-uniform quant.
    

- non-uniformly spaced하게 quant. 를 진행하는 것  
    ![a6b69d87aab9c7b6751d5fe9c1507c60.png](../../_resources/a6b69d87aab9c7b6751d5fe9c1507c60.png)
- 특정 구간 안에 존재 하는 경우 Q를 X로 배정시키는 것. i, i+1 사이의 간격은 일정하지 않다.
- 만약 parameter가 ==특정 구간에서 중요도가 높거나 낮다면 해당 구간을 더 잘게 쪼개어== 구분지어 주면 되므로 정확도를 높이는 데에 기여할 수 있다.  
    → 종 모양의 분포를 가지는 weight에 적합하게 method 가 개발되어 있다.  
    ex) logarithmic distribution을 이용하여 exponentially 증가시키는 것.  
    ex2) binary-code-based quant.
- 요즘에는 Q의 간격을 어떻게 배치하여야 quant 된 모델과 original 사이의 괴리를 줄일 수 있을지 고민하는 중.

> non-uniform이 속도 및 정확도의 측면에서 이점이 존재하지만 현재 CPU/GPU 같은 범용 프로세서를 사용하므로 uniform-quant.를 사용하는 것이 더 적합하다.

7.  ## Fine-tuning Methods
    

- quant.를 진행한 후 Neural Network 의 parameter를 adjust 하는 것이 필요하다.
- 두가지 방법이 존재하는데
    - re-training the model QAT (Quantization-Aware Training) : LEFT
    - re-training 없이 수행하는 PTQ (Post-Training Quantization) : RIGHT  
        ![14b33ca8d5e3f1d001803495d292cb62.png](../../_resources/14b33ca8d5e3f1d001803495d292cb62.png)

1.  ### QAT
    
    1.  pre-trained model의 parameter를 quantization 한다.
    2.  이후 train-set 을 가지고 quant. 된 pre-trained model을 다시 학습하여 loss 를 줄인다.
    3.  2번 과정 이후 fine-tuning 과정에서 parameter가 업데이트 되게 되고 이 과정 중에 quant되었던 weight들이 fp값으로 변한다. : backpropagation은 fp로 진행해야 zero gradient가 나오는 수를 막을 수 있으므로 필수적이다.
    4.  3번의 back propagation은 Q에 대해 진행한 것으로 이를 weight r (non-quant.)에 적용하려면 해당하는 모양으로 바꾸어 주어야 한다. 이 때 사용하는 것이 *STE*이다.

> STE : Straight Through Estimator dL/dQ를 그대로 dL/dr 로 사용하는 것  
> rounding operation을 무시하고 적용

**결국 re-train하는 과정에서 소모되는 비용이 크다. computational cost 가 너무 큼**

2.  ### PTQ
    
    1.  fine-tuning 을 진행하지 않고 quantization 한 system을 사용하는 것
    2.  ==따라서 re-train 하기 위한 추가적인 training data가 필요하지 않으므로 Data가 적은 경우에 사용하기 좋다.==
    3.  
3.  ### ZSQ (Zero-shot Quantization)
- quant 이후에 좋은 값을 찾는 행동 :  calibration
- quant 를 진행하게 되면 필연적으로 accuracy degradation이 발생한다.
- 이를 해결하기 위해서 trainset으로  tuning을 해야하는데 training dataset에 접근하지 못하는 경우가 많다.
- 이를 해결하기 위한 방법으로 ZSQ를 사용
1. Level 1 : ZSQ + PTQ &rarr; no data + no finetuning
- finetuning을 진행하지 않아도 되어 빠르고 쉬운 model quant.를 수행할 수 있다.
2. Level 2 : ZSQ + QAT &rarr; no data + yes finetuning
- accuracy degradation 해결에 있어서 의미 있는 수치의 진전을 보임
> ZSQ를 활용하는 제일 기본적인 방법은 GANs를 활용하는 것이다.
> 그렇다면 GAN이 적합한 data를 만들었는ㄴ지 확인하는 방법으로 pre-trained model에 집어 넣어서 정확한 데이터가 생성되었는지 확인하면 된다.

 __원본 데이터를 건드리지 않고 사용한다는 메리트가 있다.__
    

8.  ## Stochastic Quantization
<> deterministic quantization과 달리 확률적으로 quantization을 진행하는 것
-> 모든 parameter 가 quantization되지 않을 가능성을 남겨둔다.
 gradient가 매우 작으므로  quant. 안에서 rounding되는 경우 gradient가 사라지게 됨. 이에 대한 영향을 안받을 가능성
 
![KakaoTalk_Photo_2023-12-01-10-42-33.jpeg](../../_resources/KakaoTalk_Photo_2023-12-01-10-42-33.jpeg)

4. # Quantization below 8-bits
	1. ## Simulated Quantization
		- parameter는 quant.값으로 저장하고 arithmetic operation은 fp로 진행하여 사용하는 것.
		- 따라서 quant. 된 값을 arith. op.에 넣기 위해 dequant 하는 과정이 필요하다
		- 이는 정확도에 영향을 주기는 한다.

	2. ## Integer-only Quantization
		- parameter 와 arithmetic op. 모두 quant.된 것으로 사용
		- 정확도에서 손해가 존재하지만 속도, 파워, 저장 영역 등에서 이득이 더 크다.
&rarr; ? 일반적으로 integer-only quant.가 속도에 더 영향이 좋아서 사용하지만 bandwidth가 중요한 프로그램의 경우에는  simulated quant.를 사용하기도 한다. ( 메모리에 얼마나 자주 접근하는지가 중요하기 때문에 )
	3. ## mixed precision quant.
		- layer마다 여러 개의 bit로 quant.를 진행하는 것
		- 어떤 bit로 quant.를 진행할 지 선택하는 방법이 제일 중요한 영역이다.
		- sensitice 한 경우에는 더 높은 bit를 셀렉하여 사용한다.
		
	4. ## Hardware Aware Quant.
		- hw에 대한 정보를 바탕으로 quant하는 것.
		- lookup table 을 확인하고 이를 바탕으로 레이턴시와 같은 것을 계산해야 한다.
		
	5. ## Distillation-Assisted Quant.
	 - teacher 가 존재하여 그 학습한 data (parameter)를 가지고 학습에 도움을 받는 것.
	 - 상대적으로 더 큰 모델을 이용하여 작은 모델을 학습한다.
	 - 적합한 teacher를 고르는 것이 중요하다.
	 
	 6. ## Extreme Quantization
	 - 극단적으로 quant.를 진행하여 속도나 전력 소모를 매우 줄이는 것
	
	
	
	
![KakaoTalk_Photo_2023-12-01-10-41-44.png](../../_resources/KakaoTalk_Photo_2023-12-01-10-41-44.png)


![9d3019156a3a94e289e0ce95c6af2deb.png](../../_resources/9d3019156a3a94e289e0ce95c6af2deb.png)