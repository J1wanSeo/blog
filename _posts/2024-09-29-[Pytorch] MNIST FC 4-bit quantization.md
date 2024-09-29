---
title: [Pytorch] MNIST FC 4-bit quantization
layout: post
date: 2024-09-29 08:39:28Z
created: 2024-09-29 06:52:19Z
tags: AI, SOC, pytorch

toc: true
toc_sticky: true

latitude: 37.56653500
longitude: 126.97796920
altitude: 0.0000
---

# 개요

- pytorch 는 기본적으로 int8 양자화를 지원한다.
- 필요로 하는 양자화 기법은 int8 보다 더 적은 bit 수를 사용하는 것이다.
- 이를 제작하기 위해서는 custom quantization 기법을 사용하여야 한다.
- 따라서 PTQ를 custom quantization 하는 방법에 대해 알아보고자 한다.

# 아이디어

- PTQ를 하기 위해서는 우선 weight 의 data 분포를 알면 좋을 것 같다.
- 데이터 전처리를 수행할 때 양 끝 값이 얼마인지 체크해 봐야겠다 &rarr; ~~**pandas 를 통해 분포 확인하기**~~
- 결국에는 **BNB (bitsandbytes)를 통해서** 원하는 방법을 찾았다.
# 수행방법
- hugging face에서 linear 4bit quant 에 대한 자료를 찾았음
https://huggingface.co/docs/bitsandbytes/reference/nn/linear4bit
> 1. PTQ 방식을 선택하였으므로, 우선 모델을 학습시킨다.
> 2. 학습한 모델의 parameter를 양자화 하는 모델로 옮긴다. 
> 	load_state_dict(torch.load(parameter 위치))
> 3. 해당 모델을 device에 올린다. model.to(device)
> 4. 이후 속도 및 정확도를 체크

# 결과
MNIST 라서 그런지 생각보다 더더욱 정확도 감소율이 낮았다.

## NF4 

![image](https://github.com/user-attachments/assets/cd007179-88fd-47ad-8274-6fa94384fe7a)

## FP4
![image](https://github.com/user-attachments/assets/1987a51e-3e8b-47ee-8af6-e4f742a70759)

## datafile 용량 차이



![image](https://github.com/user-attachments/assets/31b93243-d840-40b5-994d-7a8e079b665a)

# 결론
- 생각보다 더더욱 차이가 적어서 놀랐다. FC Layer라서 그런 것 같다.
- 이제 4bit MAC 연산기의 linearity 만 맞추면 된다.
- 근데 이제 그걸 어떻게 Layer 로 넣는 지는 더 고민해봐야 겠다.