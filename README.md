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

- 프로젝트 기간 : 2023년 11월 18일 ~ 2024년 1월월 23일
- 컨퍼런스 발표일 : 2024년 1월 27일

## 4. 내용

---

2023년 8월에 시행되었던 Samsung AI Challenge는 카메라 영상 화질 정량 평가 및 자연어 정성 평가를 동시 생성하는 알고리즘 개발하는 대회를 기반으로 프로젝트를 진행한다.
화질 평가 기준에는 모두가 동의하는 절대적인 기준이 없기 때문에 이미지를 입력 받으면 이미지의 선명도, 노이즈, 색감 등의 인지화질적인 요소를 종합적으로 고려하여 ‘temperature, tint, sharpness’와 같은 자연어로 화질을 표현하는 ‘이미지 캡셔닝’ 테스크를 수행한다.


## 5. 담당 역할

---

- 정가연 : 팀장, MultiModal 모델 정리, NLP 모델 탐색 및 고도화, 베이스라인 코드 구축
- 박자영 : MultiModal 모델 정리, CV 모델 탐색 및 고도화, 서버 코드 구축
- 이인훈 : MultiModal 모델 정리, CV 모델 탐색 및 고도화, 데이터셋 업로드 
- 박상준 : MultiModal 모델 정리, CV 모델 탐색 및 고도화, 데이터셋 업로드, 병렬화
 

## 6. 프로젝트 구성

---

### 6-1. Introduction
[주제 선정 배경]
- CV 스터디원과 NLP스터디원이 모인 팀으로 딥러닝 분야에서 각광받고 있는 멀티 모달을 활용한 프로젝트를 진행하게 되었다.

[대회 설명]
- 대회명 : 2023 Samsung AI Challenge : Image Quality Assessment
- 주제 : 화질 평가 및 이미지 캡셔닝
- 설명 : 카메라 영상 화질 정량 평가 및 자연어 정성 평가를 동시에 생성하는 알고리즘 개발 대회

