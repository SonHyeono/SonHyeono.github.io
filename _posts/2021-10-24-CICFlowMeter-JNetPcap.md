---
title: "CICFlowMeter-JNetPcap"
categories:
  - Intern
feature_text: |
  The History of the 산학 R&D 프로젝트 인턴
---

#### (2021년 9월 ~ 12월) 산학 R&D 프로젝트 인턴(중간 보고서 10월 24일)

> - 현재 상황: 기업 측에서 분석 데이터로 Pcap 데이터를 주었다. Pcap 데이터는 정말 wireshark로 컴퓨터네트워크 수업때나 다루어보았지 너무 생소한 데이터여서 이것을 이해하고 분석하는데 시간을 많이 보냈다.

#### 기업에서 제공한 Data

- [header가 달린 pcap 분석 데이터](https://gitlab.thothlab.org/achaud16/apt)
- [header가 없는 pcap 분석 데이터](https://gitlab.thothlab.org/Advanced-Persistent-Threat/apt-2020/-/tree/master/data)

> > 각데이터 모두 cicflowmeter를 사용하여 capture 한것으로 보임.

#### 1. CICFlowMeter 오류 고치기

[CICFlowMeter](https://github.com/CanadianInstituteForCybersecurity/CICFlowMeter)

- Maven build시 Missing artifact 에러가 있었다. ( JnetPcap )

#### 해결법

##### 해결법 - 1

> > m2 파일 아래 settings.xml 만들고, eclipse project -> Maven-> user setting 두번째 Browse에서 만든 settings.xml 파일로 하기.

settings.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
 <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
     <localRepository>C:/Users/user/.m2/repository</localRepository>
     <interactiveMode>true</interactiveMode>
     <offline>false</offline>
     <pluginGroups/>
     <servers/>
     <mirrors/>
     <proxies/>
     <profiles/>
     <activeProfiles/>
 </settings>
```

##### 해결법 - 2

> > pom.xml과 build.gradle 그리고 /.m2/repository/org/jnetpcap/jnetpcap안의 파일과 버전을 맞추기

pom.xml

```xml
<!-- https://mvnrepository.com/artifact/jnetpcap/jnetpcap -->
		<dependency>
			<groupId>org.jnetpcap</groupId>
			<artifactId>jnetpcap</artifactId>
			<version>1.4.r1425</version>
		</dependency>
```

---

build.gradle

- compile group: 'org.jnetpcap', name: 'jnetpcap', version:'1.4.r1425'

---

/.m2/repository/org/jnetpcap/jnetpcap 안의 파일을 아래의 사진과 같이 배치

![jnetpcap-file2](https://user-images.githubusercontent.com/26592315/138590272-7d31ead8-1690-4ad7-9b63-4b216993e12d.png){: width="100%" height="100%"}{: .center}
![jnetpcap-file1](https://user-images.githubusercontent.com/26592315/138590285-a20a4d3a-d1b3-4e07-8e71-55f6b2c67099.png){: width="100%" height="100%"}{: .center}

(위에서 1.4.r1425파일 안은 jnetpcap-1.4.r1425-1.win64를 압축 풀고 나온 파일들을 집어넣고 그안에서 jnetpcap.jar 파일명을 jnetpcap-1.4.r1425으로 바꾼 형태, 그 외에 파일 안에 추가된 파일들은 실행하면서 생긴 파일들)

---

##### 해결법 - 3

> > 프로젝트 우클릭 -> Build path -> configure build path

![image](https://user-images.githubusercontent.com/26592315/138590360-19463c35-93a7-40af-91f0-832bae9d8ab8.png){: width="100%" height="100%"}{: .center}

- Source attachment 클릭후에 Edit -> 아까 jnetpcap 파일 안에 넣어둔 src zip 파일을 클릭
- Javadoc location 클릭 후에 Edit -> 아까 jnetpcap 파일 안에 넣어둔 javadoc zip 파일 클릭

---

#### 2. CICFlowMeter 실행 해보기

- App.java를 Run하면 pcap 데이터를 csv 파일로 변환 및 저장
  ![jnetpcap-file3](https://user-images.githubusercontent.com/26592315/138590723-09fb6122-ca7b-485e-bd20-82c945c3208a.png){: width="100%" height="100%"}{: .center}

---

#### 3. 기업에서 제공한 Pcap 데이터 분석 모델을 위한 논문

[논문](https://sailik1991.github.io/files/DAPT_at_MLHat2020.pdf)

##### APT(Advanced Persistent Threats)

> > 분석을 위한 기준과 코드에 대한 학습 중

#### 3. Task

- pcap를 csv파일로 변환한 데이터를 분류해주는 모델 생성
- rapiderminer와 gui 연결, Maven 라이브러리 불러오기, Java application 추가

#### 4. 최종 목표

- Foundry 팀의 최종 목표는 예측을 수행하는데 있고 필요시 분석모듈도 자체적으로 개발하고, 이를 아래 예측모듈처럼 RapidMiner GUI에 맞도록 Graph로 연결하도록 하는 것.
- 주어진 사이버공격데이타를 분류하고, 분석한후, 원하는 예측을 위하여 Deep Learning 모델을 만들고, 이것을 RapidMiner 형태의 Interface를 씌워서, 전체 RapidMiner GUI에 맞도록 Graph로 연결하도록 하는 것.
