---
title: "Efforts to find a transit center(2)"
categories:
  - Intern
feature_text: |
  The History of the 산학 R&D 프로젝트 인턴
---

## Table of Contents in this notebook

- [Chapter 1](#chapter1) 2021년 1월~9월 평일 승하차 데이터 불러오기
  - [Section 1.1](#section_1_1) 정류장별로 groupby 짓고 승객수를 sum한 데이터 준비(2021년 1월 ~ 9월 승차 데이터)
- [Chapter 2](#chapter2) 2021년 1월~9월 평일 승차 Top 20
  - [Section 2.1](#section_2_1) 2021년 1월 ~ 9월까지 평일 승차 데이터를 Top 20으로 분류 & 기본키 수정
  - [Section 2.2](#section_2_2) 2021년 1월 ~ 9월까지의 Top 20 승차 데이터를 bar로 시각화
- [Chapter 3](#chapter3) 2021년 1월 ~ 9월까지의 승차 데이터 합병
  - [Section 3.1](#section_3_1) 합병한 데이터로부터 Top39으로 분류 & 1~9 월까지의 총합과 평균 구하기
  - [Section 3.2](#section_3_2) X좌표, Y좌표 대입
  - [Section 3.3](#section_3_3) 승차 Top 39 DataFrame을 Excel에 저장
- [Chapter 4](#chapter4) 2021년 1월 ~ 9월까지의 하차 데이터 합병
  - [Section 4.1](#section_4_1) 승차와 동일하게 진행
  - [Section 4.2](#section_4_2) 하차 Top 39 DataFrame을 Excel에 저장

#### Chapter 1 <a class="anchor" id="chapter1"></a>

##### 2021년 1월~9월 평일 승하차 데이터 불러오기

```python
import pandas as pd

#평일 데이터

busroute_0119 = pd.read_csv('C:/jupyter_data/노선별_OD_20210119.csv')

busroute_0216 = pd.read_csv('C:/jupyter_data/노선별_OD_20210216.csv',encoding='cp949')

busroute_0316 = pd.read_csv('C:/jupyter_data/노선별_OD_20210316.csv',encoding='cp949')

busroute_0420 = pd.read_csv('C:/jupyter_data/노선별_OD_20210420.csv',encoding='cp949')

busroute_0518 = pd.read_csv('C:/jupyter_data/노선별_OD_20210518.csv',encoding='cp949')

busroute_0615 = pd.read_csv('C:/jupyter_data/노선별OD_20210615.csv')

busroute_0720 = pd.read_csv('C:/jupyter_data/노선별OD_20210720.csv')

busroute_0817 = pd.read_csv('C:/jupyter_data/노선별OD_20210817.csv')

busroute_0921 = pd.read_csv('C:/jupyter_data/노선별OD_20210921.csv')

busroute_0119
```

    C:\Users\ok762\.conda\envs\py38\lib\site-packages\IPython\core\interactiveshell.py:3172: DtypeWarning: Columns (1) have mixed types.Specify dtype option on import or set low_memory=False.
      has_raised = await self.run_ast_nodes(code_ast.body, cell_name,

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>기준일자</th>
      <th>노선명</th>
      <th>승차_정류장ARS</th>
      <th>승차_정류장명</th>
      <th>하차_정류장ARS</th>
      <th>하차_정류장명</th>
      <th>승차_정류장순번</th>
      <th>하차_정류장순번</th>
      <th>승객수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20210119</td>
      <td>17</td>
      <td>3689.0</td>
      <td>청암자이아파트</td>
      <td>3247.0</td>
      <td>용문시장</td>
      <td>1.0</td>
      <td>9.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20210119</td>
      <td>17</td>
      <td>3689.0</td>
      <td>청암자이아파트</td>
      <td>3250.0</td>
      <td>용산전자상가입구</td>
      <td>1.0</td>
      <td>10.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20210119</td>
      <td>17</td>
      <td>3689.0</td>
      <td>청암자이아파트</td>
      <td>3252.0</td>
      <td>신용산.지하차도</td>
      <td>1.0</td>
      <td>11.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20210119</td>
      <td>17</td>
      <td>3689.0</td>
      <td>청암자이아파트</td>
      <td>3255.0</td>
      <td>용산역</td>
      <td>1.0</td>
      <td>12.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20210119</td>
      <td>17</td>
      <td>3689.0</td>
      <td>청암자이아파트</td>
      <td>3298.0</td>
      <td>청암동강변삼성아파트</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>466675</th>
      <td>20210119</td>
      <td>중랑02</td>
      <td>7526.0</td>
      <td>새마을금고</td>
      <td>7528.0</td>
      <td>진주빌라.바다약국</td>
      <td>23.0</td>
      <td>25.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>466676</th>
      <td>20210119</td>
      <td>중랑02</td>
      <td>7526.0</td>
      <td>새마을금고</td>
      <td>7529.0</td>
      <td>진로아파트앞.종점</td>
      <td>23.0</td>
      <td>26.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>466677</th>
      <td>20210119</td>
      <td>중랑02</td>
      <td>7527.0</td>
      <td>공판장</td>
      <td>7500.0</td>
      <td>진로아파트앞.종점</td>
      <td>24.0</td>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>466678</th>
      <td>20210119</td>
      <td>중랑02</td>
      <td>7528.0</td>
      <td>진주빌라.바다약국</td>
      <td>7528.0</td>
      <td>진주빌라.바다약국</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>466679</th>
      <td>20210119</td>
      <td>중랑02</td>
      <td>7529.0</td>
      <td>진로아파트앞.종점</td>
      <td>7529.0</td>
      <td>진로아파트앞.종점</td>
      <td>26.0</td>
      <td>26.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>466680 rows × 9 columns</p>
</div>

#### Section 1.1 <a class="anchor" id="section_1_1"></a>

##### 정류장별로 groupby 짓고 승객수를 sum한 데이터 준비(2021년 1월 ~ 9월 승차 데이터)

```python
# 1월 승차 평일

busstop_0119 = busroute_0119.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0119 = pd.DataFrame(busstop_0119)
getin_0119 = busstop_0119.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

# 2월 승차 평일

busstop_0216 = busroute_0216.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0216 = pd.DataFrame(busstop_0216)
getin_0216 = busstop_0216.sort_values(by ='승객수',axis=0,ascending=False).reset_index()


# 3월 승차 평일

busstop_0316 = busroute_0316.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0316 = pd.DataFrame(busstop_0316)
getin_0316 = busstop_0316.sort_values(by ='승객수',axis=0,ascending=False).reset_index()


# 4월 승차 평일

busstop_0420 = busroute_0420.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0420 = pd.DataFrame(busstop_0420)
getin_0420 = busstop_0420.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

# 5월 승차 평일

busstop_0518 = busroute_0518.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0518 = pd.DataFrame(busstop_0518)
getin_0518 = busstop_0518.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

# 6월 승차 평일

busstop_0615 = busroute_0615.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0615 = pd.DataFrame(busstop_0615)
getin_0615 = busstop_0615.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

# 7월 승차 평일

busstop_0720 = busroute_0720.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0720 = pd.DataFrame(busstop_0720)
getin_0720 = busstop_0720.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

# 8월 승차 평일

busstop_0817 = busroute_0817.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0817 = pd.DataFrame(busstop_0817)
getin_0817 = busstop_0817.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

# 9월 승차 평일

busstop_0921 = busroute_0921.groupby(['승차_정류장ARS'])['승객수'].sum()
busstop_0921 = pd.DataFrame(busstop_0921)
getin_0921 = busstop_0921.sort_values(by ='승객수',axis=0,ascending=False).reset_index()
```

#### Chapter 2 <a class="anchor" id="chapter2"></a>

#### Section 2.1 <a class="anchor" id="section_2_1"></a>

##### 2021년 1월 ~ 9월까지 평일 승차 데이터를 Top 20으로 분류 & 기본키 수정

> - 1월 부터 9월까지 평일 승차 데이터를 '승객수' 기준으로 Top 20으로 분류하였습니다.
> - 알아보기 쉬운 기본키로 정류장명에 정류장 ID를 문자열로 결합한 열로 '정류장명'으로 새로 만들었습니다.

```python
import numpy as np
pd.set_option('mode.chained_assignment',  None) #SettingWithCopy Warning or Error 경고 끄기위해서

# 1월 top 20 승차 평일

top20_0119 = getin_0119.head(20)

top20_0119["정류장명"] = np.nan

for idx in top20_0119.index:
    stop_name = top20_0119.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0119[busroute_0119['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0119.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

# 2월 top 20 승차 평일

top20_0216 = getin_0216.head(20)

top20_0216["정류장명"] = np.nan

for idx in top20_0216.index:
    stop_name = top20_0216.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0216[busroute_0216['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0216.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

# 3월 top 20 승차 평일

top20_0316 = getin_0316.head(20)

top20_0316["정류장명"] = np.nan


for idx in top20_0316.index:
    stop_name = top20_0316.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0316[busroute_0316['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0316.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

# 4월 top 20 승차 평일


top20_0420 = getin_0420.head(20)

top20_0420["정류장명"] = np.nan

for idx in top20_0420.index:
    stop_name = top20_0420.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0420[busroute_0420['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0420.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

# 5월 top 20 승차 평일


top20_0518 = getin_0518.head(20)

top20_0518["정류장명"] = np.nan

for idx in top20_0518.index:
    stop_name = top20_0518.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0518[busroute_0518['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0518.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

# 6월 top 20 승차 평일

top20_0615 = getin_0615.head(20)

top20_0615["정류장명"] = np.nan

for idx in top20_0615.index:
    stop_name = top20_0615.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0615[busroute_0615['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0615.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

# 7월 top 20 승차 평일

top20_0720 = getin_0720.head(20)

top20_0720["정류장명"] = np.nan

for idx in top20_0720.index:
    stop_name = top20_0720.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0720[busroute_0720['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0720.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

# 8월 top 20 승차 평일

top20_0817 = getin_0817.head(20)

top20_0817["정류장명"] = np.nan

for idx in top20_0817.index:
    stop_name = top20_0817.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0817[busroute_0817['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0817.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

# 9월 top 20 승차 평일

top20_0921 = getin_0921.head(20)

top20_0921["정류장명"] = np.nan

for idx in top20_0921.index:
    stop_name = top20_0921.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0921[busroute_0921['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top20_0921.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"


```

```python
top20_0615
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>승차_정류장ARS</th>
      <th>승객수</th>
      <th>정류장명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17014.0</td>
      <td>9626</td>
      <td>구로디지털단지역환승센터(17014.0)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9012.0</td>
      <td>8602</td>
      <td>미아사거리역(9012.0)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>22019.0</td>
      <td>8525</td>
      <td>고속터미널(22019.0)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>22012.0</td>
      <td>8224</td>
      <td>지하철2호선강남역(22012.0)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22289.0</td>
      <td>7550</td>
      <td>양재역(22289.0)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>19112.0</td>
      <td>7434</td>
      <td>경방타임스퀘어.신세계백화점(19112.0)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>9004.0</td>
      <td>7430</td>
      <td>수유역.강북구청(9004.0)</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17001.0</td>
      <td>7235</td>
      <td>신도림역(17001.0)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>23408.0</td>
      <td>7115</td>
      <td>수서역(23408.0)</td>
    </tr>
    <tr>
      <th>9</th>
      <td>14015.0</td>
      <td>7083</td>
      <td>홍대입구역(14015.0)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>21350.0</td>
      <td>6905</td>
      <td>신림사거리.신림역(21350.0)</td>
    </tr>
    <tr>
      <th>11</th>
      <td>17013.0</td>
      <td>6774</td>
      <td>구로디지털단지역(17013.0)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>10126.0</td>
      <td>6769</td>
      <td>쌍문역(10126.0)</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9011.0</td>
      <td>6749</td>
      <td>미아사거리역(9011.0)</td>
    </tr>
    <tr>
      <th>14</th>
      <td>22020.0</td>
      <td>6689</td>
      <td>고속터미널(22020.0)</td>
    </tr>
    <tr>
      <th>15</th>
      <td>8008.0</td>
      <td>6680</td>
      <td>돈암사거리.성신여대입구(8008.0)</td>
    </tr>
    <tr>
      <th>16</th>
      <td>21916.0</td>
      <td>6486</td>
      <td>신림역4번출구(21916.0)</td>
    </tr>
    <tr>
      <th>17</th>
      <td>24146.0</td>
      <td>6397</td>
      <td>잠실역.롯데월드(24146.0)</td>
    </tr>
    <tr>
      <th>18</th>
      <td>3162.0</td>
      <td>6296</td>
      <td>순천향대학병원(3162.0)</td>
    </tr>
    <tr>
      <th>19</th>
      <td>21153.0</td>
      <td>6290</td>
      <td>신림사거리(21153.0)</td>
    </tr>
  </tbody>
</table>
</div>

#### Section 2.2 <a class="anchor" id="section_2_2"></a>

##### 2021년 1월 ~ 9월까지의 Top 20 승차 데이터를 bar로 시각화

> - 1월 부터 9월까지 '승객수'를 기준으로 분류한 Top 20을 bar chart로 시각화 했습니다.

> - Y축은 새로 만든 기본키인 정류장명이고 X축은 승객수입니다.

```python
import matplotlib.pyplot as plt
%matplotlib inline
import os

# 운영체제별 한글 폰트 설정
if os.name == 'posix': # Mac 환경 폰트 설정
    plt.rc('font', family='AppleGothic')
elif os.name == 'nt': # Windows 환경 폰트 설정
    plt.rc('font', family='Malgun Gothic')

plt.rc('axes', unicode_minus=False) # 마이너스 폰트 설정


# 글씨 선명하게 출력하는 설정
%config InlineBackend.figure_format = 'retina'

fig, ax = plt.subplots(5, 2, figsize=(20, 50))

ax[0,0].barh("정류장명", "승객수", data = top20_0119)
ax[0,0].set_title("January 19, 2021 top 20 bus stops")
ax[0,0].set_xlabel("Count")
ax[0,0].set_ylabel("BUS STOP")

ax[0,1].barh("정류장명", "승객수", data = top20_0216)
ax[0,1].set_title("February 16, 2021 top 20 bus stops")
ax[0,1].set_xlabel("Count")
ax[0,1].set_ylabel("BUS STOP")

ax[1,0].barh("정류장명", "승객수", data = top20_0316)
ax[1,0].set_title("March 16, 2021 top 20 bus stops")
ax[1,0].set_xlabel("Count")
ax[1,0].set_ylabel("BUS STOP")

ax[1,1].barh("정류장명", "승객수", data = top20_0420)
ax[1,1].set_title("April 20, 2021 top 20 bus stops")
ax[1,1].set_xlabel("Count")
ax[1,1].set_ylabel("BUS STOP")

ax[2,0].barh("정류장명", "승객수", data = top20_0518)
ax[2,0].set_title("May 18, 2021 top 20 bus stops")
ax[2,0].set_xlabel("Count")
ax[2,0].set_ylabel("BUS STOP")

ax[2,1].barh("정류장명", "승객수", data = top20_0615)
ax[2,1].set_title("June 15, 2021 top 20 bus stops")
ax[2,1].set_xlabel("Count")
ax[2,1].set_ylabel("BUS STOP")

ax[3,0].barh("정류장명", "승객수", data = top20_0720)
ax[3,0].set_title("July 20, 2021 top 20 bus stops")
ax[3,0].set_xlabel("Count")
ax[3,0].set_ylabel("BUS STOP")

ax[3,1].barh("정류장명", "승객수", data = top20_0817)
ax[3,1].set_title("August 17, 2021 top 20 bus stops")
ax[3,1].set_xlabel("Count")
ax[3,1].set_ylabel("BUS STOP")

ax[4,0].barh("정류장명", "승객수", data = top20_0921)
ax[4,0].set_title("September 21, 2021 top 20 bus stops")
ax[4,0].set_xlabel("Count")
ax[4,0].set_ylabel("BUS STOP")



plt.subplots_adjust(left=0.2,
                    bottom=0.25,
                    right=0.82,
                    top=0.9,
                    wspace=0.8,
                    hspace=0.3)
plt.show()
```

<img width="1113" alt="top20_9" src="https://user-images.githubusercontent.com/26592315/141969355-99419708-4099-4add-886d-0529e6b4a022.png">{:width="100%" height="100%"}{: .center}

#### Chapter 3 <a class="anchor" id="chapter3"></a>

##### 2021년 1월 ~ 9월까지의 승차 데이터 합병

```python
getin_0119.rename(columns={'승객수':'1월_평일승차수'},inplace = True)
getin_0216.rename(columns={'승객수':'2월_평일승차수'},inplace = True)
getin_0316.rename(columns={'승객수':'3월_평일승차수'},inplace = True)
getin_0420.rename(columns={'승객수':'4월_평일승차수'},inplace = True)
getin_0518.rename(columns={'승객수':'5월_평일승차수'},inplace = True)
getin_0615.rename(columns={'승객수':'6월_평일승차수'},inplace = True)
getin_0720.rename(columns={'승객수':'7월_평일승차수'},inplace = True)
getin_0817.rename(columns={'승객수':'8월_평일승차수'},inplace = True)
getin_0921.rename(columns={'승객수':'9월_평일승차수'},inplace = True)
```

```python
boarding = pd.merge(getin_0119,getin_0216, how='outer')
boarding = pd.merge(boarding,getin_0316, how = 'outer')
boarding = pd.merge(boarding,getin_0420, how = 'outer')
boarding = pd.merge(boarding,getin_0518, how = 'outer')
boarding = pd.merge(boarding,getin_0615, how = 'outer')
boarding = pd.merge(boarding,getin_0720, how = 'outer')
boarding = pd.merge(boarding,getin_0817, how = 'outer')
boarding = pd.merge(boarding,getin_0921, how = 'outer')

boarding
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>승차_정류장ARS</th>
      <th>1월_평일승차수</th>
      <th>2월_평일승차수</th>
      <th>3월_평일승차수</th>
      <th>4월_평일승차수</th>
      <th>5월_평일승차수</th>
      <th>6월_평일승차수</th>
      <th>7월_평일승차수</th>
      <th>8월_평일승차수</th>
      <th>9월_평일승차수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17014.0</td>
      <td>8861.0</td>
      <td>9436.0</td>
      <td>9606.0</td>
      <td>9330.0</td>
      <td>9495.0</td>
      <td>9626.0</td>
      <td>8875.0</td>
      <td>9232.0</td>
      <td>3018.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9012.0</td>
      <td>7624.0</td>
      <td>8112.0</td>
      <td>8754.0</td>
      <td>8708.0</td>
      <td>9083.0</td>
      <td>8602.0</td>
      <td>8128.0</td>
      <td>8109.0</td>
      <td>3812.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>22019.0</td>
      <td>7361.0</td>
      <td>8113.0</td>
      <td>8795.0</td>
      <td>8606.0</td>
      <td>9557.0</td>
      <td>8525.0</td>
      <td>7399.0</td>
      <td>7576.0</td>
      <td>5561.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9004.0</td>
      <td>6950.0</td>
      <td>7525.0</td>
      <td>7817.0</td>
      <td>8050.0</td>
      <td>8163.0</td>
      <td>7430.0</td>
      <td>7405.0</td>
      <td>7575.0</td>
      <td>3450.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22012.0</td>
      <td>6915.0</td>
      <td>7897.0</td>
      <td>8452.0</td>
      <td>7984.0</td>
      <td>9354.0</td>
      <td>8224.0</td>
      <td>7455.0</td>
      <td>7575.0</td>
      <td>2457.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>12636</th>
      <td>15372.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>12637</th>
      <td>14147.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>12638</th>
      <td>36351.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>12639</th>
      <td>14136.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>12640</th>
      <td>24238.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>12641 rows × 10 columns</p>
</div>

#### Section 3.1 <a class="anchor" id="section_3_1"></a>

##### 합병한 데이터로부터 Top39으로 분류 & 1~9 월까지의 총합과 평균 구하기

##### + 합병한 데이터 셋의 기본키 수정

> - 합병한 데이터로 부터 Top 39를 뽑았고 1~9 월까지의 총합과 평균 그리고 알아보기 편하게 문자열을 조합한 '정류장명'이라는 열도 만들었습니다.

```python
boarding["정류장_승객수총합"] = boarding.loc[:,'1월_평일승차수':'9월_평일승차수'].sum(axis=1)
boarding["정류장_승객수평균"] = boarding.loc[:,'1월_평일승차수':'9월_평일승차수'].mean(axis=1)

top39_weekday = boarding.sort_values(by ='정류장_승객수총합',axis=0,ascending=False).head(39).reset_index(drop=True)

top39_weekday["정류장명"] = np.nan

for idx in top39_weekday.index:
    stop_name = top39_weekday.loc[idx,'승차_정류장ARS']

    df_ex = busroute_0119[busroute_0119['승차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['승차_정류장ARS'].astype(np.string_).decode('UTF-8')
    top39_weekday.loc[idx,'정류장명'] = df_ex.iloc[0]['승차_정류장명'] +"(" + ts + ")"

top39_weekday
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>승차_정류장ARS</th>
      <th>1월_평일승차수</th>
      <th>2월_평일승차수</th>
      <th>3월_평일승차수</th>
      <th>4월_평일승차수</th>
      <th>5월_평일승차수</th>
      <th>6월_평일승차수</th>
      <th>7월_평일승차수</th>
      <th>8월_평일승차수</th>
      <th>9월_평일승차수</th>
      <th>정류장_승객수총합</th>
      <th>정류장_승객수평균</th>
      <th>정류장명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17014.0</td>
      <td>8861.0</td>
      <td>9436.0</td>
      <td>9606.0</td>
      <td>9330.0</td>
      <td>9495.0</td>
      <td>9626.0</td>
      <td>8875.0</td>
      <td>9232.0</td>
      <td>3018.0</td>
      <td>77479.0</td>
      <td>8608.777778</td>
      <td>구로디지털단지역환승센터(17014.0)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22019.0</td>
      <td>7361.0</td>
      <td>8113.0</td>
      <td>8795.0</td>
      <td>8606.0</td>
      <td>9557.0</td>
      <td>8525.0</td>
      <td>7399.0</td>
      <td>7576.0</td>
      <td>5561.0</td>
      <td>71493.0</td>
      <td>7943.666667</td>
      <td>고속터미널(22019.0)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9012.0</td>
      <td>7624.0</td>
      <td>8112.0</td>
      <td>8754.0</td>
      <td>8708.0</td>
      <td>9083.0</td>
      <td>8602.0</td>
      <td>8128.0</td>
      <td>8109.0</td>
      <td>3812.0</td>
      <td>70932.0</td>
      <td>7881.333333</td>
      <td>미아사거리역(9012.0)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>22012.0</td>
      <td>6915.0</td>
      <td>7897.0</td>
      <td>8452.0</td>
      <td>7984.0</td>
      <td>9354.0</td>
      <td>8224.0</td>
      <td>7455.0</td>
      <td>7575.0</td>
      <td>2457.0</td>
      <td>66313.0</td>
      <td>7368.111111</td>
      <td>지하철2호선강남역(22012.0)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9004.0</td>
      <td>6950.0</td>
      <td>7525.0</td>
      <td>7817.0</td>
      <td>8050.0</td>
      <td>8163.0</td>
      <td>7430.0</td>
      <td>7405.0</td>
      <td>7575.0</td>
      <td>3450.0</td>
      <td>64365.0</td>
      <td>7151.666667</td>
      <td>수유역.강북구청(9004.0)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>19112.0</td>
      <td>6644.0</td>
      <td>7490.0</td>
      <td>7819.0</td>
      <td>7387.0</td>
      <td>8232.0</td>
      <td>7434.0</td>
      <td>7088.0</td>
      <td>7107.0</td>
      <td>3949.0</td>
      <td>63150.0</td>
      <td>7016.666667</td>
      <td>경방타임스퀘어.신세계백화점(19112.0)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>22289.0</td>
      <td>6712.0</td>
      <td>7378.0</td>
      <td>7632.0</td>
      <td>7623.0</td>
      <td>7627.0</td>
      <td>7550.0</td>
      <td>6685.0</td>
      <td>7048.0</td>
      <td>1371.0</td>
      <td>59626.0</td>
      <td>6625.111111</td>
      <td>양재역(22289.0)</td>
    </tr>
    <tr>
      <th>7</th>
      <td>21350.0</td>
      <td>6170.0</td>
      <td>6824.0</td>
      <td>7037.0</td>
      <td>6929.0</td>
      <td>7139.0</td>
      <td>6905.0</td>
      <td>6352.0</td>
      <td>6547.0</td>
      <td>2768.0</td>
      <td>56671.0</td>
      <td>6296.777778</td>
      <td>신림사거리.신림역(21350.0)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>23408.0</td>
      <td>6267.0</td>
      <td>6809.0</td>
      <td>7300.0</td>
      <td>7241.0</td>
      <td>7455.0</td>
      <td>7115.0</td>
      <td>6128.0</td>
      <td>6433.0</td>
      <td>1745.0</td>
      <td>56493.0</td>
      <td>6277.000000</td>
      <td>수서역(23408.0)</td>
    </tr>
    <tr>
      <th>9</th>
      <td>17001.0</td>
      <td>6252.0</td>
      <td>6713.0</td>
      <td>7062.0</td>
      <td>6994.0</td>
      <td>7434.0</td>
      <td>7235.0</td>
      <td>6160.0</td>
      <td>6237.0</td>
      <td>2168.0</td>
      <td>56255.0</td>
      <td>6250.555556</td>
      <td>신도림역(17001.0)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14015.0</td>
      <td>5833.0</td>
      <td>6649.0</td>
      <td>6845.0</td>
      <td>6624.0</td>
      <td>7491.0</td>
      <td>7083.0</td>
      <td>5906.0</td>
      <td>6188.0</td>
      <td>3291.0</td>
      <td>55910.0</td>
      <td>6212.222222</td>
      <td>홍대입구역(14015.0)</td>
    </tr>
    <tr>
      <th>11</th>
      <td>9011.0</td>
      <td>6043.0</td>
      <td>6346.0</td>
      <td>6959.0</td>
      <td>6912.0</td>
      <td>7296.0</td>
      <td>6749.0</td>
      <td>6283.0</td>
      <td>6253.0</td>
      <td>2913.0</td>
      <td>55754.0</td>
      <td>6194.888889</td>
      <td>미아사거리역(9011.0)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>22020.0</td>
      <td>5606.0</td>
      <td>6297.0</td>
      <td>6595.0</td>
      <td>6600.0</td>
      <td>7246.0</td>
      <td>6689.0</td>
      <td>6213.0</td>
      <td>6312.0</td>
      <td>4034.0</td>
      <td>55592.0</td>
      <td>6176.888889</td>
      <td>고속터미널(22020.0)</td>
    </tr>
    <tr>
      <th>13</th>
      <td>17013.0</td>
      <td>6332.0</td>
      <td>6835.0</td>
      <td>7045.0</td>
      <td>6970.0</td>
      <td>7191.0</td>
      <td>6774.0</td>
      <td>6158.0</td>
      <td>5848.0</td>
      <td>2034.0</td>
      <td>55187.0</td>
      <td>6131.888889</td>
      <td>구로디지털단지역(17013.0)</td>
    </tr>
    <tr>
      <th>14</th>
      <td>21916.0</td>
      <td>6083.0</td>
      <td>6737.0</td>
      <td>6673.0</td>
      <td>6622.0</td>
      <td>6692.0</td>
      <td>6486.0</td>
      <td>6084.0</td>
      <td>6894.0</td>
      <td>2850.0</td>
      <td>55121.0</td>
      <td>6124.555556</td>
      <td>신림역4번출구(21916.0)</td>
    </tr>
    <tr>
      <th>15</th>
      <td>8008.0</td>
      <td>5457.0</td>
      <td>6125.0</td>
      <td>6675.0</td>
      <td>6615.0</td>
      <td>7175.0</td>
      <td>6680.0</td>
      <td>5946.0</td>
      <td>6195.0</td>
      <td>2740.0</td>
      <td>53608.0</td>
      <td>5956.444444</td>
      <td>돈암사거리.성신여대입구(8008.0)</td>
    </tr>
    <tr>
      <th>16</th>
      <td>21153.0</td>
      <td>5882.0</td>
      <td>6468.0</td>
      <td>6594.0</td>
      <td>6335.0</td>
      <td>6687.0</td>
      <td>6290.0</td>
      <td>5826.0</td>
      <td>6032.0</td>
      <td>2916.0</td>
      <td>53030.0</td>
      <td>5892.222222</td>
      <td>신림사거리(21153.0)</td>
    </tr>
    <tr>
      <th>17</th>
      <td>10126.0</td>
      <td>2033.0</td>
      <td>6934.0</td>
      <td>6892.0</td>
      <td>6789.0</td>
      <td>7025.0</td>
      <td>6769.0</td>
      <td>6450.0</td>
      <td>6870.0</td>
      <td>2481.0</td>
      <td>52243.0</td>
      <td>5804.777778</td>
      <td>쌍문역(10126.0)</td>
    </tr>
    <tr>
      <th>18</th>
      <td>24146.0</td>
      <td>5682.0</td>
      <td>6380.0</td>
      <td>6428.0</td>
      <td>6345.0</td>
      <td>6723.0</td>
      <td>6397.0</td>
      <td>5633.0</td>
      <td>5717.0</td>
      <td>2131.0</td>
      <td>51436.0</td>
      <td>5715.111111</td>
      <td>잠실역.롯데월드(24146.0)</td>
    </tr>
    <tr>
      <th>19</th>
      <td>3162.0</td>
      <td>5303.0</td>
      <td>5526.0</td>
      <td>6262.0</td>
      <td>6426.0</td>
      <td>6786.0</td>
      <td>6296.0</td>
      <td>5513.0</td>
      <td>5718.0</td>
      <td>1777.0</td>
      <td>49607.0</td>
      <td>5511.888889</td>
      <td>순천향대학병원(3162.0)</td>
    </tr>
    <tr>
      <th>20</th>
      <td>6019.0</td>
      <td>5279.0</td>
      <td>5791.0</td>
      <td>6116.0</td>
      <td>6219.0</td>
      <td>6147.0</td>
      <td>6222.0</td>
      <td>5490.0</td>
      <td>5486.0</td>
      <td>2253.0</td>
      <td>49003.0</td>
      <td>5444.777778</td>
      <td>청량리역환승센터(6019.0)</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1023.0</td>
      <td>5255.0</td>
      <td>5543.0</td>
      <td>5977.0</td>
      <td>6116.0</td>
      <td>6375.0</td>
      <td>5821.0</td>
      <td>5584.0</td>
      <td>5633.0</td>
      <td>2135.0</td>
      <td>48439.0</td>
      <td>5382.111111</td>
      <td>동대문역.흥인지문(1023.0)</td>
    </tr>
    <tr>
      <th>22</th>
      <td>21330.0</td>
      <td>4393.0</td>
      <td>4939.0</td>
      <td>5865.0</td>
      <td>5952.0</td>
      <td>5934.0</td>
      <td>5481.0</td>
      <td>4808.0</td>
      <td>5330.0</td>
      <td>2043.0</td>
      <td>44745.0</td>
      <td>4971.666667</td>
      <td>서울대입구역(21330.0)</td>
    </tr>
    <tr>
      <th>23</th>
      <td>9013.0</td>
      <td>4811.0</td>
      <td>5092.0</td>
      <td>5346.0</td>
      <td>5443.0</td>
      <td>5699.0</td>
      <td>5214.0</td>
      <td>5125.0</td>
      <td>5169.0</td>
      <td>2495.0</td>
      <td>44394.0</td>
      <td>4932.666667</td>
      <td>수유(강북구청)역(9013.0)</td>
    </tr>
    <tr>
      <th>24</th>
      <td>8010.0</td>
      <td>4594.0</td>
      <td>4799.0</td>
      <td>5355.0</td>
      <td>5541.0</td>
      <td>6061.0</td>
      <td>5485.0</td>
      <td>4869.0</td>
      <td>5048.0</td>
      <td>2124.0</td>
      <td>43876.0</td>
      <td>4875.111111</td>
      <td>삼선교.한성대학교.조소앙활동터(8010.0)</td>
    </tr>
    <tr>
      <th>25</th>
      <td>22010.0</td>
      <td>4559.0</td>
      <td>4992.0</td>
      <td>5492.0</td>
      <td>5526.0</td>
      <td>5871.0</td>
      <td>5275.0</td>
      <td>4556.0</td>
      <td>4606.0</td>
      <td>959.0</td>
      <td>41836.0</td>
      <td>4648.444444</td>
      <td>신분당선강남역(22010.0)</td>
    </tr>
    <tr>
      <th>26</th>
      <td>20115.0</td>
      <td>4466.0</td>
      <td>5017.0</td>
      <td>5292.0</td>
      <td>5207.0</td>
      <td>5346.0</td>
      <td>5027.0</td>
      <td>4673.0</td>
      <td>4515.0</td>
      <td>1946.0</td>
      <td>41489.0</td>
      <td>4609.888889</td>
      <td>노량진역(20115.0)</td>
    </tr>
    <tr>
      <th>27</th>
      <td>11283.0</td>
      <td>4302.0</td>
      <td>4684.0</td>
      <td>4977.0</td>
      <td>4968.0</td>
      <td>5330.0</td>
      <td>4946.0</td>
      <td>4405.0</td>
      <td>4697.0</td>
      <td>1850.0</td>
      <td>40159.0</td>
      <td>4462.111111</td>
      <td>석계역1번출구.A(11283.0)</td>
    </tr>
    <tr>
      <th>28</th>
      <td>21149.0</td>
      <td>4414.0</td>
      <td>4897.0</td>
      <td>5009.0</td>
      <td>4953.0</td>
      <td>5059.0</td>
      <td>4895.0</td>
      <td>4652.0</td>
      <td>4684.0</td>
      <td>1498.0</td>
      <td>40061.0</td>
      <td>4451.222222</td>
      <td>패션문화의거리입구(21149.0)</td>
    </tr>
    <tr>
      <th>29</th>
      <td>21131.0</td>
      <td>4168.0</td>
      <td>4827.0</td>
      <td>4794.0</td>
      <td>4913.0</td>
      <td>5229.0</td>
      <td>4965.0</td>
      <td>4644.0</td>
      <td>4869.0</td>
      <td>1532.0</td>
      <td>39941.0</td>
      <td>4437.888889</td>
      <td>봉천사거리.봉천중앙시장(21131.0)</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2004.0</td>
      <td>3963.0</td>
      <td>4387.0</td>
      <td>4837.0</td>
      <td>4909.0</td>
      <td>5299.0</td>
      <td>4772.0</td>
      <td>4069.0</td>
      <td>4187.0</td>
      <td>2587.0</td>
      <td>39010.0</td>
      <td>4334.444444</td>
      <td>서울역버스환승센터(2004.0)</td>
    </tr>
    <tr>
      <th>31</th>
      <td>22011.0</td>
      <td>4015.0</td>
      <td>4873.0</td>
      <td>4785.0</td>
      <td>4365.0</td>
      <td>5243.0</td>
      <td>4583.0</td>
      <td>4379.0</td>
      <td>4663.0</td>
      <td>1635.0</td>
      <td>38541.0</td>
      <td>4282.333333</td>
      <td>지하철2호선강남역(22011.0)</td>
    </tr>
    <tr>
      <th>32</th>
      <td>21001.0</td>
      <td>4341.0</td>
      <td>4673.0</td>
      <td>4887.0</td>
      <td>4742.0</td>
      <td>4830.0</td>
      <td>4720.0</td>
      <td>4320.0</td>
      <td>4323.0</td>
      <td>1386.0</td>
      <td>38222.0</td>
      <td>4246.888889</td>
      <td>구로디지털단지역(21001.0)</td>
    </tr>
    <tr>
      <th>33</th>
      <td>3165.0</td>
      <td>4114.0</td>
      <td>4288.0</td>
      <td>4730.0</td>
      <td>4858.0</td>
      <td>5438.0</td>
      <td>4928.0</td>
      <td>4357.0</td>
      <td>4291.0</td>
      <td>1118.0</td>
      <td>38122.0</td>
      <td>4235.777778</td>
      <td>순천향대학병원.한남오거리(3165.0)</td>
    </tr>
    <tr>
      <th>34</th>
      <td>6015.0</td>
      <td>3825.0</td>
      <td>4379.0</td>
      <td>4522.0</td>
      <td>4708.0</td>
      <td>4912.0</td>
      <td>4638.0</td>
      <td>4344.0</td>
      <td>4444.0</td>
      <td>2276.0</td>
      <td>38048.0</td>
      <td>4227.555556</td>
      <td>청량리역환승센타(6015.0)</td>
    </tr>
    <tr>
      <th>35</th>
      <td>17185.0</td>
      <td>3998.0</td>
      <td>4421.0</td>
      <td>4866.0</td>
      <td>4704.0</td>
      <td>4892.0</td>
      <td>5032.0</td>
      <td>4139.0</td>
      <td>4393.0</td>
      <td>1344.0</td>
      <td>37789.0</td>
      <td>4198.777778</td>
      <td>온수역(17185.0)</td>
    </tr>
    <tr>
      <th>36</th>
      <td>21139.0</td>
      <td>4017.0</td>
      <td>4324.0</td>
      <td>4527.0</td>
      <td>4625.0</td>
      <td>4621.0</td>
      <td>4422.0</td>
      <td>4476.0</td>
      <td>4475.0</td>
      <td>1548.0</td>
      <td>37035.0</td>
      <td>4115.000000</td>
      <td>관악구청(21139.0)</td>
    </tr>
    <tr>
      <th>37</th>
      <td>10016.0</td>
      <td>4228.0</td>
      <td>4504.0</td>
      <td>4573.0</td>
      <td>4463.0</td>
      <td>4572.0</td>
      <td>4366.0</td>
      <td>4115.0</td>
      <td>4240.0</td>
      <td>1537.0</td>
      <td>36598.0</td>
      <td>4066.444444</td>
      <td>쌍문역(10016.0)</td>
    </tr>
    <tr>
      <th>38</th>
      <td>14012.0</td>
      <td>3867.0</td>
      <td>4189.0</td>
      <td>4671.0</td>
      <td>4680.0</td>
      <td>5094.0</td>
      <td>4638.0</td>
      <td>3874.0</td>
      <td>3809.0</td>
      <td>1663.0</td>
      <td>36485.0</td>
      <td>4053.888889</td>
      <td>합정역(14012.0)</td>
    </tr>
  </tbody>
</table>
</div>

#### Section 3.2 <a class="anchor" id="section_3_2"></a>

##### X좌표, Y좌표 대입

```python
bus_stop = pd.read_csv('C:/jupyter_data/서울시버스정류소좌표데이터(2021.01.14.).csv')
bus_stop.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>표준ID</th>
      <th>ARS-ID</th>
      <th>정류소명</th>
      <th>X좌표</th>
      <th>Y좌표</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100000001</td>
      <td>1001</td>
      <td>종로2가사거리</td>
      <td>126.987786</td>
      <td>37.569764</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100000002</td>
      <td>1002</td>
      <td>창경궁.서울대학교병원</td>
      <td>126.996520</td>
      <td>37.579179</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100000003</td>
      <td>1003</td>
      <td>명륜3가.성대입구</td>
      <td>126.998290</td>
      <td>37.582709</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100000004</td>
      <td>1004</td>
      <td>종로2가.삼일교</td>
      <td>126.987507</td>
      <td>37.568582</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100000005</td>
      <td>1005</td>
      <td>혜화동로터리.여운형활동터</td>
      <td>127.001694</td>
      <td>37.586230</td>
    </tr>
  </tbody>
</table>
</div>

```python
top39_weekday["X좌표"] = np.nan
top39_weekday["Y좌표"] = np.nan

for idx in top39_weekday.index:
    stop_name = top39_weekday.loc[idx,'승차_정류장ARS']

    df_ex = bus_stop[bus_stop['ARS-ID'] == stop_name]

    top39_weekday.loc[idx,'X좌표'] = df_ex.iloc[0]['X좌표']
    top39_weekday.loc[idx,'Y좌표'] = df_ex.iloc[0]['Y좌표']


top39_weekday = top39_weekday.dropna(axis=0)
top39_weekday = top39_weekday.reindex(columns=['승차_정류장ARS','정류장명','1월_평일승차수', '2월_평일승차수', '3월_평일승차수' ,
                                               '4월_평일승차수', '5월_평일승차수','6월_평일승차수','7월_평일승차수', '8월_평일승차수',
                                               '9월_평일승차수','정류장_승객수총합', '정류장_승객수평균', 'X좌표', 'Y좌표' ])
top39_weekday
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>승차_정류장ARS</th>
      <th>정류장명</th>
      <th>1월_평일승차수</th>
      <th>2월_평일승차수</th>
      <th>3월_평일승차수</th>
      <th>4월_평일승차수</th>
      <th>5월_평일승차수</th>
      <th>6월_평일승차수</th>
      <th>7월_평일승차수</th>
      <th>8월_평일승차수</th>
      <th>9월_평일승차수</th>
      <th>정류장_승객수총합</th>
      <th>정류장_승객수평균</th>
      <th>X좌표</th>
      <th>Y좌표</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>17014.0</td>
      <td>구로디지털단지역환승센터(17014.0)</td>
      <td>8861.0</td>
      <td>9436.0</td>
      <td>9606.0</td>
      <td>9330.0</td>
      <td>9495.0</td>
      <td>9626.0</td>
      <td>8875.0</td>
      <td>9232.0</td>
      <td>3018.0</td>
      <td>77479.0</td>
      <td>8608.777778</td>
      <td>126.902006</td>
      <td>37.484607</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22019.0</td>
      <td>고속터미널(22019.0)</td>
      <td>7361.0</td>
      <td>8113.0</td>
      <td>8795.0</td>
      <td>8606.0</td>
      <td>9557.0</td>
      <td>8525.0</td>
      <td>7399.0</td>
      <td>7576.0</td>
      <td>5561.0</td>
      <td>71493.0</td>
      <td>7943.666667</td>
      <td>127.005263</td>
      <td>37.506335</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9012.0</td>
      <td>미아사거리역(9012.0)</td>
      <td>7624.0</td>
      <td>8112.0</td>
      <td>8754.0</td>
      <td>8708.0</td>
      <td>9083.0</td>
      <td>8602.0</td>
      <td>8128.0</td>
      <td>8109.0</td>
      <td>3812.0</td>
      <td>70932.0</td>
      <td>7881.333333</td>
      <td>127.030240</td>
      <td>37.612897</td>
    </tr>
    <tr>
      <th>3</th>
      <td>22012.0</td>
      <td>지하철2호선강남역(22012.0)</td>
      <td>6915.0</td>
      <td>7897.0</td>
      <td>8452.0</td>
      <td>7984.0</td>
      <td>9354.0</td>
      <td>8224.0</td>
      <td>7455.0</td>
      <td>7575.0</td>
      <td>2457.0</td>
      <td>66313.0</td>
      <td>7368.111111</td>
      <td>127.026418</td>
      <td>37.500757</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9004.0</td>
      <td>수유역.강북구청(9004.0)</td>
      <td>6950.0</td>
      <td>7525.0</td>
      <td>7817.0</td>
      <td>8050.0</td>
      <td>8163.0</td>
      <td>7430.0</td>
      <td>7405.0</td>
      <td>7575.0</td>
      <td>3450.0</td>
      <td>64365.0</td>
      <td>7151.666667</td>
      <td>127.025183</td>
      <td>37.637522</td>
    </tr>
    <tr>
      <th>5</th>
      <td>19112.0</td>
      <td>경방타임스퀘어.신세계백화점(19112.0)</td>
      <td>6644.0</td>
      <td>7490.0</td>
      <td>7819.0</td>
      <td>7387.0</td>
      <td>8232.0</td>
      <td>7434.0</td>
      <td>7088.0</td>
      <td>7107.0</td>
      <td>3949.0</td>
      <td>63150.0</td>
      <td>7016.666667</td>
      <td>126.906191</td>
      <td>37.517492</td>
    </tr>
    <tr>
      <th>6</th>
      <td>22289.0</td>
      <td>양재역(22289.0)</td>
      <td>6712.0</td>
      <td>7378.0</td>
      <td>7632.0</td>
      <td>7623.0</td>
      <td>7627.0</td>
      <td>7550.0</td>
      <td>6685.0</td>
      <td>7048.0</td>
      <td>1371.0</td>
      <td>59626.0</td>
      <td>6625.111111</td>
      <td>127.034999</td>
      <td>37.483382</td>
    </tr>
    <tr>
      <th>7</th>
      <td>21350.0</td>
      <td>신림사거리.신림역(21350.0)</td>
      <td>6170.0</td>
      <td>6824.0</td>
      <td>7037.0</td>
      <td>6929.0</td>
      <td>7139.0</td>
      <td>6905.0</td>
      <td>6352.0</td>
      <td>6547.0</td>
      <td>2768.0</td>
      <td>56671.0</td>
      <td>6296.777778</td>
      <td>126.928285</td>
      <td>37.484152</td>
    </tr>
    <tr>
      <th>8</th>
      <td>23408.0</td>
      <td>수서역(23408.0)</td>
      <td>6267.0</td>
      <td>6809.0</td>
      <td>7300.0</td>
      <td>7241.0</td>
      <td>7455.0</td>
      <td>7115.0</td>
      <td>6128.0</td>
      <td>6433.0</td>
      <td>1745.0</td>
      <td>56493.0</td>
      <td>6277.000000</td>
      <td>127.101829</td>
      <td>37.486832</td>
    </tr>
    <tr>
      <th>9</th>
      <td>17001.0</td>
      <td>신도림역(17001.0)</td>
      <td>6252.0</td>
      <td>6713.0</td>
      <td>7062.0</td>
      <td>6994.0</td>
      <td>7434.0</td>
      <td>7235.0</td>
      <td>6160.0</td>
      <td>6237.0</td>
      <td>2168.0</td>
      <td>56255.0</td>
      <td>6250.555556</td>
      <td>126.889413</td>
      <td>37.509765</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14015.0</td>
      <td>홍대입구역(14015.0)</td>
      <td>5833.0</td>
      <td>6649.0</td>
      <td>6845.0</td>
      <td>6624.0</td>
      <td>7491.0</td>
      <td>7083.0</td>
      <td>5906.0</td>
      <td>6188.0</td>
      <td>3291.0</td>
      <td>55910.0</td>
      <td>6212.222222</td>
      <td>126.923302</td>
      <td>37.556398</td>
    </tr>
    <tr>
      <th>11</th>
      <td>9011.0</td>
      <td>미아사거리역(9011.0)</td>
      <td>6043.0</td>
      <td>6346.0</td>
      <td>6959.0</td>
      <td>6912.0</td>
      <td>7296.0</td>
      <td>6749.0</td>
      <td>6283.0</td>
      <td>6253.0</td>
      <td>2913.0</td>
      <td>55754.0</td>
      <td>6194.888889</td>
      <td>127.030002</td>
      <td>37.613765</td>
    </tr>
    <tr>
      <th>12</th>
      <td>22020.0</td>
      <td>고속터미널(22020.0)</td>
      <td>5606.0</td>
      <td>6297.0</td>
      <td>6595.0</td>
      <td>6600.0</td>
      <td>7246.0</td>
      <td>6689.0</td>
      <td>6213.0</td>
      <td>6312.0</td>
      <td>4034.0</td>
      <td>55592.0</td>
      <td>6176.888889</td>
      <td>127.003841</td>
      <td>37.505637</td>
    </tr>
    <tr>
      <th>13</th>
      <td>17013.0</td>
      <td>구로디지털단지역(17013.0)</td>
      <td>6332.0</td>
      <td>6835.0</td>
      <td>7045.0</td>
      <td>6970.0</td>
      <td>7191.0</td>
      <td>6774.0</td>
      <td>6158.0</td>
      <td>5848.0</td>
      <td>2034.0</td>
      <td>55187.0</td>
      <td>6131.888889</td>
      <td>126.901476</td>
      <td>37.483136</td>
    </tr>
    <tr>
      <th>14</th>
      <td>21916.0</td>
      <td>신림역4번출구(21916.0)</td>
      <td>6083.0</td>
      <td>6737.0</td>
      <td>6673.0</td>
      <td>6622.0</td>
      <td>6692.0</td>
      <td>6486.0</td>
      <td>6084.0</td>
      <td>6894.0</td>
      <td>2850.0</td>
      <td>55121.0</td>
      <td>6124.555556</td>
      <td>126.929020</td>
      <td>37.484055</td>
    </tr>
    <tr>
      <th>15</th>
      <td>8008.0</td>
      <td>돈암사거리.성신여대입구(8008.0)</td>
      <td>5457.0</td>
      <td>6125.0</td>
      <td>6675.0</td>
      <td>6615.0</td>
      <td>7175.0</td>
      <td>6680.0</td>
      <td>5946.0</td>
      <td>6195.0</td>
      <td>2740.0</td>
      <td>53608.0</td>
      <td>5956.444444</td>
      <td>127.017819</td>
      <td>37.593321</td>
    </tr>
    <tr>
      <th>16</th>
      <td>21153.0</td>
      <td>신림사거리(21153.0)</td>
      <td>5882.0</td>
      <td>6468.0</td>
      <td>6594.0</td>
      <td>6335.0</td>
      <td>6687.0</td>
      <td>6290.0</td>
      <td>5826.0</td>
      <td>6032.0</td>
      <td>2916.0</td>
      <td>53030.0</td>
      <td>5892.222222</td>
      <td>126.929718</td>
      <td>37.482773</td>
    </tr>
    <tr>
      <th>17</th>
      <td>10126.0</td>
      <td>쌍문역(10126.0)</td>
      <td>2033.0</td>
      <td>6934.0</td>
      <td>6892.0</td>
      <td>6789.0</td>
      <td>7025.0</td>
      <td>6769.0</td>
      <td>6450.0</td>
      <td>6870.0</td>
      <td>2481.0</td>
      <td>52243.0</td>
      <td>5804.777778</td>
      <td>127.034091</td>
      <td>37.647405</td>
    </tr>
    <tr>
      <th>18</th>
      <td>24146.0</td>
      <td>잠실역.롯데월드(24146.0)</td>
      <td>5682.0</td>
      <td>6380.0</td>
      <td>6428.0</td>
      <td>6345.0</td>
      <td>6723.0</td>
      <td>6397.0</td>
      <td>5633.0</td>
      <td>5717.0</td>
      <td>2131.0</td>
      <td>51436.0</td>
      <td>5715.111111</td>
      <td>127.098090</td>
      <td>37.512636</td>
    </tr>
    <tr>
      <th>19</th>
      <td>3162.0</td>
      <td>순천향대학병원(3162.0)</td>
      <td>5303.0</td>
      <td>5526.0</td>
      <td>6262.0</td>
      <td>6426.0</td>
      <td>6786.0</td>
      <td>6296.0</td>
      <td>5513.0</td>
      <td>5718.0</td>
      <td>1777.0</td>
      <td>49607.0</td>
      <td>5511.888889</td>
      <td>127.005612</td>
      <td>37.536390</td>
    </tr>
    <tr>
      <th>20</th>
      <td>6019.0</td>
      <td>청량리역환승센터(6019.0)</td>
      <td>5279.0</td>
      <td>5791.0</td>
      <td>6116.0</td>
      <td>6219.0</td>
      <td>6147.0</td>
      <td>6222.0</td>
      <td>5490.0</td>
      <td>5486.0</td>
      <td>2253.0</td>
      <td>49003.0</td>
      <td>5444.777778</td>
      <td>127.045695</td>
      <td>37.580412</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1023.0</td>
      <td>동대문역.흥인지문(1023.0)</td>
      <td>5255.0</td>
      <td>5543.0</td>
      <td>5977.0</td>
      <td>6116.0</td>
      <td>6375.0</td>
      <td>5821.0</td>
      <td>5584.0</td>
      <td>5633.0</td>
      <td>2135.0</td>
      <td>48439.0</td>
      <td>5382.111111</td>
      <td>127.013462</td>
      <td>37.572280</td>
    </tr>
    <tr>
      <th>22</th>
      <td>21330.0</td>
      <td>서울대입구역(21330.0)</td>
      <td>4393.0</td>
      <td>4939.0</td>
      <td>5865.0</td>
      <td>5952.0</td>
      <td>5934.0</td>
      <td>5481.0</td>
      <td>4808.0</td>
      <td>5330.0</td>
      <td>2043.0</td>
      <td>44745.0</td>
      <td>4971.666667</td>
      <td>126.952490</td>
      <td>37.480696</td>
    </tr>
    <tr>
      <th>23</th>
      <td>9013.0</td>
      <td>수유(강북구청)역(9013.0)</td>
      <td>4811.0</td>
      <td>5092.0</td>
      <td>5346.0</td>
      <td>5443.0</td>
      <td>5699.0</td>
      <td>5214.0</td>
      <td>5125.0</td>
      <td>5169.0</td>
      <td>2495.0</td>
      <td>44394.0</td>
      <td>4932.666667</td>
      <td>127.026037</td>
      <td>37.638520</td>
    </tr>
    <tr>
      <th>24</th>
      <td>8010.0</td>
      <td>삼선교.한성대학교.조소앙활동터(8010.0)</td>
      <td>4594.0</td>
      <td>4799.0</td>
      <td>5355.0</td>
      <td>5541.0</td>
      <td>6061.0</td>
      <td>5485.0</td>
      <td>4869.0</td>
      <td>5048.0</td>
      <td>2124.0</td>
      <td>43876.0</td>
      <td>4875.111111</td>
      <td>127.008364</td>
      <td>37.589327</td>
    </tr>
    <tr>
      <th>25</th>
      <td>22010.0</td>
      <td>신분당선강남역(22010.0)</td>
      <td>4559.0</td>
      <td>4992.0</td>
      <td>5492.0</td>
      <td>5526.0</td>
      <td>5871.0</td>
      <td>5275.0</td>
      <td>4556.0</td>
      <td>4606.0</td>
      <td>959.0</td>
      <td>41836.0</td>
      <td>4648.444444</td>
      <td>127.029163</td>
      <td>37.494957</td>
    </tr>
    <tr>
      <th>26</th>
      <td>20115.0</td>
      <td>노량진역(20115.0)</td>
      <td>4466.0</td>
      <td>5017.0</td>
      <td>5292.0</td>
      <td>5207.0</td>
      <td>5346.0</td>
      <td>5027.0</td>
      <td>4673.0</td>
      <td>4515.0</td>
      <td>1946.0</td>
      <td>41489.0</td>
      <td>4609.888889</td>
      <td>126.943351</td>
      <td>37.513824</td>
    </tr>
    <tr>
      <th>27</th>
      <td>11283.0</td>
      <td>석계역1번출구.A(11283.0)</td>
      <td>4302.0</td>
      <td>4684.0</td>
      <td>4977.0</td>
      <td>4968.0</td>
      <td>5330.0</td>
      <td>4946.0</td>
      <td>4405.0</td>
      <td>4697.0</td>
      <td>1850.0</td>
      <td>40159.0</td>
      <td>4462.111111</td>
      <td>127.065046</td>
      <td>37.614814</td>
    </tr>
    <tr>
      <th>28</th>
      <td>21149.0</td>
      <td>패션문화의거리입구(21149.0)</td>
      <td>4414.0</td>
      <td>4897.0</td>
      <td>5009.0</td>
      <td>4953.0</td>
      <td>5059.0</td>
      <td>4895.0</td>
      <td>4652.0</td>
      <td>4684.0</td>
      <td>1498.0</td>
      <td>40061.0</td>
      <td>4451.222222</td>
      <td>126.929480</td>
      <td>37.485989</td>
    </tr>
    <tr>
      <th>29</th>
      <td>21131.0</td>
      <td>봉천사거리.봉천중앙시장(21131.0)</td>
      <td>4168.0</td>
      <td>4827.0</td>
      <td>4794.0</td>
      <td>4913.0</td>
      <td>5229.0</td>
      <td>4965.0</td>
      <td>4644.0</td>
      <td>4869.0</td>
      <td>1532.0</td>
      <td>39941.0</td>
      <td>4437.888889</td>
      <td>126.954099</td>
      <td>37.482953</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2004.0</td>
      <td>서울역버스환승센터(2004.0)</td>
      <td>3963.0</td>
      <td>4387.0</td>
      <td>4837.0</td>
      <td>4909.0</td>
      <td>5299.0</td>
      <td>4772.0</td>
      <td>4069.0</td>
      <td>4187.0</td>
      <td>2587.0</td>
      <td>39010.0</td>
      <td>4334.444444</td>
      <td>126.972552</td>
      <td>37.555478</td>
    </tr>
    <tr>
      <th>31</th>
      <td>22011.0</td>
      <td>지하철2호선강남역(22011.0)</td>
      <td>4015.0</td>
      <td>4873.0</td>
      <td>4785.0</td>
      <td>4365.0</td>
      <td>5243.0</td>
      <td>4583.0</td>
      <td>4379.0</td>
      <td>4663.0</td>
      <td>1635.0</td>
      <td>38541.0</td>
      <td>4282.333333</td>
      <td>127.025728</td>
      <td>37.501609</td>
    </tr>
    <tr>
      <th>32</th>
      <td>21001.0</td>
      <td>구로디지털단지역(21001.0)</td>
      <td>4341.0</td>
      <td>4673.0</td>
      <td>4887.0</td>
      <td>4742.0</td>
      <td>4830.0</td>
      <td>4720.0</td>
      <td>4320.0</td>
      <td>4323.0</td>
      <td>1386.0</td>
      <td>38222.0</td>
      <td>4246.888889</td>
      <td>126.902448</td>
      <td>37.483934</td>
    </tr>
    <tr>
      <th>33</th>
      <td>3165.0</td>
      <td>순천향대학병원.한남오거리(3165.0)</td>
      <td>4114.0</td>
      <td>4288.0</td>
      <td>4730.0</td>
      <td>4858.0</td>
      <td>5438.0</td>
      <td>4928.0</td>
      <td>4357.0</td>
      <td>4291.0</td>
      <td>1118.0</td>
      <td>38122.0</td>
      <td>4235.777778</td>
      <td>127.006068</td>
      <td>37.535247</td>
    </tr>
    <tr>
      <th>34</th>
      <td>6015.0</td>
      <td>청량리역환승센타(6015.0)</td>
      <td>3825.0</td>
      <td>4379.0</td>
      <td>4522.0</td>
      <td>4708.0</td>
      <td>4912.0</td>
      <td>4638.0</td>
      <td>4344.0</td>
      <td>4444.0</td>
      <td>2276.0</td>
      <td>38048.0</td>
      <td>4227.555556</td>
      <td>127.045419</td>
      <td>37.580412</td>
    </tr>
    <tr>
      <th>35</th>
      <td>17185.0</td>
      <td>온수역(17185.0)</td>
      <td>3998.0</td>
      <td>4421.0</td>
      <td>4866.0</td>
      <td>4704.0</td>
      <td>4892.0</td>
      <td>5032.0</td>
      <td>4139.0</td>
      <td>4393.0</td>
      <td>1344.0</td>
      <td>37789.0</td>
      <td>4198.777778</td>
      <td>126.824709</td>
      <td>37.492961</td>
    </tr>
    <tr>
      <th>36</th>
      <td>21139.0</td>
      <td>관악구청(21139.0)</td>
      <td>4017.0</td>
      <td>4324.0</td>
      <td>4527.0</td>
      <td>4625.0</td>
      <td>4621.0</td>
      <td>4422.0</td>
      <td>4476.0</td>
      <td>4475.0</td>
      <td>1548.0</td>
      <td>37035.0</td>
      <td>4115.000000</td>
      <td>126.952320</td>
      <td>37.479535</td>
    </tr>
    <tr>
      <th>37</th>
      <td>10016.0</td>
      <td>쌍문역(10016.0)</td>
      <td>4228.0</td>
      <td>4504.0</td>
      <td>4573.0</td>
      <td>4463.0</td>
      <td>4572.0</td>
      <td>4366.0</td>
      <td>4115.0</td>
      <td>4240.0</td>
      <td>1537.0</td>
      <td>36598.0</td>
      <td>4066.444444</td>
      <td>127.034482</td>
      <td>37.648063</td>
    </tr>
    <tr>
      <th>38</th>
      <td>14012.0</td>
      <td>합정역(14012.0)</td>
      <td>3867.0</td>
      <td>4189.0</td>
      <td>4671.0</td>
      <td>4680.0</td>
      <td>5094.0</td>
      <td>4638.0</td>
      <td>3874.0</td>
      <td>3809.0</td>
      <td>1663.0</td>
      <td>36485.0</td>
      <td>4053.888889</td>
      <td>126.913721</td>
      <td>37.549515</td>
    </tr>
  </tbody>
</table>
</div>

#### Section 3.3 <a class="anchor" id="section_3_3"></a>

##### 승차 Top 39 DataFrame을 Excel에 저장

```python
#!pip install openpyxl
```

```python
top39_weekday.to_excel('Top39평일승차수.xlsx', index=False)
```

#### Chapter 4 <a class="anchor" id="chapter4"></a>

##### 2021년 1월 ~ 9월까지의 하차 데이터 합병

#### Section 4.1 <a class="anchor" id="section_4_1"></a>

##### 승차와 동일하게 진행

##### 이제 Top39평일하차수를 구해보겠습니다.

```python
# 1월 하차 평일

dropstop_0119 = busroute_0119.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0119 = pd.DataFrame(dropstop_0119)
drop_0119 = dropstop_0119.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0119.rename(columns={'승객수':'1월_평일하차수'},inplace = True)


# 2월 하차 평일

dropstop_0216 = busroute_0216.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0216 = pd.DataFrame(dropstop_0216)
drop_0216 = dropstop_0216.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0216.rename(columns={'승객수':'2월_평일하차수'},inplace = True)


# 3월 하차 평일

dropstop_0316 = busroute_0316.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0316 = pd.DataFrame(dropstop_0316)
drop_0316 = dropstop_0316.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0316.rename(columns={'승객수':'3월_평일하차수'},inplace = True)

# 4월 하차 평일

dropstop_0420 = busroute_0420.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0420 = pd.DataFrame(dropstop_0420)
drop_0420 = dropstop_0420.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0420.rename(columns={'승객수':'4월_평일하차수'},inplace = True)

# 5월 하차 평일

dropstop_0518 = busroute_0518.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0518 = pd.DataFrame(dropstop_0518)
drop_0518 = dropstop_0518.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0518.rename(columns={'승객수':'5월_평일하차수'},inplace = True)

# 6월 하차 평일

dropstop_0615 = busroute_0615.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0615 = pd.DataFrame(dropstop_0615)
drop_0615 = dropstop_0615.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0615.rename(columns={'승객수':'6월_평일하차수'},inplace = True)

# 7월 하차 평일

dropstop_0720 = busroute_0720.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0720 = pd.DataFrame(dropstop_0720)
drop_0720 = dropstop_0720.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0720.rename(columns={'승객수':'7월_평일하차수'},inplace = True)

# 8월 하차 평일

dropstop_0817 = busroute_0817.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0817 = pd.DataFrame(dropstop_0817)
drop_0817 = dropstop_0817.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0817.rename(columns={'승객수':'8월_평일하차수'},inplace = True)

# 9월 하차 평일

dropstop_0921 = busroute_0921.groupby(['하차_정류장ARS'])['승객수'].sum()
dropstop_0921 = pd.DataFrame(dropstop_0921)
drop_0921 = dropstop_0119.sort_values(by ='승객수',axis=0,ascending=False).reset_index()

drop_0921.rename(columns={'승객수':'9월_평일하차수'},inplace = True)



```

```python
getoff = pd.merge(drop_0119,drop_0216, how='outer')
getoff = pd.merge(getoff,drop_0316, how = 'outer')
getoff = pd.merge(getoff,drop_0420, how = 'outer')
getoff = pd.merge(getoff,drop_0518, how = 'outer')
getoff = pd.merge(getoff,drop_0615, how = 'outer')
getoff = pd.merge(getoff,drop_0720, how = 'outer')
getoff = pd.merge(getoff,drop_0817, how = 'outer')
getoff = pd.merge(getoff,drop_0921, how = 'outer')

getoff
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>하차_정류장ARS</th>
      <th>1월_평일하차수</th>
      <th>2월_평일하차수</th>
      <th>3월_평일하차수</th>
      <th>4월_평일하차수</th>
      <th>5월_평일하차수</th>
      <th>6월_평일하차수</th>
      <th>7월_평일하차수</th>
      <th>8월_평일하차수</th>
      <th>9월_평일하차수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21001.0</td>
      <td>10909.0</td>
      <td>11980.0</td>
      <td>12528.0</td>
      <td>12235.0</td>
      <td>12656.0</td>
      <td>12179.0</td>
      <td>10780.0</td>
      <td>11217.0</td>
      <td>10909.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17014.0</td>
      <td>8276.0</td>
      <td>8909.0</td>
      <td>9080.0</td>
      <td>9063.0</td>
      <td>9460.0</td>
      <td>9182.0</td>
      <td>8497.0</td>
      <td>8536.0</td>
      <td>8276.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9012.0</td>
      <td>7950.0</td>
      <td>8632.0</td>
      <td>9152.0</td>
      <td>9379.0</td>
      <td>10079.0</td>
      <td>9134.0</td>
      <td>8465.0</td>
      <td>8445.0</td>
      <td>7950.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9004.0</td>
      <td>7754.0</td>
      <td>8170.0</td>
      <td>8590.0</td>
      <td>8499.0</td>
      <td>9287.0</td>
      <td>8391.0</td>
      <td>8238.0</td>
      <td>8129.0</td>
      <td>7754.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21117.0</td>
      <td>7146.0</td>
      <td>7795.0</td>
      <td>7839.0</td>
      <td>8042.0</td>
      <td>8862.0</td>
      <td>8145.0</td>
      <td>7657.0</td>
      <td>7579.0</td>
      <td>7146.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>12656</th>
      <td>8334.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12657</th>
      <td>23964.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12658</th>
      <td>23074.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12659</th>
      <td>23081.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12660</th>
      <td>16156.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>12661 rows × 10 columns</p>
</div>

```python
getoff["정류장_승객수총합"] = getoff.loc[:,'1월_평일하차수':'9월_평일하차수'].sum(axis=1)
getoff["정류장_승객수평균"] = getoff.loc[:,'1월_평일하차수':'9월_평일하차수'].mean(axis=1)

getoff_weekday = getoff.sort_values(by ='정류장_승객수총합',axis=0,ascending=False).head(39).reset_index(drop=True)

getoff_weekday["정류장명"] = np.nan

for idx in getoff_weekday.index:
    stop_name =getoff_weekday.loc[idx,'하차_정류장ARS']

    df_ex = busroute_0119[busroute_0119['하차_정류장ARS'] == stop_name]

    ts = df_ex.iloc[0]['하차_정류장ARS'].astype(np.string_).decode('UTF-8')
    getoff_weekday.loc[idx,'정류장명'] = df_ex.iloc[0]['하차_정류장명'] +"(" + ts + ")"

getoff_weekday
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>하차_정류장ARS</th>
      <th>1월_평일하차수</th>
      <th>2월_평일하차수</th>
      <th>3월_평일하차수</th>
      <th>4월_평일하차수</th>
      <th>5월_평일하차수</th>
      <th>6월_평일하차수</th>
      <th>7월_평일하차수</th>
      <th>8월_평일하차수</th>
      <th>9월_평일하차수</th>
      <th>정류장_승객수총합</th>
      <th>정류장_승객수평균</th>
      <th>정류장명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21001.0</td>
      <td>10909.0</td>
      <td>11980.0</td>
      <td>12528.0</td>
      <td>12235.0</td>
      <td>12656.0</td>
      <td>12179.0</td>
      <td>10780.0</td>
      <td>11217.0</td>
      <td>10909.0</td>
      <td>105393.0</td>
      <td>11710.333333</td>
      <td>구로디지털단지역(21001.0)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17014.0</td>
      <td>8276.0</td>
      <td>8909.0</td>
      <td>9080.0</td>
      <td>9063.0</td>
      <td>9460.0</td>
      <td>9182.0</td>
      <td>8497.0</td>
      <td>8536.0</td>
      <td>8276.0</td>
      <td>79279.0</td>
      <td>8808.777778</td>
      <td>구로디지털단지역환승센터(17014.0)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9012.0</td>
      <td>7950.0</td>
      <td>8632.0</td>
      <td>9152.0</td>
      <td>9379.0</td>
      <td>10079.0</td>
      <td>9134.0</td>
      <td>8465.0</td>
      <td>8445.0</td>
      <td>7950.0</td>
      <td>79186.0</td>
      <td>8798.444444</td>
      <td>미아사거리역(9012.0)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9004.0</td>
      <td>7754.0</td>
      <td>8170.0</td>
      <td>8590.0</td>
      <td>8499.0</td>
      <td>9287.0</td>
      <td>8391.0</td>
      <td>8238.0</td>
      <td>8129.0</td>
      <td>7754.0</td>
      <td>74812.0</td>
      <td>8312.444444</td>
      <td>수유역.강북구청(9004.0)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22020.0</td>
      <td>7142.0</td>
      <td>7754.0</td>
      <td>8475.0</td>
      <td>8479.0</td>
      <td>9619.0</td>
      <td>8482.0</td>
      <td>7394.0</td>
      <td>7367.0</td>
      <td>7142.0</td>
      <td>71854.0</td>
      <td>7983.777778</td>
      <td>고속터미널(22020.0)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>21117.0</td>
      <td>7146.0</td>
      <td>7795.0</td>
      <td>7839.0</td>
      <td>8042.0</td>
      <td>8862.0</td>
      <td>8145.0</td>
      <td>7657.0</td>
      <td>7579.0</td>
      <td>7146.0</td>
      <td>70211.0</td>
      <td>7801.222222</td>
      <td>신림사거리.신림역(21117.0)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20114.0</td>
      <td>6851.0</td>
      <td>7673.0</td>
      <td>8132.0</td>
      <td>8276.0</td>
      <td>8712.0</td>
      <td>8168.0</td>
      <td>7452.0</td>
      <td>7279.0</td>
      <td>6851.0</td>
      <td>69394.0</td>
      <td>7710.444444</td>
      <td>노량진역(20114.0)</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3165.0</td>
      <td>6155.0</td>
      <td>6106.0</td>
      <td>7265.0</td>
      <td>7285.0</td>
      <td>8126.0</td>
      <td>7405.0</td>
      <td>6463.0</td>
      <td>6587.0</td>
      <td>6155.0</td>
      <td>61547.0</td>
      <td>6838.555556</td>
      <td>순천향대학병원.한남오거리(3165.0)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>17002.0</td>
      <td>6196.0</td>
      <td>6706.0</td>
      <td>6885.0</td>
      <td>6994.0</td>
      <td>7344.0</td>
      <td>6939.0</td>
      <td>6301.0</td>
      <td>6451.0</td>
      <td>6196.0</td>
      <td>60012.0</td>
      <td>6668.000000</td>
      <td>신도림역(17002.0)</td>
    </tr>
    <tr>
      <th>9</th>
      <td>6015.0</td>
      <td>5719.0</td>
      <td>6341.0</td>
      <td>6900.0</td>
      <td>7155.0</td>
      <td>7287.0</td>
      <td>6941.0</td>
      <td>6636.0</td>
      <td>6395.0</td>
      <td>5719.0</td>
      <td>59093.0</td>
      <td>6565.888889</td>
      <td>청량리역환승센타(6015.0)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>22019.0</td>
      <td>5121.0</td>
      <td>6084.0</td>
      <td>6582.0</td>
      <td>6680.0</td>
      <td>7324.0</td>
      <td>7066.0</td>
      <td>6441.0</td>
      <td>6405.0</td>
      <td>5121.0</td>
      <td>56824.0</td>
      <td>6313.777778</td>
      <td>고속터미널(22019.0)</td>
    </tr>
    <tr>
      <th>11</th>
      <td>21252.0</td>
      <td>5371.0</td>
      <td>5970.0</td>
      <td>6616.0</td>
      <td>6909.0</td>
      <td>6621.0</td>
      <td>6549.0</td>
      <td>6102.0</td>
      <td>6248.0</td>
      <td>5371.0</td>
      <td>55757.0</td>
      <td>6195.222222</td>
      <td>서울대입구역(21252.0)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>10015.0</td>
      <td>5684.0</td>
      <td>6231.0</td>
      <td>6396.0</td>
      <td>6467.0</td>
      <td>6894.0</td>
      <td>6200.0</td>
      <td>5889.0</td>
      <td>5923.0</td>
      <td>5684.0</td>
      <td>55368.0</td>
      <td>6152.000000</td>
      <td>쌍문역(10015.0)</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9013.0</td>
      <td>5630.0</td>
      <td>6118.0</td>
      <td>6257.0</td>
      <td>6413.0</td>
      <td>6685.0</td>
      <td>6182.0</td>
      <td>5976.0</td>
      <td>6207.0</td>
      <td>5630.0</td>
      <td>55098.0</td>
      <td>6122.000000</td>
      <td>수유(강북구청)역(9013.0)</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14016.0</td>
      <td>5700.0</td>
      <td>6376.0</td>
      <td>6769.0</td>
      <td>6806.0</td>
      <td>5874.0</td>
      <td>5925.0</td>
      <td>4818.0</td>
      <td>5069.0</td>
      <td>5700.0</td>
      <td>53037.0</td>
      <td>5893.000000</td>
      <td>홍대입구역(14016.0)</td>
    </tr>
    <tr>
      <th>15</th>
      <td>22011.0</td>
      <td>5238.0</td>
      <td>5844.0</td>
      <td>6120.0</td>
      <td>6042.0</td>
      <td>6909.0</td>
      <td>6273.0</td>
      <td>5413.0</td>
      <td>5653.0</td>
      <td>5238.0</td>
      <td>52730.0</td>
      <td>5858.888889</td>
      <td>지하철2호선강남역(22011.0)</td>
    </tr>
    <tr>
      <th>16</th>
      <td>9011.0</td>
      <td>5112.0</td>
      <td>5924.0</td>
      <td>6149.0</td>
      <td>6016.0</td>
      <td>6394.0</td>
      <td>6065.0</td>
      <td>5880.0</td>
      <td>5646.0</td>
      <td>5112.0</td>
      <td>52298.0</td>
      <td>5810.888889</td>
      <td>미아사거리역(9011.0)</td>
    </tr>
    <tr>
      <th>17</th>
      <td>21377.0</td>
      <td>5025.0</td>
      <td>5631.0</td>
      <td>5631.0</td>
      <td>5780.0</td>
      <td>6060.0</td>
      <td>5526.0</td>
      <td>5094.0</td>
      <td>5013.0</td>
      <td>5025.0</td>
      <td>48785.0</td>
      <td>5420.555556</td>
      <td>신림역2번출구(21377.0)</td>
    </tr>
    <tr>
      <th>18</th>
      <td>24132.0</td>
      <td>5168.0</td>
      <td>5616.0</td>
      <td>5600.0</td>
      <td>5453.0</td>
      <td>5809.0</td>
      <td>5495.0</td>
      <td>5054.0</td>
      <td>5006.0</td>
      <td>5168.0</td>
      <td>48369.0</td>
      <td>5374.333333</td>
      <td>잠실역8번출구(24132.0)</td>
    </tr>
    <tr>
      <th>19</th>
      <td>21916.0</td>
      <td>4950.0</td>
      <td>5400.0</td>
      <td>5506.0</td>
      <td>5426.0</td>
      <td>5765.0</td>
      <td>5518.0</td>
      <td>5194.0</td>
      <td>5259.0</td>
      <td>4950.0</td>
      <td>47968.0</td>
      <td>5329.777778</td>
      <td>신림역4번출구(21916.0)</td>
    </tr>
    <tr>
      <th>20</th>
      <td>8010.0</td>
      <td>4682.0</td>
      <td>4849.0</td>
      <td>5492.0</td>
      <td>5646.0</td>
      <td>5956.0</td>
      <td>5611.0</td>
      <td>5084.0</td>
      <td>5111.0</td>
      <td>4682.0</td>
      <td>47113.0</td>
      <td>5234.777778</td>
      <td>삼선교.한성대학교.조소앙활동터(8010.0)</td>
    </tr>
    <tr>
      <th>21</th>
      <td>9277.0</td>
      <td>4588.0</td>
      <td>4834.0</td>
      <td>5071.0</td>
      <td>5081.0</td>
      <td>5482.0</td>
      <td>5125.0</td>
      <td>4858.0</td>
      <td>4898.0</td>
      <td>4588.0</td>
      <td>44525.0</td>
      <td>4947.222222</td>
      <td>롯데백화점미아점(9277.0)</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22012.0</td>
      <td>4434.0</td>
      <td>4842.0</td>
      <td>5073.0</td>
      <td>4839.0</td>
      <td>5593.0</td>
      <td>4900.0</td>
      <td>4788.0</td>
      <td>4840.0</td>
      <td>4434.0</td>
      <td>43743.0</td>
      <td>4860.333333</td>
      <td>지하철2호선강남역(22012.0)</td>
    </tr>
    <tr>
      <th>23</th>
      <td>12381.0</td>
      <td>4367.0</td>
      <td>4910.0</td>
      <td>4891.0</td>
      <td>4917.0</td>
      <td>5177.0</td>
      <td>5096.0</td>
      <td>4540.0</td>
      <td>4778.0</td>
      <td>4367.0</td>
      <td>43043.0</td>
      <td>4782.555556</td>
      <td>녹번역(12381.0)</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2006.0</td>
      <td>4238.0</td>
      <td>4651.0</td>
      <td>4923.0</td>
      <td>5028.0</td>
      <td>5620.0</td>
      <td>5068.0</td>
      <td>4437.0</td>
      <td>4590.0</td>
      <td>4238.0</td>
      <td>42793.0</td>
      <td>4754.777778</td>
      <td>서울역버스환승센터(2006.0)</td>
    </tr>
    <tr>
      <th>25</th>
      <td>19156.0</td>
      <td>4404.0</td>
      <td>4799.0</td>
      <td>5026.0</td>
      <td>5020.0</td>
      <td>5243.0</td>
      <td>5057.0</td>
      <td>4418.0</td>
      <td>4419.0</td>
      <td>4404.0</td>
      <td>42790.0</td>
      <td>4754.444444</td>
      <td>여의도역(19156.0)</td>
    </tr>
    <tr>
      <th>26</th>
      <td>14011.0</td>
      <td>4644.0</td>
      <td>5057.0</td>
      <td>5599.0</td>
      <td>5830.0</td>
      <td>4735.0</td>
      <td>4367.0</td>
      <td>3683.0</td>
      <td>3780.0</td>
      <td>4644.0</td>
      <td>42339.0</td>
      <td>4704.333333</td>
      <td>합정역(14011.0)</td>
    </tr>
    <tr>
      <th>27</th>
      <td>8007.0</td>
      <td>4194.0</td>
      <td>4574.0</td>
      <td>4818.0</td>
      <td>4893.0</td>
      <td>5425.0</td>
      <td>4977.0</td>
      <td>4458.0</td>
      <td>4662.0</td>
      <td>4194.0</td>
      <td>42195.0</td>
      <td>4688.333333</td>
      <td>돈암사거리.성신여대입구(8007.0)</td>
    </tr>
    <tr>
      <th>28</th>
      <td>17184.0</td>
      <td>4081.0</td>
      <td>4445.0</td>
      <td>5060.0</td>
      <td>4902.0</td>
      <td>5348.0</td>
      <td>5451.0</td>
      <td>4323.0</td>
      <td>4482.0</td>
      <td>4081.0</td>
      <td>42173.0</td>
      <td>4685.888889</td>
      <td>온수역(17184.0)</td>
    </tr>
    <tr>
      <th>29</th>
      <td>22015.0</td>
      <td>4162.0</td>
      <td>4362.0</td>
      <td>4918.0</td>
      <td>5032.0</td>
      <td>5406.0</td>
      <td>4933.0</td>
      <td>4442.0</td>
      <td>4418.0</td>
      <td>4162.0</td>
      <td>41835.0</td>
      <td>4648.333333</td>
      <td>신사역.푸른저축은행(22015.0)</td>
    </tr>
    <tr>
      <th>30</th>
      <td>19112.0</td>
      <td>4032.0</td>
      <td>4675.0</td>
      <td>4832.0</td>
      <td>4650.0</td>
      <td>5252.0</td>
      <td>4817.0</td>
      <td>4594.0</td>
      <td>4501.0</td>
      <td>4032.0</td>
      <td>41385.0</td>
      <td>4598.333333</td>
      <td>경방타임스퀘어.신세계백화점(19112.0)</td>
    </tr>
    <tr>
      <th>31</th>
      <td>20166.0</td>
      <td>4100.0</td>
      <td>4454.0</td>
      <td>4880.0</td>
      <td>5030.0</td>
      <td>5192.0</td>
      <td>4817.0</td>
      <td>4280.0</td>
      <td>4364.0</td>
      <td>4100.0</td>
      <td>41217.0</td>
      <td>4579.666667</td>
      <td>숭실대입구역(20166.0)</td>
    </tr>
    <tr>
      <th>32</th>
      <td>14015.0</td>
      <td>4397.0</td>
      <td>4993.0</td>
      <td>5121.0</td>
      <td>5097.0</td>
      <td>4810.0</td>
      <td>4287.0</td>
      <td>3884.0</td>
      <td>4224.0</td>
      <td>4397.0</td>
      <td>41210.0</td>
      <td>4578.888889</td>
      <td>홍대입구역(14015.0)</td>
    </tr>
    <tr>
      <th>33</th>
      <td>24138.0</td>
      <td>4259.0</td>
      <td>4620.0</td>
      <td>4686.0</td>
      <td>4606.0</td>
      <td>4979.0</td>
      <td>4573.0</td>
      <td>4220.0</td>
      <td>4296.0</td>
      <td>4259.0</td>
      <td>40498.0</td>
      <td>4499.777778</td>
      <td>잠실역.롯데월드(24138.0)</td>
    </tr>
    <tr>
      <th>34</th>
      <td>3009.0</td>
      <td>4075.0</td>
      <td>4401.0</td>
      <td>4788.0</td>
      <td>4674.0</td>
      <td>5109.0</td>
      <td>4803.0</td>
      <td>4140.0</td>
      <td>4368.0</td>
      <td>4075.0</td>
      <td>40433.0</td>
      <td>4492.555556</td>
      <td>숙대입구역(3009.0)</td>
    </tr>
    <tr>
      <th>35</th>
      <td>8008.0</td>
      <td>3984.0</td>
      <td>4310.0</td>
      <td>4722.0</td>
      <td>4672.0</td>
      <td>4997.0</td>
      <td>4741.0</td>
      <td>4219.0</td>
      <td>4354.0</td>
      <td>3984.0</td>
      <td>39983.0</td>
      <td>4442.555556</td>
      <td>돈암사거리.성신여대입구(8008.0)</td>
    </tr>
    <tr>
      <th>36</th>
      <td>1037.0</td>
      <td>4067.0</td>
      <td>4145.0</td>
      <td>4719.0</td>
      <td>4648.0</td>
      <td>4737.0</td>
      <td>4344.0</td>
      <td>4248.0</td>
      <td>4217.0</td>
      <td>4067.0</td>
      <td>39192.0</td>
      <td>4354.666667</td>
      <td>동대문(흥인지문)(1037.0)</td>
    </tr>
    <tr>
      <th>37</th>
      <td>19006.0</td>
      <td>3893.0</td>
      <td>4210.0</td>
      <td>4656.0</td>
      <td>4576.0</td>
      <td>5059.0</td>
      <td>4829.0</td>
      <td>3864.0</td>
      <td>4066.0</td>
      <td>3893.0</td>
      <td>39046.0</td>
      <td>4338.444444</td>
      <td>영등포역(19006.0)</td>
    </tr>
    <tr>
      <th>38</th>
      <td>12184.0</td>
      <td>3825.0</td>
      <td>4236.0</td>
      <td>4549.0</td>
      <td>4514.0</td>
      <td>4796.0</td>
      <td>4556.0</td>
      <td>4260.0</td>
      <td>4376.0</td>
      <td>3825.0</td>
      <td>38937.0</td>
      <td>4326.333333</td>
      <td>연신내역.로데오거리(12184.0)</td>
    </tr>
  </tbody>
</table>
</div>

```python
bus_stop = pd.read_csv('C:/jupyter_data/서울시버스정류소좌표데이터(2021.01.14.).csv')
bus_stop.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>표준ID</th>
      <th>ARS-ID</th>
      <th>정류소명</th>
      <th>X좌표</th>
      <th>Y좌표</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100000001</td>
      <td>1001</td>
      <td>종로2가사거리</td>
      <td>126.987786</td>
      <td>37.569764</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100000002</td>
      <td>1002</td>
      <td>창경궁.서울대학교병원</td>
      <td>126.996520</td>
      <td>37.579179</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100000003</td>
      <td>1003</td>
      <td>명륜3가.성대입구</td>
      <td>126.998290</td>
      <td>37.582709</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100000004</td>
      <td>1004</td>
      <td>종로2가.삼일교</td>
      <td>126.987507</td>
      <td>37.568582</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100000005</td>
      <td>1005</td>
      <td>혜화동로터리.여운형활동터</td>
      <td>127.001694</td>
      <td>37.586230</td>
    </tr>
  </tbody>
</table>
</div>

```python
getoff_weekday["X좌표"] = np.nan
getoff_weekday["Y좌표"] = np.nan

for idx in getoff_weekday.index:
    stop_name = getoff_weekday.loc[idx,'하차_정류장ARS']

    df_ex = bus_stop[bus_stop['ARS-ID'] == stop_name]

    getoff_weekday.loc[idx,'X좌표'] = df_ex.iloc[0]['X좌표']
    getoff_weekday.loc[idx,'Y좌표'] = df_ex.iloc[0]['Y좌표']


getoff_weekday = getoff_weekday.dropna(axis=0)
getoff_weekday = getoff_weekday.reindex(columns=['하차_정류장ARS','정류장명','1월_평일하차수', '2월_평일하차수', '3월_평일하차수' ,
                                               '4월_평일하차수', '5월_평일하차수','6월_평일하차수','7월_평일하차수', '8월_평일하차수',
                                               '9월_평일하차수','정류장_승객수총합', '정류장_승객수평균', 'X좌표', 'Y좌표' ])
getoff_weekday
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>하차_정류장ARS</th>
      <th>정류장명</th>
      <th>1월_평일하차수</th>
      <th>2월_평일하차수</th>
      <th>3월_평일하차수</th>
      <th>4월_평일하차수</th>
      <th>5월_평일하차수</th>
      <th>6월_평일하차수</th>
      <th>7월_평일하차수</th>
      <th>8월_평일하차수</th>
      <th>9월_평일하차수</th>
      <th>정류장_승객수총합</th>
      <th>정류장_승객수평균</th>
      <th>X좌표</th>
      <th>Y좌표</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21001.0</td>
      <td>구로디지털단지역(21001.0)</td>
      <td>10909.0</td>
      <td>11980.0</td>
      <td>12528.0</td>
      <td>12235.0</td>
      <td>12656.0</td>
      <td>12179.0</td>
      <td>10780.0</td>
      <td>11217.0</td>
      <td>10909.0</td>
      <td>105393.0</td>
      <td>11710.333333</td>
      <td>126.902448</td>
      <td>37.483934</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17014.0</td>
      <td>구로디지털단지역환승센터(17014.0)</td>
      <td>8276.0</td>
      <td>8909.0</td>
      <td>9080.0</td>
      <td>9063.0</td>
      <td>9460.0</td>
      <td>9182.0</td>
      <td>8497.0</td>
      <td>8536.0</td>
      <td>8276.0</td>
      <td>79279.0</td>
      <td>8808.777778</td>
      <td>126.902006</td>
      <td>37.484607</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9012.0</td>
      <td>미아사거리역(9012.0)</td>
      <td>7950.0</td>
      <td>8632.0</td>
      <td>9152.0</td>
      <td>9379.0</td>
      <td>10079.0</td>
      <td>9134.0</td>
      <td>8465.0</td>
      <td>8445.0</td>
      <td>7950.0</td>
      <td>79186.0</td>
      <td>8798.444444</td>
      <td>127.030240</td>
      <td>37.612897</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9004.0</td>
      <td>수유역.강북구청(9004.0)</td>
      <td>7754.0</td>
      <td>8170.0</td>
      <td>8590.0</td>
      <td>8499.0</td>
      <td>9287.0</td>
      <td>8391.0</td>
      <td>8238.0</td>
      <td>8129.0</td>
      <td>7754.0</td>
      <td>74812.0</td>
      <td>8312.444444</td>
      <td>127.025183</td>
      <td>37.637522</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22020.0</td>
      <td>고속터미널(22020.0)</td>
      <td>7142.0</td>
      <td>7754.0</td>
      <td>8475.0</td>
      <td>8479.0</td>
      <td>9619.0</td>
      <td>8482.0</td>
      <td>7394.0</td>
      <td>7367.0</td>
      <td>7142.0</td>
      <td>71854.0</td>
      <td>7983.777778</td>
      <td>127.003841</td>
      <td>37.505637</td>
    </tr>
    <tr>
      <th>5</th>
      <td>21117.0</td>
      <td>신림사거리.신림역(21117.0)</td>
      <td>7146.0</td>
      <td>7795.0</td>
      <td>7839.0</td>
      <td>8042.0</td>
      <td>8862.0</td>
      <td>8145.0</td>
      <td>7657.0</td>
      <td>7579.0</td>
      <td>7146.0</td>
      <td>70211.0</td>
      <td>7801.222222</td>
      <td>126.927447</td>
      <td>37.483857</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20114.0</td>
      <td>노량진역(20114.0)</td>
      <td>6851.0</td>
      <td>7673.0</td>
      <td>8132.0</td>
      <td>8276.0</td>
      <td>8712.0</td>
      <td>8168.0</td>
      <td>7452.0</td>
      <td>7279.0</td>
      <td>6851.0</td>
      <td>69394.0</td>
      <td>7710.444444</td>
      <td>126.941737</td>
      <td>37.513598</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3165.0</td>
      <td>순천향대학병원.한남오거리(3165.0)</td>
      <td>6155.0</td>
      <td>6106.0</td>
      <td>7265.0</td>
      <td>7285.0</td>
      <td>8126.0</td>
      <td>7405.0</td>
      <td>6463.0</td>
      <td>6587.0</td>
      <td>6155.0</td>
      <td>61547.0</td>
      <td>6838.555556</td>
      <td>127.006068</td>
      <td>37.535247</td>
    </tr>
    <tr>
      <th>8</th>
      <td>17002.0</td>
      <td>신도림역(17002.0)</td>
      <td>6196.0</td>
      <td>6706.0</td>
      <td>6885.0</td>
      <td>6994.0</td>
      <td>7344.0</td>
      <td>6939.0</td>
      <td>6301.0</td>
      <td>6451.0</td>
      <td>6196.0</td>
      <td>60012.0</td>
      <td>6668.000000</td>
      <td>126.888472</td>
      <td>37.509100</td>
    </tr>
    <tr>
      <th>9</th>
      <td>6015.0</td>
      <td>청량리역환승센타(6015.0)</td>
      <td>5719.0</td>
      <td>6341.0</td>
      <td>6900.0</td>
      <td>7155.0</td>
      <td>7287.0</td>
      <td>6941.0</td>
      <td>6636.0</td>
      <td>6395.0</td>
      <td>5719.0</td>
      <td>59093.0</td>
      <td>6565.888889</td>
      <td>127.045419</td>
      <td>37.580412</td>
    </tr>
    <tr>
      <th>10</th>
      <td>22019.0</td>
      <td>고속터미널(22019.0)</td>
      <td>5121.0</td>
      <td>6084.0</td>
      <td>6582.0</td>
      <td>6680.0</td>
      <td>7324.0</td>
      <td>7066.0</td>
      <td>6441.0</td>
      <td>6405.0</td>
      <td>5121.0</td>
      <td>56824.0</td>
      <td>6313.777778</td>
      <td>127.005263</td>
      <td>37.506335</td>
    </tr>
    <tr>
      <th>11</th>
      <td>21252.0</td>
      <td>서울대입구역(21252.0)</td>
      <td>5371.0</td>
      <td>5970.0</td>
      <td>6616.0</td>
      <td>6909.0</td>
      <td>6621.0</td>
      <td>6549.0</td>
      <td>6102.0</td>
      <td>6248.0</td>
      <td>5371.0</td>
      <td>55757.0</td>
      <td>6195.222222</td>
      <td>126.952578</td>
      <td>37.479945</td>
    </tr>
    <tr>
      <th>12</th>
      <td>10015.0</td>
      <td>쌍문역(10015.0)</td>
      <td>5684.0</td>
      <td>6231.0</td>
      <td>6396.0</td>
      <td>6467.0</td>
      <td>6894.0</td>
      <td>6200.0</td>
      <td>5889.0</td>
      <td>5923.0</td>
      <td>5684.0</td>
      <td>55368.0</td>
      <td>6152.000000</td>
      <td>127.034752</td>
      <td>37.648824</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9013.0</td>
      <td>수유(강북구청)역(9013.0)</td>
      <td>5630.0</td>
      <td>6118.0</td>
      <td>6257.0</td>
      <td>6413.0</td>
      <td>6685.0</td>
      <td>6182.0</td>
      <td>5976.0</td>
      <td>6207.0</td>
      <td>5630.0</td>
      <td>55098.0</td>
      <td>6122.000000</td>
      <td>127.026037</td>
      <td>37.638520</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14016.0</td>
      <td>홍대입구역(14016.0)</td>
      <td>5700.0</td>
      <td>6376.0</td>
      <td>6769.0</td>
      <td>6806.0</td>
      <td>5874.0</td>
      <td>5925.0</td>
      <td>4818.0</td>
      <td>5069.0</td>
      <td>5700.0</td>
      <td>53037.0</td>
      <td>5893.000000</td>
      <td>126.924522</td>
      <td>37.557534</td>
    </tr>
    <tr>
      <th>15</th>
      <td>22011.0</td>
      <td>지하철2호선강남역(22011.0)</td>
      <td>5238.0</td>
      <td>5844.0</td>
      <td>6120.0</td>
      <td>6042.0</td>
      <td>6909.0</td>
      <td>6273.0</td>
      <td>5413.0</td>
      <td>5653.0</td>
      <td>5238.0</td>
      <td>52730.0</td>
      <td>5858.888889</td>
      <td>127.025728</td>
      <td>37.501609</td>
    </tr>
    <tr>
      <th>16</th>
      <td>9011.0</td>
      <td>미아사거리역(9011.0)</td>
      <td>5112.0</td>
      <td>5924.0</td>
      <td>6149.0</td>
      <td>6016.0</td>
      <td>6394.0</td>
      <td>6065.0</td>
      <td>5880.0</td>
      <td>5646.0</td>
      <td>5112.0</td>
      <td>52298.0</td>
      <td>5810.888889</td>
      <td>127.030002</td>
      <td>37.613765</td>
    </tr>
    <tr>
      <th>17</th>
      <td>21377.0</td>
      <td>신림역2번출구(21377.0)</td>
      <td>5025.0</td>
      <td>5631.0</td>
      <td>5631.0</td>
      <td>5780.0</td>
      <td>6060.0</td>
      <td>5526.0</td>
      <td>5094.0</td>
      <td>5013.0</td>
      <td>5025.0</td>
      <td>48785.0</td>
      <td>5420.555556</td>
      <td>126.929817</td>
      <td>37.483318</td>
    </tr>
    <tr>
      <th>18</th>
      <td>24132.0</td>
      <td>잠실역8번출구(24132.0)</td>
      <td>5168.0</td>
      <td>5616.0</td>
      <td>5600.0</td>
      <td>5453.0</td>
      <td>5809.0</td>
      <td>5495.0</td>
      <td>5054.0</td>
      <td>5006.0</td>
      <td>5168.0</td>
      <td>48369.0</td>
      <td>5374.333333</td>
      <td>127.101521</td>
      <td>37.513798</td>
    </tr>
    <tr>
      <th>19</th>
      <td>21916.0</td>
      <td>신림역4번출구(21916.0)</td>
      <td>4950.0</td>
      <td>5400.0</td>
      <td>5506.0</td>
      <td>5426.0</td>
      <td>5765.0</td>
      <td>5518.0</td>
      <td>5194.0</td>
      <td>5259.0</td>
      <td>4950.0</td>
      <td>47968.0</td>
      <td>5329.777778</td>
      <td>126.929020</td>
      <td>37.484055</td>
    </tr>
    <tr>
      <th>20</th>
      <td>8010.0</td>
      <td>삼선교.한성대학교.조소앙활동터(8010.0)</td>
      <td>4682.0</td>
      <td>4849.0</td>
      <td>5492.0</td>
      <td>5646.0</td>
      <td>5956.0</td>
      <td>5611.0</td>
      <td>5084.0</td>
      <td>5111.0</td>
      <td>4682.0</td>
      <td>47113.0</td>
      <td>5234.777778</td>
      <td>127.008364</td>
      <td>37.589327</td>
    </tr>
    <tr>
      <th>21</th>
      <td>9277.0</td>
      <td>롯데백화점미아점(9277.0)</td>
      <td>4588.0</td>
      <td>4834.0</td>
      <td>5071.0</td>
      <td>5081.0</td>
      <td>5482.0</td>
      <td>5125.0</td>
      <td>4858.0</td>
      <td>4898.0</td>
      <td>4588.0</td>
      <td>44525.0</td>
      <td>4947.222222</td>
      <td>127.030862</td>
      <td>37.614651</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22012.0</td>
      <td>지하철2호선강남역(22012.0)</td>
      <td>4434.0</td>
      <td>4842.0</td>
      <td>5073.0</td>
      <td>4839.0</td>
      <td>5593.0</td>
      <td>4900.0</td>
      <td>4788.0</td>
      <td>4840.0</td>
      <td>4434.0</td>
      <td>43743.0</td>
      <td>4860.333333</td>
      <td>127.026418</td>
      <td>37.500757</td>
    </tr>
    <tr>
      <th>23</th>
      <td>12381.0</td>
      <td>녹번역(12381.0)</td>
      <td>4367.0</td>
      <td>4910.0</td>
      <td>4891.0</td>
      <td>4917.0</td>
      <td>5177.0</td>
      <td>5096.0</td>
      <td>4540.0</td>
      <td>4778.0</td>
      <td>4367.0</td>
      <td>43043.0</td>
      <td>4782.555556</td>
      <td>126.934804</td>
      <td>37.600835</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2006.0</td>
      <td>서울역버스환승센터(2006.0)</td>
      <td>4238.0</td>
      <td>4651.0</td>
      <td>4923.0</td>
      <td>5028.0</td>
      <td>5620.0</td>
      <td>5068.0</td>
      <td>4437.0</td>
      <td>4590.0</td>
      <td>4238.0</td>
      <td>42793.0</td>
      <td>4754.777778</td>
      <td>126.972773</td>
      <td>37.555475</td>
    </tr>
    <tr>
      <th>25</th>
      <td>19156.0</td>
      <td>여의도역(19156.0)</td>
      <td>4404.0</td>
      <td>4799.0</td>
      <td>5026.0</td>
      <td>5020.0</td>
      <td>5243.0</td>
      <td>5057.0</td>
      <td>4418.0</td>
      <td>4419.0</td>
      <td>4404.0</td>
      <td>42790.0</td>
      <td>4754.444444</td>
      <td>126.924659</td>
      <td>37.521449</td>
    </tr>
    <tr>
      <th>26</th>
      <td>14011.0</td>
      <td>합정역(14011.0)</td>
      <td>4644.0</td>
      <td>5057.0</td>
      <td>5599.0</td>
      <td>5830.0</td>
      <td>4735.0</td>
      <td>4367.0</td>
      <td>3683.0</td>
      <td>3780.0</td>
      <td>4644.0</td>
      <td>42339.0</td>
      <td>4704.333333</td>
      <td>126.912836</td>
      <td>37.548845</td>
    </tr>
    <tr>
      <th>27</th>
      <td>8007.0</td>
      <td>돈암사거리.성신여대입구(8007.0)</td>
      <td>4194.0</td>
      <td>4574.0</td>
      <td>4818.0</td>
      <td>4893.0</td>
      <td>5425.0</td>
      <td>4977.0</td>
      <td>4458.0</td>
      <td>4662.0</td>
      <td>4194.0</td>
      <td>42195.0</td>
      <td>4688.333333</td>
      <td>127.018087</td>
      <td>37.593775</td>
    </tr>
    <tr>
      <th>28</th>
      <td>17184.0</td>
      <td>온수역(17184.0)</td>
      <td>4081.0</td>
      <td>4445.0</td>
      <td>5060.0</td>
      <td>4902.0</td>
      <td>5348.0</td>
      <td>5451.0</td>
      <td>4323.0</td>
      <td>4482.0</td>
      <td>4081.0</td>
      <td>42173.0</td>
      <td>4685.888889</td>
      <td>126.823795</td>
      <td>37.492778</td>
    </tr>
    <tr>
      <th>29</th>
      <td>22015.0</td>
      <td>신사역.푸른저축은행(22015.0)</td>
      <td>4162.0</td>
      <td>4362.0</td>
      <td>4918.0</td>
      <td>5032.0</td>
      <td>5406.0</td>
      <td>4933.0</td>
      <td>4442.0</td>
      <td>4418.0</td>
      <td>4162.0</td>
      <td>41835.0</td>
      <td>4648.333333</td>
      <td>127.019844</td>
      <td>37.514627</td>
    </tr>
    <tr>
      <th>30</th>
      <td>19112.0</td>
      <td>경방타임스퀘어.신세계백화점(19112.0)</td>
      <td>4032.0</td>
      <td>4675.0</td>
      <td>4832.0</td>
      <td>4650.0</td>
      <td>5252.0</td>
      <td>4817.0</td>
      <td>4594.0</td>
      <td>4501.0</td>
      <td>4032.0</td>
      <td>41385.0</td>
      <td>4598.333333</td>
      <td>126.906191</td>
      <td>37.517492</td>
    </tr>
    <tr>
      <th>31</th>
      <td>20166.0</td>
      <td>숭실대입구역(20166.0)</td>
      <td>4100.0</td>
      <td>4454.0</td>
      <td>4880.0</td>
      <td>5030.0</td>
      <td>5192.0</td>
      <td>4817.0</td>
      <td>4280.0</td>
      <td>4364.0</td>
      <td>4100.0</td>
      <td>41217.0</td>
      <td>4579.666667</td>
      <td>126.953594</td>
      <td>37.496385</td>
    </tr>
    <tr>
      <th>32</th>
      <td>14015.0</td>
      <td>홍대입구역(14015.0)</td>
      <td>4397.0</td>
      <td>4993.0</td>
      <td>5121.0</td>
      <td>5097.0</td>
      <td>4810.0</td>
      <td>4287.0</td>
      <td>3884.0</td>
      <td>4224.0</td>
      <td>4397.0</td>
      <td>41210.0</td>
      <td>4578.888889</td>
      <td>126.923302</td>
      <td>37.556398</td>
    </tr>
    <tr>
      <th>33</th>
      <td>24138.0</td>
      <td>잠실역.롯데월드(24138.0)</td>
      <td>4259.0</td>
      <td>4620.0</td>
      <td>4686.0</td>
      <td>4606.0</td>
      <td>4979.0</td>
      <td>4573.0</td>
      <td>4220.0</td>
      <td>4296.0</td>
      <td>4259.0</td>
      <td>40498.0</td>
      <td>4499.777778</td>
      <td>127.097975</td>
      <td>37.512839</td>
    </tr>
    <tr>
      <th>34</th>
      <td>3009.0</td>
      <td>숙대입구역(3009.0)</td>
      <td>4075.0</td>
      <td>4401.0</td>
      <td>4788.0</td>
      <td>4674.0</td>
      <td>5109.0</td>
      <td>4803.0</td>
      <td>4140.0</td>
      <td>4368.0</td>
      <td>4075.0</td>
      <td>40433.0</td>
      <td>4492.555556</td>
      <td>126.972559</td>
      <td>37.543299</td>
    </tr>
    <tr>
      <th>35</th>
      <td>8008.0</td>
      <td>돈암사거리.성신여대입구(8008.0)</td>
      <td>3984.0</td>
      <td>4310.0</td>
      <td>4722.0</td>
      <td>4672.0</td>
      <td>4997.0</td>
      <td>4741.0</td>
      <td>4219.0</td>
      <td>4354.0</td>
      <td>3984.0</td>
      <td>39983.0</td>
      <td>4442.555556</td>
      <td>127.017819</td>
      <td>37.593321</td>
    </tr>
    <tr>
      <th>36</th>
      <td>1037.0</td>
      <td>동대문(흥인지문)(1037.0)</td>
      <td>4067.0</td>
      <td>4145.0</td>
      <td>4719.0</td>
      <td>4648.0</td>
      <td>4737.0</td>
      <td>4344.0</td>
      <td>4248.0</td>
      <td>4217.0</td>
      <td>4067.0</td>
      <td>39192.0</td>
      <td>4354.666667</td>
      <td>127.012493</td>
      <td>37.572167</td>
    </tr>
    <tr>
      <th>37</th>
      <td>19006.0</td>
      <td>영등포역(19006.0)</td>
      <td>3893.0</td>
      <td>4210.0</td>
      <td>4656.0</td>
      <td>4576.0</td>
      <td>5059.0</td>
      <td>4829.0</td>
      <td>3864.0</td>
      <td>4066.0</td>
      <td>3893.0</td>
      <td>39046.0</td>
      <td>4338.444444</td>
      <td>126.907027</td>
      <td>37.516594</td>
    </tr>
    <tr>
      <th>38</th>
      <td>12184.0</td>
      <td>연신내역.로데오거리(12184.0)</td>
      <td>3825.0</td>
      <td>4236.0</td>
      <td>4549.0</td>
      <td>4514.0</td>
      <td>4796.0</td>
      <td>4556.0</td>
      <td>4260.0</td>
      <td>4376.0</td>
      <td>3825.0</td>
      <td>38937.0</td>
      <td>4326.333333</td>
      <td>126.919913</td>
      <td>37.617855</td>
    </tr>
  </tbody>
</table>
</div>

#### Section 4.2 <a class="anchor" id="section_4_2"></a>

##### 하차 Top 39 DataFrame을 Excel에 저장

```python
getoff_weekday.to_excel('Top39평일하차수.xlsx', index=False)
```
