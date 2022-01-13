---
title: "마지막보고서-transit_center(9)"
categories:
  - Intern
feature_text: |
  The History of the 산학 R&D 프로젝트 인턴
---

- [Chapter 1](#chapter1) RapidMiner New Operator 개발 코드

- [Chapter 2](#chapter2) Python 와 RapidMiner 차이

- [Chapter 3](#chapter3) 느낀점

---

# Chapter 1 <a class="anchor" id="chapter1"></a> : 6개의 Operator 코드

# [6개 Operator 코드 Github 주소](https://github.com/SonHyeono/Analyze-public-transportation-data/tree/main/RapidMiner)

- #### 이중에서 ExtractionTextOperator, CostOperator를 제외한 4개의 Operator는 내가 개발했다.

- #### 또한 RapidMiner로 분석하는 Process 전체도 내가 개발했다. 팀원들이 다른 일 때문에 바빠서 혼자 많이 했다. 슬프기도 하고 나도 할일이 많지만 나는 이 일을 잘 마무리하고 싶었다. 빅데이터분석 Tool인 RapidMiner로 직접 해보니, 편리했다. 하지만 세심한 데이터 전처리를 하는데 있어서 에로사항을 많이 겪었고 좌표데이터를 사용하는데 있어서 좌표간의 거리를 이용해야 하기에 Operator를 새로 만들었고 그 밖에도 전처리, 다양한 함수 때문에 Operator를 만들었다. 직접 Operator를 만드니깐 분석하기에 편리했다. 좋은 Tool인 것 같고 Python으로 세심하게 전처리하고 그 데이터를 사용하면 더 좋을 것 같다.

---

# Chapter 2 <a class="anchor" id="chapter2"></a> : Python 와 RapidMiner 차이

#### 서울시의 대중교통 환승 센터에 적합한 지점을 찾고자 두 가지 기술을 사용하여 분석하고 결론을 도출하였다.

#### RapidMiner의 경우 기존에 존재하는 Operator만 이용하게 되면 빠르게 가시적인 결과를 확인할 수 있어 시각화와 편리함에 높은 점수를 부여할 수 있다. 그러나 Operator 들의 제한으로 인해 RapidMiner로 세밀한 데이터 전처리에는 다소 어려움을 겪었다. 또한 필요한 Operator가 없을 경우 직접 개발해야 한다는 점이 이슈가 될 수 있다.

#### 반면, Python3로 모델을 만드는 과정에서는 정교하고 세밀하게 코드를 작성하며, 여러 유용한 패키지를 손쉽게 가져올 수 있었다. 결과적으로 데이터와 분석과정에 대한 이해도가 높다면 Python을 활용하고, Operator의 다양성만 확보된다면 초보자에겐 RapidMiner가 더 활용하기 좋다고 판단된다.

---

# Chapter 3 <a class="anchor" id="chapter3"></a> : 느낀점

#### RapidMiner Tool 사용 시에는 RapidMiner의 Join Operator를 사용했으나, Open Source 버전에서의 Join Operator 구현이 되어있지 않아 분석에 어려움이 있었다.

#### 또한 변수 선정에 보다 많은 시간을 들였다면 실제로 본 연구에서 정한 8개의 변수들이 입지 선정에 얼마나 중요한 영향을 미치는지는 정확하게 파악할 수 있었을 것이다.

#### 그러나 서울시 환승 센터의 입지선정 과정 뿐만 아니라 데이터 분석이 가능한 여러 Tool을 사용해보며 분석 용이성과 접근성, 분석 프로세스에 대해 깊이 있게 이해할 수 있었다. 직접 데이터를 기반으로 선정한 변수들을 고려하고 변수들의 값과 가중치를 생각하여 하나의 함수로 개발하고, 이를 통해 결과값을 도출해보았다는 것에 의의를 가지고 프로젝트에 임할 수 있었다.

#### 이러한 변수들을 생각해 봄으로써 추가적인 변수들을 구상하고 확장해 나가는 것은 이전에 변수들을 만들지 않았을 때보다 유리하게 작용하여, 앞으로 본 연구와 프로젝트에 살을 붙여 확장해 나가는 것이 수월할 것으로 예상된다.
