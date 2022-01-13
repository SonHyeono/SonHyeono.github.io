---
title: "산학 R&D 프로젝트 인턴-Palantir_Foundry"
categories:
  - Intern
feature_text: |
  The History of the 산학 R&D 프로젝트 인턴
---

## (2021년 9월 ~ 12월) 산학 R&D 프로젝트 인턴

## 기업체가 제시한 주제

- [Foundry](https://www.palantir.com/platforms/foundry/) | 기업용 데이터 분석도구

  > - Foundry Software-Defined Data Integration enables you to automatically build data pipelines from your systems in hours and days – not months.
  >   It automates away the expensive, manual work of the past to build a semantic layer in hours, without having to write a single line of new code.

- [Gotham](https://www.palantir.com/platforms/gotham/) | 국방용 의사결정 시스템

  > - Gotham’s built-in feedback loops train and refine models that augment human analysis and decision making during operations.
  >   In turn, operator actions improve these models over time.

- Engine | 공개 SW를 이용한 엔진 확장
  > - Rapidminer 교육용버젼 공개SW소스 활용
  > - 현상태는 5,000개 데이타처리가능 용량 => 수십만개 까지 확장
  > - 데이터 처리속도도 무척 느림. 속도느린 원인 찾아 분석하고 개선

---

### 투입된 인원은 총 10명, 필자는 Foundry 팀

### Engine 팀이 해야할 일

- 하부 분산 처리 등을 이용해서 무료 버전에서 처리할수 있는 데이터 수를 늘리고 느린 데이터 처리 속도를 빠르게 하기.

### Foundry 팀이 해야할 일

> - Gui를 통해서 공급자한테 엔티티를 연결하며 Foundry 개념의 래피드마이너, 범용, dbms에서 데이터를 뽑아내서 분석하고 예측하는 것.
> - (주제가 물류,국방 상관없이) 대부분 large 데이터가 dbms에 저장이 되어있고, SCM은 회사내부에 다 있으니 법용 tool을 만들고 domain이 정해지면 쭉쭉 뽑아지는 tool을 만들기.
> - 래피드마이너는 operator만 있으면 발전 가능성이 많다.

---

# Foundry

> - 현재 팔란티어는 다양한 형태의 데이터를 통합하는 핵심 플랫폼인 ‘팔란티어 파운드리(Palantir Foundry)’와 도시·공공 문제 해결을 위한 ‘팔란티어 고담(Palantir Gotham)’ 솔루션을 구축하고 있다. 이를 바탕으로 사이버 보안, 금융, 법률, 제조, 기업합병, 보험 분석 등 다양한 영역에서의 분석 예측 서비스를 제공하고 있다.

### Foundry의 기능

> - 데이터 사이의 장벽을 제거하여 데이터를 재창조해 주는 플랫폼
> - 기업이 자체 데이터를 활용 할 수 있는 플랫폼을 제공
> - Ex) 기업 및 기관에게 금융사기 피해 방지, 내부 비리 포착, 제품 생산관리 분석

---

### 기업과 Palantir Foundry와의 협업 사례

![image](https://user-images.githubusercontent.com/26592315/135643248-b94b8ffc-e906-4424-a5ef-a6e032761781.png){: width="100%" height="100%"}{: .center}

- EX) [두산 인프라코어](https://www.youtube.com/watch?v=S7st0QER5So&t=213s)

> - 두산 인프라코어에서는 팔란티어와 파트너십으로 제품개발, 생산, 영업, 품질, 서비스등 value chain 전반에 데이터를 통합적으로 분석해서 데이터기반 협업 체인을 구축하고 데이터 중심의 사고와 의사결정을 하는 문화를 만들어 가고 있습니다.

    제조업의 주요 value chain인 SCM(공급망관리)업무를 가지고 설명하자면 건설 장비의 scm은 마켓 변화를 감지하고 빠르게 감지하고 신속하게 대응하는 것입니다. 그러나 코로나로 인해 신속하게 대응하기에는 기존의 방법들에 문제가 많이 생겼습니다. 그래서 DI360에서 Palantir와 함께 만든 3억 row에 달하는 빅데이터인 시장 수요 데이터 셋과 건설장비에 달린 TMS기기를 통해서 생성된 장비가동 시간 정보를 워크플로우를 만들어서 매시간 업데이트가 되는 장비가동시간 trend를 분석하여 국가별 마켓 수요의 회복속도를 현장에 가보지 않고 데이터기반으로 빠르게 반응할수 있습니다. 이런 분석을 기반으로 시장 예측을 계산을 하면서 팬더믹 상황아래에서 경쟁사들보다 빠르게 SCM 안정화를 이뤄나갈수 있게 되었습니다. DI360은 접근성 개선도 필요했기에 Palantir사와 논의 끝에 개발 cycle에서 필요한 다양한 영업정보들이 모두 담겨있으면서 하나 통합 권한으로 관리 되는 시스템을 구축하기로 하였습니다.
    신제품 개발 시 목표로 했던 판매량, 판매 가격, 수익성, 품질 수준등의 개별 목표항목 등에 대한 실시간 확인, 데이터 분석에 필요한 마켓 수요 변동현황등을 NPD 성과 관리라는 하나의 워크플로우에 담아 이를 통하여 제공되는 생생한 정보들이 신제품 개발에 도움이 되는 선순환 구조 업무 환경이 구축되었습니다.
    이렇게 두산 인프라코어는 정통적 제조사가 디지털 기술과 데이터 기반의 새로운 업무 방식을 추구하게 되었습니다.

---

# Task

> - RapidMiner와 DBMS( MongoDB, MySQL )등 연결 가능 확인

- RapidMiner의 Open Source를 이용해서 최대한 비슷하게 만든 후에 RapidMiner Engine을 이용한 Foundry의 多 기능 구현
