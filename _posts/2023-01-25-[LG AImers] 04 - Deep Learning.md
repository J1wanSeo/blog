---
title: '[LG AImers] 04 - Deep Learning'
layout: post
date: 2023-01-25 09:59:55Z
created: 2023-01-18 13:50:12Z
categories: DNN
latitude: 37.56653500
longitude: 126.97796920
altitude: 0.0000
---

# Perceptron and Neural Networks

## Perceptron

: 인간의 Neuron을 본따 만든 구조 (선형 분류를 기반으로 한다)

### Single Layer Perceptron

- Hard thresholding function을 통해 표현한다.
- Linear 하게 구분 가능한 것들
- ex) AND / OR ..

### Multi Layer Perceptron

- Linear 하게 구분할 수 없는 것들
- ex) XOR

## Hidden Layer

- Input Layer 와 Output Layer을 제외한 신경망을 구성하는 다른 Layer

# Foward Propagation

: Neural Network의 진행방향대로 진행하는 것

## Linear Layer (a.k.a Fully-Connected Layer)

Neural Network의 Perceptron들

# Softmax Layer (Softmax Classifier)

배경: Sigmoid Output 과 MSE 의 문제점에서 출발
→ 학습이 느려지는 문제가 발생

## 방법

음수의 값을 특정 함수를 통해 양수화 한 뒤, 그 값의 상대적 비율을 계산한다.

## Softmax Loss ( Cross Entropy Loss )

softmax filter를 통해 나온 값이 1에 가까우면 가까울수록 L ↓

## Logistic Regression as a Special Case ?

# Training Neural Networks

## BackPropagation to Compute Gradient Descent

Computing 의 연산를 반대방향으로 진행하여 값을 구하는 것

## problem of using sigmoid

back propagation이 진핼될 때 gradient가 점점 작아져 나중에는 거의 변화가 없게 된다.

## alternative of sigmoid

### Tanh Activation

- zero -centered
- 여전히 사라지는 문제가 발생한다.

### ReLU

- 양수일 땐 그대로, 0보다 작을 땐 0
- 0보다 작다고 하더라도 gradient가 0인 것은 아니지만 이를 사용하면 그렇게 간주하게 된다.

# Batch Normalization

학습을 용이하게 하기 위한 과정
Activation Function들의 실효적인 부분에서만 사용할 수 있도록 training dataset 을 Gaussian을 적용하여 Normalization하여 그 부분에만 할당.

## problem

결과값에서 normalize 된 내용을 원하는 것이 아니므로 원상복구 해주는 과정이 필요하다.

# Convolutional Neural Networks & Image Classification

- 2012년 AlexNet등장 이후 비약적인 발전을 함.
- 2015년 이후 사람보다 더 정확한 판정을 내리고 있음

## How computers see

- Image를 픽셀별로 구분하여 각각의 구분사각형이 filter 와 얼마나 유사한지를 통해 판별
- 같다면 1 다르면 -1 을 Matrix에 저장한다
- 값을 모두 더한 뒤 구분사각형의 사이즈로 나누어 저장한다.

## Convolution Layer

- Channel = Depth : Layer 를 몇개의 층으로 할 것인지 일반적으로 3 (RGB)
- Activation Map : filter를 거친 값들을 저장하는 공간

## Pooling

- Activation Map에서 새로운 개념의 filter를 적용하여 가장 큰 값만 추출

## ReLUs (Rectified Linear Units)

- Activation Map의 값에 ReLU를 적용하여 저장

## Feature Extraction

이미지에서 filter에서 중요하다고 생각되는 부분을 추출

## Fully Connected Layer

축약된 Matrix의 값들을 한줄짜리 벡터로 변환한다.
feature value들의 값을 통해 어떤 것인지 구분하는 것

# Advanced CNN Architectures

## VGGNet

- Using small convolution filters & deep Layers

## ResNet

- Convolution 된 이미지에 입력을 한번 더 더하여 Layer을 추가함
- H(x)가 x가 되게끔 하여 학습을 용이하게 하는 것이 목표임

# Seq2Seq with Attention for NLP

# Recurrent Neural Network

- sequence Data에 특화된 것
- 같은 함수를 여러번 반복하는 것 (재귀의 방식)

## Problems

- one to many : 사진을 설명하는 내용 추출하기
- many to one : 설명을 통해 사진 찾기 / 문장의 감정을 추출하는 것
- many to many: 기계번역 / 언어를 번역하는 것

# Character - Level Language Model

- 다음에 나올 단어를 찾아내는 것

## How to solve gradient vanishing problem?

(Softmax 함수를 사용하므로 gradient vanishing problem 발생)

## LSTM (Long Short-Term Memory)

- Memorize the data that induced fore-step
- Choosing data from memory that would be used

# Seq2Seq and Attention Model

## 배경

- NLP 에서 주로 사용됨
- Encoder 와 Decoder 를 포함하고 있음
- Encoder를 사용하기 때문에 입력 Vector의 사이즈가 크다면 학습이 어렵거나 유실될 수 있음

## Attention

- Encoder 에서 문장 안에서 중요한 내용이 무엇인지 decoder의 이전 내용을 이용하여 판단하여 softmax filter로 제공하고 결과를 도출
- encoder의 단어들 사이의 관계를 미리 파악하여 사용하는 것임

# Transformer

- Attention 모듈 만을 사용하는 방식 ( RNN / CNN 사용 X )
- RNN에서는 시점을 기준 ( 하나를 통과하고 다음 것을 통과하여 데이터를 정리) 였지만 여기선 아니다.

>  - Data를 병렬적으로 전달하므로 문장 Data들의 위치를 모르므로 Postioning Vector와 같이 정보를 제공해야 한다.
>  - RNN의 역할을 Encoder 와 Decoder를 거치며 진행하는 방식
>  - Decoder가 사실상의 RNN 역할, 결과를 도출 할 때 Encoder에 Naive하게 입력된 값을 이용한다는 점
>  - 결과를 도출하고 전체 결과에서 그 내용이 얼마나 영향을 미치는 지 확인
>  **Q** : 그렇다면 Transformer이나 Attention모델 에서도 Decoder의 연산이 끝날 때 까지 시간을 기다려야 하는가?

# Self-Supervised Learning
## BERT
- Bidirectional Transformers = Encoder
## Pre-training of BERT
### MLM (Masked Language Model)
- 내용의 일부를 가리고 학습시키는 것
### NSP (Next Sentence Prediction)
- 문장의 순서를 미리 예측하는 것
## GPT
- Generative Pre-Training Task (a.k.a Languager Modeling)