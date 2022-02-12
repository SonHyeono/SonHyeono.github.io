---
title: "Palantir_Foundry-Transport(bus)_seoul"
categories:
  - Intern
feature_text: |
  The History of the 산학 R&D 프로젝트 인턴
---

#### Task

> - 회사에서 [서울시 시민들의 버스 데이터](https://topis.seoul.go.kr/refRoom/openRefRoom_3_4.do)를 처리해서 대중교통의 흐름을 파악하고 어디에 환승센터를 설립하는 것이 좋을지에 대한 판단을 위해 데이터를 다루어 보기로 했습니다.
> - 일단 서울시 버스에 관한 데이터를 간단히 다루어 보았다.

##### 1. jupyter notebook으로 데이터 다루기

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

trading = pd.read_csv('C:\\Users\\ok762\\Documents\\RapidMinerData\\노선별_OD_20210119.csv', encoding='cp949')
```

    C:\Users\ok762\.conda\envs\py38\lib\site-packages\IPython\core\interactiveshell.py:3165: DtypeWarning: Columns (1) have mixed types.Specify dtype option on import or set low_memory=False.
      has_raised = await self.run_ast_nodes(code_ast.body, cell_name,

##### 간단히 1월 평일 버스 데이터를 열어봄.

```python
print(trading)
```

                기준일자   노선명  승차_정류장ARS    승차_정류장명  하차_정류장ARS     하차_정류장명  승차_정류장순번  \
    0       20210119  0017     3689.0    청암자이아파트     3247.0        용문시장       1.0
    1       20210119  0017     3689.0    청암자이아파트     3250.0    용산전자상가입구       1.0
    2       20210119  0017     3689.0    청암자이아파트     3252.0    신용산.지하차도       1.0
    3       20210119  0017     3689.0    청암자이아파트     3255.0         용산역       1.0
    4       20210119  0017     3689.0    청암자이아파트     3298.0  청암동강변삼성아파트       1.0
    ...          ...   ...        ...        ...        ...         ...       ...
    466675  20210119  중랑02     7526.0      새마을금고     7528.0   진주빌라.바다약국      23.0
    466676  20210119  중랑02     7526.0      새마을금고     7529.0   진로아파트앞.종점      23.0
    466677  20210119  중랑02     7527.0        공판장     7500.0   진로아파트앞.종점      24.0
    466678  20210119  중랑02     7528.0  진주빌라.바다약국     7528.0   진주빌라.바다약국      25.0
    466679  20210119  중랑02     7529.0  진로아파트앞.종점     7529.0   진로아파트앞.종점      26.0

            하차_정류장순번  승객수
    0            9.0    1
    1           10.0    1
    2           11.0    1
    3           12.0    6
    4            2.0    1
    ...          ...  ...
    466675      25.0    5
    466676      26.0    5
    466677       1.0    1
    466678      25.0    1
    466679      26.0    1

    [466680 rows x 9 columns]

```python

get_in = trading.groupby(['승차_정류장ARS'])['승객수'].sum()
label = get_in.index
index = np.arange(len(label))
plt.bar(index, get_in)
plt.xlabel('get in busstop')
plt.ylabel('count')
plt.xticks(index,label)
plt.show()
```

![get_in](https://user-images.githubusercontent.com/26592315/139856242-799182ed-e345-4b02-99cc-c3a1f8cc3146.png){:width="100%" height="100%"}{: .center}

##### 간단히 승차정류장별로 승객수를 봄.

```python
get_out = trading.groupby(['하차_정류장ARS'])['승객수'].sum()
label2 = get_out.index
index2 = np.arange(len(label2))
plt.bar(index2, get_out)
plt.xlabel('get out busstop')
plt.ylabel('count')
plt.xticks(index2,label2)
plt.show()
```

![get_out](https://user-images.githubusercontent.com/26592315/139856309-406aa1c8-efaf-4c80-b9b6-e5c384f72f9d.png){:width="100%" height="100%"}{: .center}

##### 똑같이 하차 정류장별로 승객수

##### 다음은 1월 평일 데이터의 노선들 중 종로13을 선택하여

##### 종로13 노선에 대한 승차\_정류장명과 승객수의 관계임.

```python
line = trading.groupby(['노선명','승차_정류장명'])['승객수'].sum()

df_ex1 = line.loc[['종로13']]

label = df_ex1.index
index = np.arange(len(label))
plt.bar(index, df_ex1)
plt.xlabel('jongro13')
plt.ylabel('count')
plt.xticks(index,label,fontsize = 5)
plt.show()

pd.DataFrame(df_ex1)

```

![jongro13](https://user-images.githubusercontent.com/26592315/139856331-8d315bb1-cf02-4467-a315-eb397ab88f47.png){:width="100%" height="100%"}{: .center}

##### 종로13 노선에 대한 정류장 별로 승객수

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
      <th></th>
      <th>승객수</th>
    </tr>
    <tr>
      <th>노선명</th>
      <th>승차_정류장명</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="24" valign="top">종로13</th>
      <th>경진빌라</th>
      <td>10</td>
    </tr>
    <tr>
      <th>구기동</th>
      <td>126</td>
    </tr>
    <tr>
      <th>구기터널입구</th>
      <td>9</td>
    </tr>
    <tr>
      <th>국민은행.세검정지점</th>
      <td>4</td>
    </tr>
    <tr>
      <th>마트앞</th>
      <td>8</td>
    </tr>
    <tr>
      <th>문방구</th>
      <td>3</td>
    </tr>
    <tr>
      <th>부암동주민센터.무계원</th>
      <td>30</td>
    </tr>
    <tr>
      <th>부암슈퍼</th>
      <td>5</td>
    </tr>
    <tr>
      <th>산정빌라</th>
      <td>1</td>
    </tr>
    <tr>
      <th>상명대입구</th>
      <td>48</td>
    </tr>
    <tr>
      <th>상명대입구.석파랑</th>
      <td>1</td>
    </tr>
    <tr>
      <th>상명대정문</th>
      <td>46</td>
    </tr>
    <tr>
      <th>상명대후문</th>
      <td>43</td>
    </tr>
    <tr>
      <th>상명초등학교</th>
      <td>7</td>
    </tr>
    <tr>
      <th>서교빌라</th>
      <td>2</td>
    </tr>
    <tr>
      <th>세검정교회</th>
      <td>7</td>
    </tr>
    <tr>
      <th>세검초등학교</th>
      <td>4</td>
    </tr>
    <tr>
      <th>엄마분식</th>
      <td>4</td>
    </tr>
    <tr>
      <th>완성빌라</th>
      <td>19</td>
    </tr>
    <tr>
      <th>인왕빌딩</th>
      <td>2</td>
    </tr>
    <tr>
      <th>청구빌라</th>
      <td>14</td>
    </tr>
    <tr>
      <th>평창파출소</th>
      <td>78</td>
    </tr>
    <tr>
      <th>하림각</th>
      <td>37</td>
    </tr>
    <tr>
      <th>화정박물관</th>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>

##### 노선별 승객수가 가장 많은 정류장

```python
line = trading.groupby(['노선명','승차_정류장명'])
line_top = pd.DataFrame(line.sum()['승객수'])
pd.set_option('display.max.colwidth',50)
df = line_top.sort_values(by='승객수', ascending=False).groupby('노선명').head(1)
df
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
      <th></th>
      <th>승객수</th>
    </tr>
    <tr>
      <th>노선명</th>
      <th>승차_정류장명</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>금천03</th>
      <th>가산디지털단지역</th>
      <td>3764</td>
    </tr>
    <tr>
      <th>동대문01</th>
      <th>회기역</th>
      <td>3336</td>
    </tr>
    <tr>
      <th>노원14</th>
      <th>창동역서측</th>
      <td>3086</td>
    </tr>
    <tr>
      <th>서초18</th>
      <th>양재역</th>
      <td>3084</td>
    </tr>
    <tr>
      <th>5515</th>
      <th>서울대입구역</th>
      <td>2937</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>N26</th>
      <th>동대문역.흥인지문</th>
      <td>41</td>
    </tr>
    <tr>
      <th>N65</th>
      <th>경방타임스퀘어.신세계백화점</th>
      <td>37</td>
    </tr>
    <tr>
      <th>8541</th>
      <th>미림여고.미림여자정보과학고</th>
      <td>31</td>
    </tr>
    <tr>
      <th>8112</th>
      <th>북서울꿈의숲</th>
      <td>28</td>
    </tr>
    <tr>
      <th>03</th>
      <th>안국역.종로경찰서.인사동</th>
      <td>7</td>
    </tr>
  </tbody>
</table>
<p>624 rows × 1 columns</p>
</div>

---

#### 2. RapidMiner로 데이터 돌려보기.

![get_in_rapidminer](https://user-images.githubusercontent.com/26592315/139856878-c62e3abd-2fee-4829-8804-627945050adf.png){:width="100%" height="100%"}{: .center}

> - 승차정류장과 승객수의 그래프를 rapidminer results에 visualization으로 확인

![get_out_rapidminer](https://user-images.githubusercontent.com/26592315/139856888-050f6ba2-21ef-4951-b352-ea6c33ea9e3c.png){:width="100%" height="100%"}{: .center}

> - 하차정류장과 승객수의 그래프를 rapidminer results에 visualizations으로 확인

---

#### 3. 상용 version과 open version의 차이점

- ##### 상용 version

  ![rapidminer](https://user-images.githubusercontent.com/26592315/139856902-7cefb598-3cae-43e1-a6e8-3b9b6fd3fe2d.png){:width="100%" height="100%"}{: .center}

- ##### open version
  ![openrapidminer](https://user-images.githubusercontent.com/26592315/139856898-850c136f-2269-4502-aec9-6675c273b79f.png){:width="100%" height="100%"}{: .center}

#### 4. 시각화

- 데이터에 대한 시각화를 Folium 패키지를 이용해서 지도 위에서 띄우기로 함.

##### Folium

> - 시각화 패키지중 하나이며 leaflet.js 기반으로 지도를 그려주고 나온지가 오래되어서 안정적이며 pandas와 쉽게 연동이 가능함.

---

#### 5. 결론

> - Foundry 답게 데이터가 들어왔을 때 시각화를 더 완벽하게 하기위해 Folium을 사용하기로 했고 이를 위해 정류장명으로 된 데이터에서 위도와 경도를 추출해야한다.

> - rapidminer를 이용하기 위해서 open version에는 visualizations이 없어서 엔진팀에 문의 해보기로 했음.

> - 오세훈 서울시장님이 서울시에 서울역 같은 환승센터를 더 지어서 교통을 편리하게 하려고 하는데 그에 대해 데이터를 다루어보고 최적의 환승센터의 위치를 찾는 것이 목표이다.
