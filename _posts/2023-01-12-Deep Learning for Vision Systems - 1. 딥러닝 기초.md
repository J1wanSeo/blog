---
title: Deep Learning for Vision Systems - 1. 딥러닝 기초
updated: 2023-01-12 11:32:09Z
created: 2023-01-12 01:51:28Z
tags:
  - data
  - feature
  - image
  - vector
  - 이미지
---

## 1\. Computer Vision

- Visual Perception
    - 카메라를 통해 주변을 인식
- Vision System
    - ex) 사람: 👀 → 🧠
    - Machine Learning
        1.  '개'의 이미지로 학습을 시킴 (Labeled DATA)
        2.  '개'가 아닌 이미지를 제공하여 학습
        3.  학습된 DATA 가 틀렸다는 것을 제공하여 PARAMETER 수정(Training by Trial & Error)
    - Scanning System
    - Interpretation System
        - f(x)를 제작, 이를 뉴런으로 생각한다.
        - 이를 연결하여 딥러닝 수행
        - Newron Based

## 2\. Image Classification

#### Convolution Neural Network

ex) YOLO & SSD Faster R-CNN

> GAN (Genrative Adversaial Network) : 생성적 적대 신경망
> 현재까지는 그림이나 이미지의 영역에만 한계가 있지만 추후 발전될 것이다.

- Face Recognition
    - Face Identification
    - Face Verification

## 3\. Computer Vision Pipeline

#### 전체 처리과정

- Data Input : Image ' Video'..
- Normalization: 이미지 표준화 (색 변환..grayscale)
- 특징 추출 (Feature Vector): 이미지를 구분할 수 있는 특징 찾기
- 머신 러닝 모델: 특징을 학습하여 대상을 예측 분류..

> **정확도를 높이기 위해서 각 구간을 반복하거나 최적화를 해야한다.**

## 4\. Image Input

- 함수로 나타낸 이미지 ( greyscale )
    - F(x, y) = x , y 좌표의 빛의 밝기
    - 컴퓨터 입장에서의 이미지
        - Pixel 에 담기는 숫자\[F(x, y)\] 들의 Matrix
    - Color Image
        - 행렬을 3개를 이용하여 RGB를 사용하여 표현한다

## 5\. 이미지 전처리

- 컬러 이미지를 회색조(greyscale) 이미지로 변환한다
    *처리를 요하는 픽셀의 수를 줄인다 ( Matrix 를 1개로 감소시킴)*
    - 이미지 표준화 : Data Image를 CNN이 요구하는 크기로 Resize
    - 데이터 강화 : 주어진 Data를 조금씩 변화시켜 학습 데이터로서 동작하게 함
    - Extra: 배경색을 제거

## 6\. 특징 추출 (Feature Extraction)

- Original Data로 부터 Feature Vector를 추출하여 특성을 학습하게 한다.
    
- What's good feature Vector?
    
    - Feature should be easily classificated.
    
    > P.O. Using Pandas / Python would be essentiable
    
    - Tracking and Compartion should be easily practiced
    - Shouldn't be effected by Ratio, Brightness, viewpoint.
    - Could be found by part of object
- How to get Feature Vectors
    
    - Manually ( SVM , AdaBoost )
        
        - 기울기 방향성 히스토그램
        - [Haar Cascade](http://www.gisdeveloper.co.kr/?p=7208)
        - 크기 불변 특정 변환
        - 고속 강인한 특징 추출
    - Automatically ( Deep Learning )
        
        - Original Image → Newron Web → Pass
        
        > automatically extract feature vectors by recognizing the patterns
        > **give the points by featuring every parts of Data**
        

## 7\. Classification Algorithms

- Image input → Image normalization → Extract Feature
    
- CNN: Deep Learning Algorithm
    
    - Extract Features automatically + predict labels
    
    > as many as newron floors exists, easily get many feature vectors