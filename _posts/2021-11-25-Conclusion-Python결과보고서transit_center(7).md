---
title: "My conclusion in Python about the transit center(7)-Python결과 보고서"
categories:
  - Intern
feature_text: |
  The History of the 산학 R&D 프로젝트 인턴
---

##### 서울시 대중교통 데이터를 이용해서 새로운 환승센터 적합지를 찾는 것이 주제.

버스-버스, 버스-타 교통수단을 잇는 대중교통 환승 센터(이하 환승 센터)는 승용차 위주의 교통량을 줄이고 대중교통 이용을 활성화하여 도심 교통환경을 개선하는 역할을 하고 있다.

---

##### 환승 센터를 찾기 위한 기준

환승 센터 정책 시행 결과 나타난 특징을 지표화 할 수 있도록 기준을 마련하였다. ‘교통수단 간 환승 편의성’은 지하철역 주변의 버스정류장, 지하철역의 개수를 통해 측정할 수 있다. ‘대중교통 활성화로 도심교통 환경 개선’은 공간성 확보를 위한 도로의 차선 수로 간접적 평가가 가능하다. 이는 환승 동선 최적화로 환승 시간 단축 효과에도 기여할 수 있다. ‘체계적인 노선 및 환승 정보 제공’은 후보지 주변 버스 노선 개수 및 빈도를 통해 지표화 할 수 있다. 환승 센터 입지를 선정하는 기준을 위해 데이터를 기반으로 변수를 설정하여 아래와 같은 총 8개의 입지선정 기준을 마련하였다.

---

![image](https://user-images.githubusercontent.com/26592315/147805373-24870d0e-b20a-473a-adaf-a8d1872e2f33.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805706-e6203288-2fce-48d9-bad6-8e037cdfc5f7.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805741-c0df4311-a641-4ef1-9050-0d7b868b4697.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805763-0d70a83f-c54f-4c6b-886e-c200d570be27.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805784-a13e82ea-482e-4de7-b5c5-c6601d7225de.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805804-ac816ec2-2ab8-4594-bdea-557dfb762a34.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805819-c6c0b29b-7a9d-4946-88da-87b075f3c00b.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805830-53714852-2ce0-4a8d-b76c-0784899c3373.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805838-32e4cf17-09a5-4e8b-806d-7960528b7ed7.png){:width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/147805843-ec991401-a626-4775-a51f-9a0d2009a8d6.png){:width="100%" height="100%"}{: .center}

---

##### 최종 환승 센터 입지 선정에 대한 결론 도출

- 결과적으로 Cost 함수 결과값이 제일 작은 역인 강남, 홍대입구, 수유 3개의 최종 후보지에 대한 조사를 추가적으로 진행하여 환승 센터 입지로서의 데이터 분석 결과를 뒷받침하였다.

---

##### 강남역

- 경기도에서 직접적으로 강남을 거쳐 서울에 유입되는 경기도 광주, 용인의 인구추이를 확인해본 결과 인구 추이가 늘고 있었고 성남의 인구는 줄어드는 추세이나, 여전히 많은 인구가 있었다.

---

##### 홍대입구역

- 홍대입구는 홍대 인근 역인 합정도 후보지 내에 있어 이 둘의 수요가 합쳐지면 더욱 영향력 있는 후보지가 될 수 있다. 추가로 신도시 계획 지역인 고양은 경의중앙선과 공항철도를 이용하므로 두 지하철이 만나는 홍대입구가 중요한 요충지가 될 것으로 보이며 고양시 인구추이 또한 계속해서 증가하고 있다.

##### 수유역

- 인근에 후보지인 쌍문역과 미아사거리가 있어 이를 한 지점으로 고려한다면 매우 경쟁력 있는 후보가 될 수 있다. 또한 보다시피 경기 북부의 의정부와 양주에서 서울을 진입하는 거점지로 해당 시의 인구 추이 증가와 더불어 노원, 도봉, 강북 인구를 통한 유동인구 증가가능성이 있다.
