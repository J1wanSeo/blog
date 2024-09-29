---
title: PyTorch + PIM AI 가속기 설계 아이디어 및 제안배경
layout: post
updated: 2024-09-29 06:01:26Z
created: 2024-09-09 04:55:36Z

tags:
  - [ AI, SoC ]

toc: true
toc_sticky: true
latitude: 37.56653500
longitude: 126.97796920
altitude: 0.0000
---

# 제안 배경

![image](https://github.com/user-attachments/assets/593cff63-fc24-4ba9-aebc-51df14164f26)

딥 러닝 증가와 함께 데이터 서버의 사용량 또한 증가되고 있다.  
데이터 서버 증가에 따른 과도한 전력 소모는 전지구적 논쟁거리로 대두되고 있다.  
특히 ESG 경영이 중점적으로 다루어지는 현대 사회에서, 가치 창출을 위한 무변별한 전력 소비는 시대에 뒤쳐지고 있다는 관점이다.

따라서 우리는 해당 문제점을 해결할 수 있는 방법으로 MAC 연산을 HW로 대체하고 이를 통해 전력소비와 속도 두마리 토끼를 모두 달성하고자 한다.  

하기 그래프를 참조해 보면 기존의 SW 로 MNIST 추론을 수행한 결과와 이를 HW로 변환하여 수행하였을 때를 비교하고 있다.

![image](https://github.com/user-attachments/assets/9169eeea-e6e5-48f8-8caf-e2e6d21ffd4b) 

따라서 데이터 서버 내 연산용 기기들의 HW 설계를 통해 전력소모를 줄이고 이를 통해 현시대의 문제점 해결로 나아갈 수 있다.

# 계획

1.  Pytorch를 이용해서 간단한 DNN 을 제작하고 이의 정확도를 확인한다.
2.  해당 구조 내에 존재하는 conv2d를 우리가 가지고 있는 3bit mac 연산기에 배치하여 사용하자
3.  그렇다면 MAC 연산기는 몇 bit로 제작하는 것이 좋을까 고민이다.
4.  이 때 MAC 연산기의 bit 수를 결정하기 위해 quantization을 사용한다.
5.  quantization으로 발생하는 data loss에 의한 정확도 감소율을 먼저 확인하고 bit를 결정하자

Quantization 방법의 선택에서 고민

- 구조 내에 존재하는 layer가 특정 비트의 연산을 수행해야한다.
- 학습 후 동적 양자화를 수행해야 할 것 ( 함수들이 다 양자화된 애들로 계산 )
- 그렇다면 양자화된 네트워크의 일부분을 회로로 대체할 때 어떤 파트를 할 것인가?
    - ex) nn.Linear, nn.conv2d 를 바꾸어야 되는데 이를 회로로 모델링 할 수 있는가?
        - 세부 구조 중에서 계산하는 부분만을 바꾸어야 되나?