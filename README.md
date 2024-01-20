# TAVE-Image_Captioning
TAVE 12기 딥러닝 심화프로젝트

---

## 1. 배경 & 목적

---

- 대회명: 신한AI, 보다 나은 금융 생활을 위한 AI 서비스 아이디어 경진대회
- 프로젝트명 : NLP를 활용한 산업분석 기반 다이렉트 인덱싱
- 목적 : 자연어처리를 활용해서 유망한 산업군에 투자할 수 있는 개인 맞춤형 포트폴리오 제작

## 2. 주최/주관 & 참가 대상 & 성과

---

- 주최: 신한AI
- 주관: 데이콘
- 참가대상 : 국내 거주자로 참가팀(5인 이내)구성
- 평가지표 : 리더보드 및 심사위언 평가
- 성과: 14등 / 67등(상위 20%)

## 3. 대회 기간

---

- 예선-리더보드 평가기간: 2023년 4월 10일~5월 15일
- 본선-오프라인 발표

## 4. 내용

---

자연어처리를 활용해서 산업 분석 기반의 다이렉트 인덱싱을 기획해보았다.

먼저 산업 섹터별로 월별 뉴스기사 본문 데이터를 수집하였다. 데이터 전처리를 진행한 후 뉴스 기사 본문을 바탕으로 감성분석을 진행하였고 이를 바탕으로 산업별 월별 전망지수를 생성하였다.

산업 전망지수를 이용해서 MVO기반 다이렉트 인덱싱을 구현하였고 나만의 포트폴리오를 만들 수 있도록 모바일 어플리케이션으로 UI/UX를 구현해보았다.

## 5. 담당 역할

---

- 뉴스 데이터 수집(API활용 크롤링)
- 뉴스 데이터 전처리(Cleaning, Tokenization, Normaliztion, Stopword Removal)
- 산업별 월별 감성지수 도출
- 그래핑 및 시각화 자료 제작
- 코드 정리

## 6. 데이터 분석 Process

---

### 1. 뉴스 데이터 수집

- 1-1. 검색어 입력 및 API 불러오기
- 1-2. 검색 결과에서 실제 뉴스 가져오기
- 1-3 뉴스 본문 가져오기
- 1-4 수집한 데이터 dataframe으로 제작

### 2. 데이터 전처리

- 2-1. Cleaning
- 2-2. Tokenization & Pos Tagging
- 2-3. Normalization
- 2-4. Stopword Removal

### 3. 산업 현황 분석 및 산업 감정 지표 도출

- 3.1 WordCloud 및 단어빈도 수를 통한 산업 현황 파악
- 3.2 산업별 월별 감성지수

### 4. 블랙리터만 모델을 활용한 다이렉트 인덱싱

## 7. 증빙자료

---

- PPT

https://docs.google.com/presentation/d/1Ce55AkkZyK6oMZT6ODzvYuLw_O6MOujW/edit?usp=sharing&ouid=109060680601725630686&rtpof=true&sd=true

[NLP를 활용한 산업분석 기반 다이렉트 인덱싱_제출용.pptx](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/720262de-080d-4b3b-bf95-78ced06c9744/NLP%EB%A5%BC_%ED%99%9C%EC%9A%A9%ED%95%9C_%EC%82%B0%EC%97%85%EB%B6%84%EC%84%9D_%EA%B8%B0%EB%B0%98_%EB%8B%A4%EC%9D%B4%EB%A0%89%ED%8A%B8_%EC%9D%B8%EB%8D%B1%EC%8B%B1_%EC%A0%9C%EC%B6%9C%EC%9A%A9.pptx)

- 코드
https://drive.google.com/file/d/1ddDEDc0FqhLGvwuvYpAEPQ27gaD5gEcG/view?usp=sharing

- 데이터
https://drive.google.com/drive/folders/1nBozeSLWxHIGn0cyN9R_sqysh9bh_FJZ?usp=sharing
[Dacon : 2023 Samsung AI Challenge Image Quality Assessment](https://dacon.io/competitions/official/236134/data)


- Github
https://github.com/Gayeon6423/Direct-Indexing-Based-on-Industry-Analysis-Using-NLP
























# Advantage Actor Critic TRADER IN KOSPI 200

## 개요
- 강화학습 에이전트가 수익률을 극대화하는 거래를 할 수 있도록 학습하고 KOSPI 200 종목에서 실전 매매를 진행

## 배경 
- 딥러닝을 이용하여 주식 가격을 예측하는 프로젝트는 일반적으로 시도되었으나, 단순 예측에 기반하기 때문에 투자 의사결정 및 수익률을 극대화하는 주식 매매의 목적을 이루기에 한계가 있음
- 불확실한 환경에서 매매를 해야하는 현실의 문제에 맞도록 에이전트가 수 십만개의 시나리오를 통해 수익률을 극대화할 수 있는 액션을 학습하게하여 수익률을 극대화하고자 함

## 방법론 : Advantage Actor Critic 
- 정책 경사를 활용하여 Policy Network의 액션(Buy, Sell, Hold) 학습
- Critic Network 도입으로 Policy Network가 예측한 action의 가치 측정
- Advantage Term (Q(st,at)- V(st))를 이용하여 Policy, Critic Network 학습
- A2C는 Onpolicy이므로 N개에 대한 Batch 학습을 진행하고 샘플을 재사용하지 않는다
- 보상함수 설계
  - one buy - one sell이 일어날 시 매도 차익에 대한 수익률로 보상 설정 
  - Monte carlo, Target Difference 방식 중 주식 거래 도메인에 더 효과적인 방식 채택

## 개발 방향

### 데이터 및 처리
- KOSPI 200에 해당하는 종목의 지난 10년(2013.01.01~2022.12.31) 일별 데이터를 수집(2023.08.26 기준)
  - 수집 데이터 : 시가, 고가, 저가, 종가, 거래량, 투자자별 거래대금(기관, 개인, 외국인)
- 거래량 및 가격 지표를 생성 및 전처리(클렌징, 변수변환 등)
- 학습기간 동안 사용한 스케일러를 테스트 때 사용하기 위해서 종목별 스케일러 저장

### 환경 구성
- Environment와 state를 구성하기 위한 작업 실시
  - 개별 종목 코드를 부르면 전체 주가 데이터를 불러오는 기능
  - 환경에는 두 가지 데이터 셋이 존재
    - 차트 데이터 : 에이전트가 실거래가로 매매하기 위해 사용 (시가, 저가, 고가, 종가)
    - 학습 데이터 : policy network에 들어가기 위한 데이터 (각종 지표들)
  - 지정한 윈도우 사이즈만큼 개별 state를 호출하고 next state를 불러주는 기능

### 에이전트
- 거래 관련 파라미터
  - 운용자금, 포트폴리오 가치, 평단가, 거래 수수료 등
- 거래 관련 함수 선언
  - Buy, Sell, Hold 등
- Policy Network (Gradient Ascent)
  - loss = -logprob * advantage
- Critic Network (Gradient Descent)
  - loss = (advantage)^2
- Advantage = V(st+1) - V(st) :
  - Q(st,at)를 bellman equation으로 변환 후 state만을 가지고 advantage term을 나타낼 수 있어 연산 효율화 가능

