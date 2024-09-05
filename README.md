## TAVE_12 : Multi-Moadal based Image Captioning

---

## 1. 배경 & 목적

---

- 프로젝트명 : 멀티모달 기반 이미지 캡셔닝
- 목적 : TAVE 12기 딥러닝 심화프로젝트
- 배경 : NLP 모델과 CV 모델을 결합한 Multi Modal 테스크를 수행해보고자 'Image Captioning'을 주제로선정, 데이콘에서 주관하는 '2023 Samsung AI Challenge : Image Quality Assessment' 대회의 데이터를 활용하였으며 리더보드 성능을 높이는 모델을 개발하는 방향으로 프로젝트를 진행하였다.

## 2. 주최/주관 & 참가 대상 & 성과

---

- 주최: 4차산업혁명동아리 TAVE
- 참가대상 : TAVE 학회원
- 평가지표 : 데이콘 리더보드, 운영진 및 동아리원 평가
- 성과: 

## 3. 프로젝트 기간

---

- 프로젝트 기간 : 2023년 11월 18일 ~ 2024년 1월 23일
- 컨퍼런스 발표일 : 2024년 1월 27일

## 4. 내용

---

2023년 8월에 시행되었던 Samsung AI Challenge는 카메라 영상 화질 정량 평가 및 자연어 정성 평가를 동시 생성하는 알고리즘 개발하는 대회이다. 
화질 평가 기준에는 모두가 동의하는 절대적인 기준이 없기 때문에 이미지를 입력 받으면 이미지의 선명도, 노이즈, 색감 등의 인지화질적인 요소를 종합적으로 고려하여 ‘temperature, tint, sharpness’와 같은 자연어로 화질을 표현하는 ‘이미지 캡셔닝’ 테스크를 수행한다.


## 5. 담당 역할

---

- 정가연 : 팀장, MultiModal 모델 정리, NLP 모델 탐색 및 고도화, MultiModal 모델 정리, 베이스라인 코드 구축
- 박자영 : MultiModal 모델 정리, CV 모델 탐색 및 고도화, 서버 코드 구축
- 이인훈 : MultiModal 모델 정리, CV 모델 탐색 및 고도화, 데이터셋 업로드 
- 박상준 : MultiModal 모델 정리, CV 모델 탐색 및 고도화, 데이터셋 업로드, 병렬화
 

## 6. 프로젝트 구성

---
### 이미지 캡셔닝이란?
- 멀티 모달 개념
- 이미지 캡셔닝 개념
- 이미지 캡셔닝 모델 종류
  - ExpansionNet
  - Flamingo
  - CLIP

### 방법론
- 데이터 소개

- 모델 선정 배경
  - Basic Code 모델 분석
  - ResNet, MobileNet, GRU, LSTM 결합 모델 

- 모델 아키텍쳐

- 손실 함수 및 평가 지표

### 모델 학습
- 데이터 전처리
- 모델 학습 과정

### 분석 결과 및 결론
- 실험 결과
- 의의 및 한계/보완점


## 7. 증빙자료

---

- PPT


- 코드

https://drive.google.com/file/d/1ddDEDc0FqhLGvwuvYpAEPQ27gaD5gEcG/view?usp=sharing

- 데이터

https://drive.google.com/drive/folders/1nBozeSLWxHIGn0cyN9R_sqysh9bh_FJZ?usp=sharing

[Dacon : 2023 Samsung AI Challenge Image Quality Assessment](https://dacon.io/competitions/official/236134/data)
