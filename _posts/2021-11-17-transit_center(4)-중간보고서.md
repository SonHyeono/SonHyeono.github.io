---
title: "Efforts to find a transit center(4)-중간 보고서"
layout: post
date: 2021-11-17 22:41:00 +0900
category: Intern
---

#### 현재 상황

- Palantir Foundry가 주제였던 산학 R&D였지만, 회사에서 국방부 사이버 보안 사업을 못따내자, 우리 팀에게 서울시 새로운 환승센터의 적격지를 찾는 일을 맡겼습니다.
- [서울시 시민들의 버스 데이터](https://topis.seoul.go.kr/refRoom/openRefRoom_3_4.do)를 이용해서 서울시 대중교통 버스 승객, 노선, 지하철 환승등을 분석후, 서울시내 대형 환승Hub센타를 어느곳, 몇군데 만들면 가장 여객이 덜혼잡하고, 여행시간과 환승횟수가 최소가 되고, 만족도가 높은지를? 정책안 제시하는 일을 맡았습니다.

---

#### 중간 보고서

- [Chapter 1](#chapter1) 2021년 버스와 지하철 승하차 승객수 Top 20

  - [Section 1.1](#section_1_1) 버스 승하차 Top 20 정류장
  - [Section 1.2](#section_1_2) 지하철 승하차 Top 20 역

- [Chapter 2](#chapter2) 버스와 지하철 승객수 Top 20 & 39 시각화

  - [Section 2.1](#section_2_1) 버스와 지하철 승하차 Top 20
  - [Section 2.2](#section_2_2) 버스와 지하철 승하차 Top 39

- [Chapter 3](#chapter3) 기존 환승센터 & 새로운 환승센터 후보지
  - [Section 3.1](#section_3_1) 기존 환승센터
  - [Section 3.2](#section_3_2) 새로운 환승센터 후보지
  - [Section 3.3](#section_3_3)
- [Chapter 4](#chapter4) 후보지 평가 및 Cost 점수 정하기
  - [Section 4.1](#section_4_1) 후보지 평가
  - [Section 4.2](#section_4_2) Cost의 점수 정하기
- [Chapter 5](#chapter5) Task

---

##### Chapter 1 <a class="anchor" id="chapter1"></a> : 2021년 버스와 지하철 승하차 승객수 Top 20

##### Section 1.1 <a class="anchor" id="section_1_1"></a> 버스 승하차 Top 20 정류장

- transit_center(3)까지 해서 1월부터 ~ 9월까지 버스의 평일 승하차 승객수 top 39를 뽑아 냈고, 다른 팀원이 1월부터 10월까지의 지하철 top 39개의 데이터를 뽑아 냈습니다.

![bus_on](https://user-images.githubusercontent.com/26592315/142203811-dba6f022-5f26-4fc4-b4c0-8d834de83847.png){:width="100%" height="100%"}{: .center}

![bus_off](https://user-images.githubusercontent.com/26592315/142203821-2c776e7a-4d61-45a6-91ca-240334736e03.png){:width="100%" height="100%"}{: .center}

##### Section 1.2 <a class="anchor" id="section_1_2"></a> 자하철 승하차 Top 20 역

![sub_on](https://user-images.githubusercontent.com/26592315/142203851-ae41aee4-c850-4baf-bc8d-74142bf99f00.png){:width="100%" height="100%"}{: .center}

![sub_off](https://user-images.githubusercontent.com/26592315/142203866-a5626e8b-21ef-4d73-b8e1-3a3806af200e.png){:width="100%" height="100%"}{: .center}

---

##### Chapter 2 <a class="anchor" id="chapter2"></a> 버스와 지하철 승객수 Top 20 & 39 시각화

##### Section 2.1 <a class="anchor" id="section_2_1"></a> 버스와 지하철 승하차 Top 20

![top20지도](https://user-images.githubusercontent.com/26592315/142205422-2bec902e-7632-4713-b68d-44ebe26197f1.png){:width="100%" height="100%"}{: .center}

##### Section 2.2 <a class="anchor" id="section_2_2"></a> 버스와 지하철 승하차 Top 39

![top39지도](https://user-images.githubusercontent.com/26592315/142205434-4976e0ca-25b3-4e2c-b897-be3554eeb429.png){:width="100%" height="100%"}{: .center}

---

##### Chapter 3 <a class="anchor" id="chapter3"></a> 기존 환승센터 & 새로운 환승센터 후보지

##### Section 3.1 <a class="anchor" id="section_3_1"></a> 기존 환승센터

![transit_origi](https://user-images.githubusercontent.com/26592315/142205440-b3027e60-7c8a-4ca2-b812-cb53b7c02f2a.png){:width="100%" height="100%"}{: .center}

##### Section 3.2 <a class="anchor" id="section_3_2"></a> 새로운 환승센터 후보지

![transit1](https://user-images.githubusercontent.com/26592315/142205453-9e3b5075-b024-429f-8bc7-5c9c27f9db8f.png){:width="100%" height="100%"}{: .center}

![transit2](https://user-images.githubusercontent.com/26592315/142205456-7b021115-1170-4742-a355-9800a6ba519f.png){:width="100%" height="100%"}{: .center}

---

##### Chapter 4 <a class="anchor" id="chapter4"></a> 후보지 평가 및 Cost 점수 정하기

##### Section 4.1 <a class="anchor" id="section_4_1"></a> 후보지 평가

- 버스와 지하철 데이터를 이용해서 승하차 승객수 Top9곳을 새로운 환승센터 후보지로 선정을 하였습니다.(기존 환승센터의 버스 정류장과 지하철역은 제외)

- 서울역을 중심으로 시계방향으로
  > - 미아사거리
  > - 수유
  > - 쌍문
  > - 고속버스터미널
  > - 서울대입구역
  > - 신림
  > - 신도림
  > - 합정
  > - 홍대입구

---

##### 후보지 평가 (후보지를 3개로 분할해서 평가)

1. 미아사거리 , 수유 , 쌍문

> - **길음과 창동에 환승주차장 有 (미아사거리-길음, 쌍문-창동)**
> - 미아사거리와 수유, 쌍문이 한 도로 상에 이어져 있음.
> - 단점: 북한산이 서쪽에 있어서 위치적으로 고립( 그러나 위정부시 발전할 경우 환승센터로서의 역할이 극대화 )

---

2. 고속버스터미널, 서울대입구, 신림, 신도림

> - 고속버스터미널의 경우는 강남(기존환승센터, 2023예정)과 지리적으로 가깝고 환승의 개념보다 유입과 반출이 많음. 즉, **환승하려고 모이는 것이 아니라 외부(서울시X)로 벗어나기 위해 모임.**
> - 서울대입구와 신림의 경우는 남부순환로로 이어져 있고 **이곳의 교통량이 많아서 환승센터로 하면 더욱 복잡해질 가능성 농후.**
> - 신도림의 경우는 지리적으로 **환승센터 2곳**(여의도 환승센터와 구로디지털 단지 환승센터)과 바로 연결되어있음.

---

3. 합정 , 홍대입구

> - 합정의 경우는 지리적으로 양화대교랑 가까워서 환승센터로서의 이점이 낮아질 가능성이 있음.
> - 홍대입구의 경우는 지리적으로 **서울역(기존 환승센터)** 이랑 가까움.

---

---

##### Section 4.2 <a class="anchor" id="section_4_2"></a> Cost 점수 정하기

New 환승센터를 정하기 위해서 점수를 부여해서 결정하는 방식으로 하기로 함.(부여 점수는 수정할 수 있음.)

- 환승 편의를 위해 교통수단간 점수부여, 후보지 주변: 버스 정류장 1점, 지하철 1점

- 체계적인 노선을 위한 후보지 근처 주변 노선 개수 당: 0
- 대중교통 활성화를 위한 공간여부, 도로의 차선마다 0.1점
- 최소환승을 위해서는 해당 후보지에 지나는 노선들이 속한 구(강남구, 구로구..)들의 개수가 많을 수록 점수
- 교통량(이거는 고민중)

---

##### Chapter 5 <a class="anchor" id="chapter5"></a> Task

새로운 환승센터의 적격지를 위해 기준을 더 고민 해보고 점수를 매겨서 후보지에서 적격지를 골라보기.
