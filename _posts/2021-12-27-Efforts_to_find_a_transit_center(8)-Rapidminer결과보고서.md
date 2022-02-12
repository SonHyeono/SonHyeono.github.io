---
title: "Efforts to find a transit center(8)-Rapidminer결과보고서"
categories:
  - Intern
feature_text: |
  The History of the 산학 R&D 프로젝트 인턴
---

##### Rapidminer를 이용해서 분석하기

- [Chapter 1](#chapter1) RapidMiner 기반 입지 도출 과정

  - [Section 1.1](#section_1_1) 1단계: Top 39 환승센터 후보지 선정
  - [Section 1.2](#section_1_2) 2단계: RapidMiner Extension Operator 개발 및 변수기반 최종입지 선정

- [Chapter 2](#chapter2) RapidMiner New Operator 개발(6개)

  - [Section 2.1](#section_2_1) Extraction Text Operator
  - [Section 2.2](#section_2_2) How Many In Circle Operator
  - [Section 2.3](#section_2_3) Specific MyOperator
  - [Section 2.4](#section_2_4) Distance Metric Operator
  - [Section 2.5](#section_2_5) Rank Operator
  - [Section 2.6](#section_2_6) Cost Operator

- [Chapter 3](#chapter3) RapidMiner 결론
  - [Section 3.1](#section_3_1) 상용에 없는 Operator를 개발한 후에 RapidMiner로 분석 결론
  - [Section 3.2](#section_3_2) RapidMiner 전체 Process

---

##### Chapter 1 <a class="anchor" id="chapter1"></a> : RapidMiner 기반 입지 도출 과정

##### Section 1.1 <a class="anchor" id="section_1_1"></a> 1단계: Top 39 환승센터 후보지 선정

![image](https://user-images.githubusercontent.com/26592315/148472115-b9baf777-5bb6-414e-b43c-f3bd8f6734db.png){:width="100%" height="100%"}{: .center}

- 서울시에 기존 존재하는 환승 센터의 공통점은 모두 지하철을 중심으로 형성되어 있다는 점이다. 그래서 먼저 지하철의 이용인구 데이터를 이용해서 Top39 데이터 셋을 뽑아냈다. 여기서 기존 환승 센터는 SetMinus Operator를 이용해서 제외했고 Top39 데이터 셋에다가 위치 좌표를 새로운 열로 추가시켰다.

---

##### Section 1.2 <a class="anchor" id="section_1_2"></a> 2단계: RapidMiner Extension Operator 개발 및 변수기반 최종입지 선정

- 8가지 기준을 구하기 위해 상용 RapidMiner 버전에 없는 새로운 Operator 6개를 개발하였다. 총 6개의 Operator를 새로 구현하였고, 이들과 기존 Operator를 이용하여 Top39개의 후보지 별 적합 Cost 함수 프로세스를 구현하였다. RapidMiner를 통한 서울시 환승센터 입지선정에서는 자체 개발한 Operator 6개를 중심으로 분석 프로세스를 구축했다.

---

##### Chapter 2 <a class="anchor" id="chapter2"></a> : 6개의 Operator

##### Section 2.1 <a class="anchor" id="section_2_1"></a> Extraction Text Operator

데이터셋의 특정 컬럼에서 괄호((), {}, [] 등의 소괄호, 중괄호, 대괄호) 안 텍스트를 자동으로 삭제해주는 텍스트마이닝 전처리 Operator이다. Operator 개발 필요성은 다음과 같다.

- 1. 현장에서 생성되는 Raw Data를 정제하고, 여러 데이터셋 간의 원활한 매핑, 조인을 위해

- 2. 수백만개의 Row로 구성된 데이터셋에서의 빠르고 효과적인 텍스트 작업

실제로 개발한 기능은 소괄호/중괄호/대괄호 등 사용자가 입력한 시작문자, 끝 문자 사이의 단어를 모두 제거하는 기능이다. 예를 들어 ‘미아사거리(4호선)’ 텍스트에 대해 ‘미아사거리’를 추출하는 것이다.

사용 방법은 다음과 같이 등록한 데이터셋을 input으로 하여 간단하게 attribute를 선택하고 해당하는 attribute 내의 괄호 안 텍스트를 삭제하는 원리이다.

![image](https://user-images.githubusercontent.com/26592315/148484762-002bf806-7423-496d-b56b-deaef27f6090.png){:width="100%" height="100%"}{: .center}

---

##### Section 2.2 <a class="anchor" id="section_2_2"></a> How Many In Circle Operator

시작점의 좌표와 도착점의 좌표를 입력하고, 기준(km)과 새로운 열의 이름을 정하면 기준 원 안의 개수를 구할 수 있는 Operator이다. 개발 필요성은 다음과 같다.

- 1.  서울시 대중교통 데이터에서 500m 내 정류장과 지하철 역이 몇 개인지 파악하고자
- 2.  좌표 간 거리를 계산하기 위해

RapidMiner 자체 Operator 중 좌표를 이용하여 거리를 구하는 기능은 없고, 기준좌표 중심의 반경에 포함되는 개수를 구하는 기능 역시 존재하지 않는다. 실제로 개발한 기능은 위도와 경도를 기준으로 각각 거리가 얼마나 되는지를 구할 수 있는 역함수인 아크하버사인을 활용해 좌표 간 거리를 구하는 것이다. 해당 오퍼레이터를 통해 Top39 후보지 위치에서 500m 내의 버스 정류장 개수, 지하철 역 개수, 1.5km 내의 환승 주차장 개수 등 3가지 기준을 구할 수 있다.

##### 아크하버사인 공식

<img src="https://latex.codecogs.com/svg.latex?\Large&space; d = r \times archav(h) = 2r \times arcsin(\sqrt{h})" title="\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" />

Operator 개발을 위한 아크하버사인 구현 소스코드는 다음과 같다.

```java
    double R = 6373.0;
    double s_lat = example.getValue(attribute);
    double s_lng = example.getValue(attribute2);
    double e_lat = example1.getValue(attribute3);
    double e_lng = example1.getValue(attribute4);

    s_lat = s_lat * Math.PI / 180.0;
    s_lng = deg2rad(s_lng);
    e_lat = deg2rad(e_lat);
    e_lng = deg2rad(e_lng);

    double d = Math.pow(Math.sin((e_lat - s_lat) / 2), 2) + Math.cos(s_lat) * Math.cos(e_lat) * Math.pow(Math.sin((e_lng - s_lng) / 2), 2);
    double distance = 2 * R * Math.asin(Math.sqrt(d));
```

![image](https://user-images.githubusercontent.com/26592315/148485383-49011615-244e-4460-931a-657a8ee9a6c0.png){:width="100%" height="100%"}{: .center}

##### 지금까지의 프로세스의 결과물

![image](https://user-images.githubusercontent.com/26592315/148633614-6248d645-e3ae-4970-9971-ecde9eb78204.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/148633631-71448637-ee34-447d-a16b-d50cd38e40db.png){:width="100%" height="100%"}{: .center}

---

##### Section 2.3 <a class="anchor" id="section_2_3"></a> Specific MyOperator

How Many In Circle Operator를 이용하면 기준(km)안의 개수를 구할 수는 있지만, 어떤 원소가 포함되는지 그 원소 리스트를 배열로 뽑아낼 수 없으므로 새로운 Operator를 개발했다. 이 Operator의 핵심 원리는 새로운 행의 추가이다. Matrix 형식의 데이터셋에 배열을 삽입할 수 없는 한계점이 있으므로 OS Process에서 착안하여 데이터가 나올 때마다 행을 추가해서 마치 배열이 저장되는 것처럼 구현하였다.

![image](https://user-images.githubusercontent.com/26592315/148633676-222bbb56-55f0-474a-acf8-c82349a01065.png){:width="100%" height="100%"}{: .center}

##### Operator 활용 프로세스

![image](https://user-images.githubusercontent.com/26592315/148633684-e84aa94b-f6fa-49d4-b74c-938a6cdcb17a.png){:width="100%" height="100%"}{: .center}

이러한 과정을 거쳐 환승 센터 후보지의 반경 500m 내에 지나가는 버스 노선의 개수, 후보지를 지나가는 노선의 길이 \* 총 운행횟수, 후보지 이용인구 등을 구했다.

---

##### Section 2.4 <a class="anchor" id="section_2_4"></a> Distance Metric Operator

환승 센터 후보지들과 기존 환승 센터들 과의 거리 합을 계산하기 위해 새로운 Operator를 개발하였다. 출발 좌표와 도착 좌표를 이용하면 거리 계산이 가능하며 거리들의 총합을 구하도록 Operator를 만들었다.

![image](https://user-images.githubusercontent.com/26592315/148633739-53e11810-8c43-4df2-ba84-493a5a98bae1.png){:width="100%" height="100%"}{: .center}

이렇게 4개의 Operator를 추가 개발하여 총 7개의 변수에 해당하는 후보지 값을 도출했다.

![image](https://user-images.githubusercontent.com/26592315/148633763-1f67cdd8-8b52-4a65-8c0c-e89ff6e9670a.png){:width="100%" height="100%"}{: .center}

##### Section 2.5 <a class="anchor" id="section_2_5"></a> Rank Operator

지금까지 계산한 총 7개의 변수 별 등수(Ranking)를 구하고, 그 등수의 열을 합치는 과정이다. 사용 방법은 Attribute를 설정하여 해당 attribute의 등수를 동점까지 분류한다. 기존 RapidMiner에서 제공하는 Rank Operator는 나의 등수를 새로운 열로 나타내기 위해 generate ID 등을 이용하여 입지선정과 같은 여러 데이터를 다루는 상황에서는 적합하지 않았다. 이를 보완하여 동점자까지 자동으로 처리하여 각 열의 Rank를 새로운 열로 만들어주는 Operator를 고안하였다.

![image](https://user-images.githubusercontent.com/26592315/148633791-3aa65426-8a5b-4e6a-bbee-b91d510a1d9d.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/148633799-2a290376-578a-4e5c-81f5-548f4df1ed6e.png){:width="100%" height="100%"}{: .center}

해당 오퍼레이터를 사용하여 변수별로 Ranking 한 결과

![image](https://user-images.githubusercontent.com/26592315/148633836-edda36d8-75aa-4b0c-ac69-6f40247c252b.png){:width="100%" height="100%"}{: .center}

---

##### Section 2.6 <a class="anchor" id="section_2_6"></a> Cost Operator

사용자가 원하는 가중치(Weight)를 곱하여 여러 항목을 통합하는 단일 결과를 낼 수 있는 Operator를 개발하였다. 여러 변수들을 입력 값으로 하는 cost 함수를 이용해 각종 변수들과 가중치를 입력 받아 변수와 가중치를 곱해 하나의 점수로 만들고 최종 후보지를 도출하는 과정이 필요하다.

Cost 함수에는 현재 500m 내 정류장 개수, 지하철 역 개수, 버스 노선 개수, 버스 노선 빈도, 환승 주차장 개수, 주변 차선 수, 지하철/버스 승 하차 인구, 기존 환승 센터까지의 거리 총 8개의 변수와 각각의 변수마다의 가중치가 포함되었다.

![image](https://user-images.githubusercontent.com/26592315/148633874-14317efd-bf79-4b56-8033-f06638688f9e.png){:width="100%" height="100%"}{: .center}

---

##### Chapter 3 <a class="anchor" id="chapter3"></a> : RapidMiner 결론

##### Section 3.1 <a class="anchor" id="section_3_1"></a> 상용에 없는 Operator를 개발한 후에 RapidMiner로 분석 결론

- 6가지 Operator를 개발하여 다음과 같은 최종 결과물이 도출되었다.

![image](https://user-images.githubusercontent.com/26592315/148634157-f2ac6937-c8fd-4106-a9f6-bd0e5f1f1e0c.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/148634193-d06fc1ee-0252-4221-b7ef-4e6f843ef2ed.png){:width="100%" height="100%"}{: .center}
![image](https://user-images.githubusercontent.com/26592315/148634205-7506d75a-ec8f-4d40-b536-877bf0319534.png){:width="100%" height="100%"}{: .center}

##### 결론

> - RapidMiner로 후보지 39곳의 Cost점수를 비교한 결과

| 등수 | 후보지         | Cost 점수 | 등수 | 후보지     | Cost 점수 |
| ---- | -------------- | --------- | ---- | ---------- | --------- |
| 1    | 강남           | 385.500   | 21   | 노원       | 820.750   |
| 2    | 시청           | 411.250   | 22   | 공덕       | 832.750   |
| 3    | 홍대입구       | 425.750   | 23   | 서울대입구 | 850       |
| 4    | 신촌           | 438.750   | 24   | 당산       | 940.750   |
| 5    | 종각           | 453.375   | 25   | 합정       | 950.125   |
| 6    | 을지로입구     | 470.875   | 26   | 쌍문       | 999.625   |
| 7    | 수유           | 562.125   | 27   | 혜화       | 1014      |
| 8    | 양재           | 585       | 28   | 선릉       | 1063.125  |
| 9    | 신림           | 638.250   | 29   | 건대입구   | 1073.875  |
| 10   | 가산디지털단지 | 667.750   | 30   | 천호       | 1102.625  |
| 11   | 연신내         | 695.125   | 31   | 대림       | 1116.125  |
| 12   | 사당           | 697.125   | 32   | 까치산     | 1161.500  |
| 13   | 신도림         | 703.500   | 33   | 남부터미널 | 1180.500  |
| 14   | 고속터미널     | 726.375   | 34   | 신사       | 1229.250  |
| 15   | 을지로3가      | 740.875   | 35   | 교대       | 1259.375  |
| 16   | 종로3가        | 785.625   | 36   | 압구정     | 1380.125  |
| 17   | 광화문         | 793       | 37   | 역삼       | 1427.750  |
| 18   | 신논현         | 799.375   | 38   | 강변       | 1510      |
| 19   | 동대문         | 800.375   | 39   | 성수       | 1637.875  |
| 20   | 노량진         | 816.375   |

- Cost 점수로 비교해본 결과 Python에서의 결론과 비슷하게 강남(1등), 홍대입구(3등), 수유(7등)로 나왔고 2,4,5,6등은 후보지인 홍대입구 근처이거나, 서울역 근처이기에 제외한다고 가정하면 Python에서의 결론과 같다.

결론: 서울시의 새로운 환승센터 후보지는 강남, 홍대입구, 수유이다.

---

##### Section 3.2 <a class="anchor" id="section_3_2"></a> RapidMiner 전체 Process

![image](https://user-images.githubusercontent.com/26592315/148634801-41e79b92-6e37-42c5-ab0b-b451d5d7ad62.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/148634803-c1237c9c-7c77-4051-8439-c3090b4d3404.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/148634804-5cbf310c-0fbd-4286-a415-278be97e49dd.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/148634806-0520f53c-16e8-4a43-b452-6cd7e3958a36.png){:width="100%" height="100%"}{: .center}
