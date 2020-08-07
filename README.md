# 암 이미지 분류 프로젝트
## 프로젝트 소개
- 600개의 암 이미지 데이터 분류 인식률 높이기 프로젝트입니다.
- 이미지 분류에 많이 쓰이는 딥러닝 기술인 CNN을 이용했습니다.

## 개발환경
- MATLAB에 있는 AlexNet, GoogLeNet, ResNet50 등 toolbox를 사용했습니다.

## 왜 CNN(Convolutional Neural Network)을 사용했는지
- CNN은 이미지 인식과 패턴 감지를 위한 최적의 아키텍쳐를 제공합니다.
- 특징을 직접 학습하기 때문에 특징을 수동으로 추출해야 할 필요가 없습니다. 

## 인식률 높이기
- CNN 모델을 그대로 사용
- Fully Connected Layer 중 특정 Layer를 선택해 활성화해서 나온 feature들을 합쳐 분류
> 예시)
```
layer = 'fc7';
featuresTrain = activations(net,augimdsTrain,layer,'OutputAs','rows');
featuresTest  = activations(net,augimdsTest, layer,'OutputAs','rows');
```
> AlexNet의 레이어를 보면 Fully Connected Layer가 fc6, fc7, fc8이 존재합니다.
이 중 'fc7' 계층의 특징 표현을 갖고 온 것입니다.
- CNN 모델을 섞어 사용
> 예시)
```
net1 = alexnet;
net2 = resnet50;
(생략)
featuresTrain1 = activations(net1,augimdsTrain,layer1,'OutputAs','rows');
featuresTest1  = activations(net1,augimdsTest, layer1,'OutputAs','rows');
featuresTrain2 = activations(net2,augimdsTrain,layer2,'OutputAs','rows');
featuresTest2  = activations(net2,augimdsTest, layer2,'OutputAs','rows');
featuresTrain = [featuresTrain1 featuresTrain2];
featuresTest = [featuresTest1 featuresTest2];
```

## 결과
- 70%였던 인식률을 92.8%로 높였습니다.
- 프로젝트를 제안했던 곳에서 준 테스트를 통과해 5000개의 암 이미지 데이터 분류 사용 허가를 받았습니다.