![대회](https://github.com/Gayeon6423/TAVE-Image_Captioning/assets/113704015/7fa89342-49fa-4a1d-b983-d15b4a72f0a8)

[Dacon : 2023 Samsung AI Challenge Image Quality Assessment](https://dacon.io/competitions/official/236134/data)


[데이터 소개]
- Train Data는 74,568개의 이미지, Test Data는 13,012개의 이미지로 구성되어 있다. 각 csv파일 형식의 데이터는 이미지 파일명, 이미지 경로, 화질 평가 점수, 캡셔닝 칼럼으로 이루어 진다.

![이미지캡셔닝](https://github.com/Gayeon6423/TAVE-Image_Captioning/assets/113704015/07d18872-d7a5-402d-9d07-ef9d173de243)

[멀티 모달 개념]
- 멀티 모달 : 서로 다른 특성을 갖는 데이터 타입들을 함께 사용하는 학습법

[이미지 캡셔닝 개념]
- 이미지 캡셔닝 : 주어진 이미지에 대한 캡션을 예측하고 생성해내는 작업

 
### 6-2. Methodology
- ResNet : Residual Block 구조가 쌓여 만들어진 모델, overfitting, gradient vanishing 문제를 해결하여 성능을 향상시킴
- MobileNet : Depthwise Separable Convolution 이용하며 연산량이 크게 늘지 않으면서 성능 개선한 모델, 모바일과 같은 작은 규모에서도 사용이 용이함
- GoogLeNet : Inception Module(1x1 Convolution 활용)을 통한 연산량 감소 및 성능 개선한 모델.
- LSTM : 기존 RNN 모델에 cell-state가 추가된 구조, 3개의 Gate를 통해 메모리 값을 균일하게 유지하면서 꼭 필요한 만큼의 정보를 기억하는 모델
- GRU : LSTM의 단점을 개선한 모델로 두 개의 Gate로 효율적 계산가능, 빠른 학습, 낮은 계산 복잡성 가짐
- Drop-out : Regularization의 일종으로 Layer에서 각각 독립적인 unit을 일정 비율에 맞춰 삭제하는 기법
- Data parallelism : 다수의 GPU를 병렬적으로 활용하는 기법 학습 속도 개선 효과를 가짐


### 6-3. Data Preprocessing
[Color to Black & White]
- 모델 경량화를 위해 컬러 이미지를 흑백 이미지로 변환 => 학습 시간 단축 X, 성능 하락 => 사용 X
[Image Size]
- 이미지 사이즈 224 -> 이미지 사이즈 128 => 학습 시간 단축 O, 성능 유지 => 사용 O


### 6-4. Model Train
[Train Model] 
- CNN : MobileNet, GoogLeNet
- RNN : GRU

[Hyper Parameter] 
- Learning rate = 0.01, Epochs = 10, Batch Size = 32, 64


### 6-5. Results & Discussion
[모델 성능]
- ResNet + LSTM 조합과 MobileNet + GRU 조합의 성능이 우수하게 나옴
- MobileNet + GRU 조합의 성능과 학습 시간이 모두 우수하게 나왔으므로 최종 모델로 선택

![소요시간](https://github.com/Gayeon6423/TAVE-Image_Captioning/assets/113704015/33d61cd2-3024-4294-ac48-393c564f035c)


[한계점 및 개선 방향]
- GPU 자원의 한계 => 모델 이분화를 통하여 경량화 개선 예정
- 모델의 성능보다 경량화에 비중을 맞춘 진행 => 다양한 모델을 찾고 파라미터 조정 진행하며 개선 예정

[의의]
- 팀원들 모두 멀티모달의 개념 조차 알지 못했지만 프로젝트를 진행하며 이론 공부에 더해서 직접 구현까지 해봤다는데 의의를 둠
- NLP 모델과 CV 모델을 공부해볼 수 있었고 이미지 캡셔닝 테스크에 대한 전반적인 과정을 배울 수 있었음


## 7. 자료
---

- PPT


- 코드
  
https://colab.research.google.com/drive/14V5WdyTV5MTc4sSaNaVgcXvQLNCrqnX3?usp=sharing

https://colab.research.google.com/drive/11KBrkSVJRr8Wn71_vgIz6W4OILWggK_6?usp=sharing

https://colab.research.google.com/drive/1ADIa3AYd2kcd32qszzf6otRmbUjvb7p4?usp=sharing

- 데이터

https://drive.google.com/drive/folders/1nBozeSLWxHIGn0cyN9R_sqysh9bh_FJZ?usp=sharing



## 8. 프로젝트 소감

---


| 이름 | 소감 |
| --- | --- |
| 정가연 | 안녕하세요 TAVE 12기 정가연입니다. 저희 팀은 멀티모달 기반 이미지 캡셔닝 프로젝트를 진행했습니다. 프로젝트를 진행하며 두가지 이종 데이터(텍스트, 이미지)를 활용하는 멀티 모달에 대해 배울 수 있었고 NLP 모델과 CV모델에 대해서도 탐색해 볼 수 있어서 좋았습니다. 직접 논문을 읽고 코드를 구현해보며 딥러닝 분야에 대한 이해의 폭이 넓어질 수 있었던 좋은 프로젝트였다고 생각합니다. 자영이, 상준 오빠, 인훈 오빠 모두 너무 좋은 팀원이였고 어려운 주제 임에도 모두들 매주 열정적으로 참여해준 덕분에 많은 것을 배울 수 있었습니다. 프로젝트 기간 동안 고생하셨고 감사했습니다 :D |
| 이인훈 | 안녕하세요. TAVE 12기 이인훈입니다. 후반기에는 전반기에 스터디로 진행했던 ‘컴퓨터 비전’을 바탕으로 ‘NLP’를 더해 ‘Multi Modal’을 구현하는 프로젝트를 진행하였습니다. 처음 스터디를 진행할 때는 딥러닝이 익숙하지 않아 조금은 어색한 모습이었다면 프로젝트는 스터디 때보다 약간 더 넓은 이해력을 바탕으로 성장한 모습으로 임할 수 있었습니다. 팀의 방향성이 목표를 향할 수 있도록 충분한 도움과 실력이 되지 못하여 아쉬운 마음입니다. ㅠㅠ |
| 박상준 | 안녕하세요! TAVE 12기 박상준입니다. 저희 팀은 전반기에 컴퓨터 비전 스터디를 했던 팀원들과 NLP 스터디를 했던 팀원으로 구성되어 비전과 NLP를 더해 멀티모달을 구현해보는 프로젝트를 진행했습니다. 프로젝트를 시작하기 전만 해도 멀티모달에 대해 막연한 생각이었지만 프로젝트가 진행됨에 따라 팀원들과 함께 ‘멀티모달’에 대해 공부해보고 새로운 모델들에 대한 논문들도 읽어보고, 무지했던 NLP 분야에 대해서도 공부해보면서 많이 성장한 시간이었던 것 같습니다. 특히나, 향후에 이미지 센서 분야를 더욱 공부해 나가고 싶은데 그와 관련한 컴퓨터 비전 스터디를 팀원들과 했던 것, 그리고 이번 프로젝트를 통해 이미지 캡셔닝에 대해 많이 배울 수 있어서 미래에 한발짝 더 가까이 다가갔던 것도 같습니다. 다만, 인공지능 전공자가 아니어서 그런지, 딥러닝에 대한 이해가 아직은 부족해서 그런지, 스스로가 조금은 부족했던 모습들도 있어서 팀원들에게 미안하고 고마운 마음도 큽니다. 프로젝트 기간동안 모두들 정말 고생 많았고 감사했습니다! | 
| 박자영 | 안녕하세요! TAVE 12기 박자영입니다. 저희는 많은 사람들이 관심을 가지고 있는 주제인 ‘Multi Modal’을 활용한 프로젝트를 진행했습니다. 상반기에 CV 스터디를 진행하면서 익혔던 여러 기법들을 적용해봄과 동시에 새로운 분야인 NLP에 대해서도 경험해볼 수 있었던 아주 귀중한 시간이었습니다. 여러 사람들이 여러 가지를 ‘찍먹' 하기보다는 한 가지 분야에 집중하여 전문가가 되라고 말합니다. 저도 이번 프로젝트를 토대로 ‘Multi Modal’ 기반 Image Captioning 을 마스터하고, 그 과정에서 CV, NLP 중 더 공부하고 싶은 분야를 선택하여 제대로 익혀보고자 합니다. 짧지 않은 시간동안 팀원들과 함께하면서 새로운 목표를 설정할 수 있어 정말 좋았습니다. 가연님, 상준님, 인훈님 모두 함께해서 행복했고 감사했습니다:-) 모두 앞으로도 더욱 성장하는 테이비가 될 수 있길! |
