---
title: "국민건강보험공단_건강검진정보 데이터 분석"
categories:
  - KB 국민은행 IT 아카데미
feature_text: |
  The History of the KB 국민은행 IT 아카데미 IT's Your Life
---

# 국민건강보험공단_건강검진정보_2021_12 분석

[건강검진 결과지 읽는 법](https://health.chosun.com/site/data/html_dir/2016/11/30/2016113001291.html)

## 국민건강보험공단_건강검진정보 다운로드하는 방법

1. http://data.go.kr 접속
2. 검색어 "국민건강보험공단" 검색
3. 검색결과 3번째쯤 제목이 "국민건강보험공단_건강검진정보" 클릭
4. 우측 "다운로드" 클릭 하여 데이터파일 다운로드한다
5. 하단 "주기성과거데이터" 우측 "더보기" 클릭
6. 3번째 "...사용자매뉴얼" 클릭
7. "다운로드" 클릭. 사용자메뉴얼은 한글파일이라서 한글뷰어 설치가 필요하다. 
8. 데이터파일내 코드들은 사용자매뉴얼내 설명을 참고하여 이용한다.

## 프로젝트 목표
1. 건강검진정보를 보고 최대한 다양한 방법으로 통계를 내어 시각화를 한다. 즉 EDA를 하시오.
2. 검진정보와 검진결과지를 제대로 읽는법을 참고하여 개인별 건강상태정보를 요약하시오. 특히 BMI수치에 대한 해석은 성별, 연령별로 다르게 적용해야한다는 주장과 자료가 있으니 확인바랍니다. 
3. 예를 들어 비만도 칼럼을 만들어 비만정도를 기록, 혈압칼럼만들어 저혈압,.. 을 기록한다. 건강상태별로 통계내고 시각화하고 건강상태를 요양한 칼럼을 작성한다. 그외 미디어를 통해 건강관련 통계와 직접 계산한 통계를 비교한 내용을 작성할 수 있다.
3. 작성된 개인별 요약상태를 이용한 통계를 시각화할 수 있다.( 예를들어 비만도가 중증인 사람들중 xx%는 흡연중이다. 등등 )
4. 팀별로 모여 목표와 해야하는 내용에 대해 의견을 나눈다.
5. 프로젝트는 개인별로 작성하여 매너모스트에서 DM으로 제출하세요
6. 제출기한은 내일(4월 8일 13시)
7. 제출자중 팀별로 1명씩 제출한 내용에 대해 발표한다.

### 아래는 건강검진정보를 분리,저장한 경우를 예로 들었다. 각자 다운로드 받아 사용하세요.

```python
# https://www.data.go.kr/data/15007122/fileData.do#layer_data_infomation
import pandas as pd
df = pd.read_csv("./국민건강보험공단_건강검진정보_20211229.CSV", encoding="euc-kr")
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
      <th>기준년도</th>
      <th>가입자 일련번호</th>
      <th>시도코드</th>
      <th>성별코드</th>
      <th>연령대 코드(5세단위)</th>
      <th>신장(5Cm단위)</th>
      <th>체중(5Kg 단위)</th>
      <th>허리둘레</th>
      <th>시력(좌)</th>
      <th>시력(우)</th>
      <th>...</th>
      <th>혈청크레아티닌</th>
      <th>(혈청지오티)AST</th>
      <th>(혈청지오티)ALT</th>
      <th>감마 지티피</th>
      <th>흡연상태</th>
      <th>음주여부</th>
      <th>구강검진 수검여부</th>
      <th>치아우식증유무</th>
      <th>치석</th>
      <th>데이터 공개일자</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020</td>
      <td>1</td>
      <td>36</td>
      <td>1</td>
      <td>9</td>
      <td>165</td>
      <td>60</td>
      <td>72.1</td>
      <td>1.2</td>
      <td>1.5</td>
      <td>...</td>
      <td>1.1</td>
      <td>21.0</td>
      <td>27.0</td>
      <td>21.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020</td>
      <td>2</td>
      <td>27</td>
      <td>2</td>
      <td>13</td>
      <td>150</td>
      <td>65</td>
      <td>81.0</td>
      <td>0.8</td>
      <td>0.8</td>
      <td>...</td>
      <td>0.5</td>
      <td>18.0</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020</td>
      <td>3</td>
      <td>11</td>
      <td>2</td>
      <td>12</td>
      <td>155</td>
      <td>55</td>
      <td>70.0</td>
      <td>0.6</td>
      <td>0.7</td>
      <td>...</td>
      <td>0.7</td>
      <td>27.0</td>
      <td>25.0</td>
      <td>7.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020</td>
      <td>4</td>
      <td>31</td>
      <td>1</td>
      <td>13</td>
      <td>160</td>
      <td>70</td>
      <td>90.8</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>1.2</td>
      <td>65.0</td>
      <td>97.0</td>
      <td>72.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2021-12-29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020</td>
      <td>5</td>
      <td>41</td>
      <td>2</td>
      <td>12</td>
      <td>155</td>
      <td>50</td>
      <td>75.2</td>
      <td>1.5</td>
      <td>1.2</td>
      <td>...</td>
      <td>0.7</td>
      <td>18.0</td>
      <td>17.0</td>
      <td>14.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
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
      <td>...</td>
    </tr>
    <tr>
      <th>999995</th>
      <td>2020</td>
      <td>999996</td>
      <td>41</td>
      <td>2</td>
      <td>13</td>
      <td>145</td>
      <td>55</td>
      <td>81.0</td>
      <td>0.9</td>
      <td>1.0</td>
      <td>...</td>
      <td>0.6</td>
      <td>21.0</td>
      <td>25.0</td>
      <td>18.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
    </tr>
    <tr>
      <th>999996</th>
      <td>2020</td>
      <td>999997</td>
      <td>26</td>
      <td>2</td>
      <td>12</td>
      <td>160</td>
      <td>55</td>
      <td>76.5</td>
      <td>1.5</td>
      <td>1.5</td>
      <td>...</td>
      <td>0.8</td>
      <td>21.0</td>
      <td>14.0</td>
      <td>19.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
    </tr>
    <tr>
      <th>999997</th>
      <td>2020</td>
      <td>999998</td>
      <td>48</td>
      <td>1</td>
      <td>9</td>
      <td>175</td>
      <td>70</td>
      <td>85.0</td>
      <td>1.2</td>
      <td>1.2</td>
      <td>...</td>
      <td>0.9</td>
      <td>26.0</td>
      <td>20.0</td>
      <td>17.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
    </tr>
    <tr>
      <th>999998</th>
      <td>2020</td>
      <td>999999</td>
      <td>48</td>
      <td>2</td>
      <td>9</td>
      <td>160</td>
      <td>70</td>
      <td>91.0</td>
      <td>0.6</td>
      <td>0.5</td>
      <td>...</td>
      <td>1.0</td>
      <td>25.0</td>
      <td>29.0</td>
      <td>13.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
    </tr>
    <tr>
      <th>999999</th>
      <td>2020</td>
      <td>1000000</td>
      <td>28</td>
      <td>1</td>
      <td>11</td>
      <td>160</td>
      <td>55</td>
      <td>76.1</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>...</td>
      <td>0.9</td>
      <td>17.0</td>
      <td>13.0</td>
      <td>24.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-12-29</td>
    </tr>
  </tbody>
</table>
<p>1000000 rows × 31 columns</p>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1000000 entries, 0 to 999999
    Data columns (total 31 columns):
     #   Column        Non-Null Count    Dtype  
    ---  ------        --------------    -----  
     0   기준년도          1000000 non-null  int64  
     1   가입자 일련번호      1000000 non-null  int64  
     2   시도코드          1000000 non-null  int64  
     3   성별코드          1000000 non-null  int64  
     4   연령대 코드(5세단위)  1000000 non-null  int64  
     5   신장(5Cm단위)     1000000 non-null  int64  
     6   체중(5Kg 단위)    1000000 non-null  int64  
     7   허리둘레          999892 non-null   float64
     8   시력(좌)         999743 non-null   float64
     9   시력(우)         999748 non-null   float64
     10  청력(좌)         999778 non-null   float64
     11  청력(우)         999770 non-null   float64
     12  수축기 혈압        992468 non-null   float64
     13  이완기 혈압        992466 non-null   float64
     14  식전혈당(공복혈당)    992398 non-null   float64
     15  총 콜레스테롤       402306 non-null   float64
     16  트리글리세라이드      402322 non-null   float64
     17  HDL 콜레스테롤     402315 non-null   float64
     18  LDL 콜레스테롤     394471 non-null   float64
     19  혈색소           992389 non-null   float64
     20  요단백           987859 non-null   float64
     21  혈청크레아티닌       992398 non-null   float64
     22  (혈청지오티)AST    992399 non-null   float64
     23  (혈청지오티)ALT    992398 non-null   float64
     24  감마 지티피        992397 non-null   float64
     25  흡연상태          999657 non-null   float64
     26  음주여부          999804 non-null   float64
     27  구강검진 수검여부     1000000 non-null  int64  
     28  치아우식증유무       331383 non-null   float64
     29  치석            331382 non-null   float64
     30  데이터 공개일자      1000000 non-null  object 
    dtypes: float64(22), int64(8), object(1)
    memory usage: 236.5+ MB
    

## 결측치 처리


![image](https://user-images.githubusercontent.com/26592315/163108483-5b419dc3-4e15-4e45-a5b2-6d5d9627e4dd.png)
![image](https://user-images.githubusercontent.com/26592315/163108549-4aadae0d-ff06-4a7b-a63d-14a3f8781784.png)

- 코드 

```python

df.fillna({
            '식전혈당(공복혈당)' : round(df['식전혈당(공복혈당)'].mean(), 1),
            '이완기 혈압' : round(df['이완기 혈압'].mean(), 1),
            '수축기 혈압' : round(df['수축기 혈압'].mean(), 1),
            '허리둘레': round(df['허리둘레'].mean(),1),
            '시력(좌)' : round(df['시력(좌)'].mean(),1),
            '시력(우)' : round(df['시력(우)'].mean(),1),
            '청력(좌)' : df['청력(좌)'].mode()[0],
            '청력(우)' : df['청력(우)'].mode()[0],
            '혈색소': round(df['혈색소'].mean(), 3),
            '요단백': df['요단백'].mode()[0],
            '혈청크레아티닌' : round(df['혈청크레아티닌'].mean(), 5),
            '(혈청지오티)AST': round(df['(혈청지오티)AST'].mean(),2),
            '(혈청지오티)ALT': round(df['(혈청지오티)ALT'].mean(),2),
            '감마 지티피': round(df['감마 지티피'].mean(), 1),
           '흡연상태':df['흡연상태'].mode()[0],
           '음주여부':df['음주여부'].mode()[0]}, inplace=True)

df[df["청력(우)"] == 3]["청력(우)"] = 2.0
df[df["청력(좌)"] == 3]["청력(좌)"] = 2.0

df = df.drop(['총 콜레스테롤','트리글리세라이드','HDL 콜레스테롤','LDL 콜레스테롤',
              '치아우식증유무', '치석', '데이터 공개일자'], axis=1) 


```

    C:\Users\user\AppData\Local\Temp/ipykernel_6680/1967347842.py:19: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      df[df["청력(우)"] == 3]["청력(우)"] = 2.0
    C:\Users\user\AppData\Local\Temp/ipykernel_6680/1967347842.py:20: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      df[df["청력(좌)"] == 3]["청력(좌)"] = 2.0
    


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1000000 entries, 0 to 999999
    Data columns (total 24 columns):
     #   Column        Non-Null Count    Dtype  
    ---  ------        --------------    -----  
     0   기준년도          1000000 non-null  int64  
     1   가입자 일련번호      1000000 non-null  int64  
     2   시도코드          1000000 non-null  int64  
     3   성별코드          1000000 non-null  int64  
     4   연령대 코드(5세단위)  1000000 non-null  int64  
     5   신장(5Cm단위)     1000000 non-null  int64  
     6   체중(5Kg 단위)    1000000 non-null  int64  
     7   허리둘레          1000000 non-null  float64
     8   시력(좌)         1000000 non-null  float64
     9   시력(우)         1000000 non-null  float64
     10  청력(좌)         1000000 non-null  float64
     11  청력(우)         1000000 non-null  float64
     12  수축기 혈압        1000000 non-null  float64
     13  이완기 혈압        1000000 non-null  float64
     14  식전혈당(공복혈당)    1000000 non-null  float64
     15  혈색소           1000000 non-null  float64
     16  요단백           1000000 non-null  float64
     17  혈청크레아티닌       1000000 non-null  float64
     18  (혈청지오티)AST    1000000 non-null  float64
     19  (혈청지오티)ALT    1000000 non-null  float64
     20  감마 지티피        1000000 non-null  float64
     21  흡연상태          1000000 non-null  float64
     22  음주여부          1000000 non-null  float64
     23  구강검진 수검여부     1000000 non-null  int64  
    dtypes: float64(16), int64(8)
    memory usage: 183.1 MB
    


```python
df.columns
```




    Index(['기준년도', '가입자 일련번호', '시도코드', '성별코드', '연령대 코드(5세단위)', '신장(5Cm단위)',
           '체중(5Kg 단위)', '허리둘레', '시력(좌)', '시력(우)', '청력(좌)', '청력(우)', '수축기 혈압',
           '이완기 혈압', '식전혈당(공복혈당)', '혈색소', '요단백', '혈청크레아티닌', '(혈청지오티)AST',
           '(혈청지오티)ALT', '감마 지티피', '흡연상태', '음주여부', '구강검진 수검여부'],
          dtype='object')




```python
import requests
import json

# 대한민국 행정구역 json raw파일(githubcontent)
# https://neurowhai.tistory.com/350
r = requests.get('https://raw.githubusercontent.com/kbAcademyBclassSuperTeam/draft/main/TL_SCCO_CTPRVN.json')
c = r.content
seoul_geo = json.loads(c)
```


```python
city = {11: "서울특별시", 42: "강원도", 26 : "부산광역시", 43 : "충청북도", 27 : "대구광역시" , 44: "충청남도", 28: "인천광역시", 
        45: "전라북도", 29 : "광주광역시", 46: "전라남도", 30: "대전광역시", 47: "경상북도", 31: "울산광역시", 48: "경상남도", 
        36: "세종특별자치시", 49: "제주특별자치도", 41: "경기도"}

city = pd.DataFrame(list(city.items()),
                   columns=['시도코드', '시도명'])

```


```python
# https://address.dawul.co.kr/
from pandas import Series, DataFrame
korea = {
    '시도코드':[11, 26, 28, 27, 30, 29, 
          31,41, 42,
          43, 44, 45, 46, 47, 48,49, 36],
    '위도':[37.5230201, 35.1851772, 37.4586682, 35.8495971, 36.3437035, 35.1493858, 35.5373683, 37.3990400, 37.8796466, 36.8545487,
         36.5968017, 35.7901670, 34.8288912, 36.3702891, 35.4070497, 33.3926885, 36.5256400],
    '경도':[126.982219, 129.112042, 126.633866, 128.539950, 127.390448, 126.821757, 129.323877, 127.301738, 128.514632, 127.774990,
         126.662838, 127.117254, 126.910324, 128.838189, 128.293600, 126.494894, 127.268516]
        }

korea = DataFrame(korea)
```

##  위도, 경도, BMI 열 추가


```python
df = pd.merge(df, korea, left_on='시도코드', right_on='시도코드', how='outer')
```


```python
df["BMI"] = round(df["체중(5Kg 단위)"] / ((df["신장(5Cm단위)"] / 100) ** 2), 2) # BMI 추가
```

[40세 이상 인구 데이터](https://jumin.mois.go.kr/ageStatMonth.do#none)


```python
population = pd.read_csv('./40세이상인구데이터.csv', encoding='euc-kr')
# population
```


```python
import re
total_pop = population[['행정구역', '2021년12월_계_연령구간인구수']]
# total_pop
regex = "\(.*\)|\s-\s.*"

for i in range(len(total_pop)):
    total_pop['행정구역'][i] =  re.sub(regex, '', total_pop['행정구역'][i])
total_pop = total_pop.drop(0)
# total_pop
```

    C:\Users\user\AppData\Local\Temp/ipykernel_6680/3436244759.py:7: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      total_pop['행정구역'][i] =  re.sub(regex, '', total_pop['행정구역'][i])
    

## 시도별 비만율


```python
bmi_count = df[df["BMI"] > 30]['시도코드'].value_counts().to_frame()
bmi_count.rename(columns = {"시도코드" :"고도비만 수"}, inplace =True)
bmi_count['시도코드'] = bmi_count.index
# bmi_count
```


```python
pop_count = df['시도코드'].value_counts().to_frame()
pop_count.rename(columns = {"시도코드" :"총인원 수"}, inplace =True)
pop_count['시도코드'] = pop_count.index
pop_count
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
      <th>총인원 수</th>
      <th>시도코드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>41</th>
      <td>247369</td>
      <td>41</td>
    </tr>
    <tr>
      <th>11</th>
      <td>166231</td>
      <td>11</td>
    </tr>
    <tr>
      <th>26</th>
      <td>69025</td>
      <td>26</td>
    </tr>
    <tr>
      <th>48</th>
      <td>68530</td>
      <td>48</td>
    </tr>
    <tr>
      <th>28</th>
      <td>58345</td>
      <td>28</td>
    </tr>
    <tr>
      <th>47</th>
      <td>54438</td>
      <td>47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>48413</td>
      <td>27</td>
    </tr>
    <tr>
      <th>44</th>
      <td>42582</td>
      <td>44</td>
    </tr>
    <tr>
      <th>45</th>
      <td>38066</td>
      <td>45</td>
    </tr>
    <tr>
      <th>46</th>
      <td>38041</td>
      <td>46</td>
    </tr>
    <tr>
      <th>43</th>
      <td>34009</td>
      <td>43</td>
    </tr>
    <tr>
      <th>42</th>
      <td>32023</td>
      <td>42</td>
    </tr>
    <tr>
      <th>30</th>
      <td>30057</td>
      <td>30</td>
    </tr>
    <tr>
      <th>29</th>
      <td>28532</td>
      <td>29</td>
    </tr>
    <tr>
      <th>31</th>
      <td>26001</td>
      <td>31</td>
    </tr>
    <tr>
      <th>49</th>
      <td>11878</td>
      <td>49</td>
    </tr>
    <tr>
      <th>36</th>
      <td>6460</td>
      <td>36</td>
    </tr>
  </tbody>
</table>
</div>




```python
pro_bmi = pd.merge(bmi_count, pop_count, left_on='시도코드', right_on='시도코드', how='outer')
pro_bmi = pd.merge(pro_bmi, city, left_on='시도코드', right_on='시도코드', how='outer')
pro_bmi['비만율'] = pro_bmi["고도비만 수"]/pro_bmi["총인원 수"]*100
# pro_bmi
```


```python
import matplotlib.pyplot as plt
import seaborn as sns
plt.figure(figsize=(15,8))

plt.rcParams['font.family'] = 'Malgun Gothic'

sns.barplot(y="시도명",x="비만율",data = pro_bmi.sort_values(by="비만율"))

```




    <AxesSubplot:xlabel='비만율', ylabel='시도명'>




    
![output_22_1](https://user-images.githubusercontent.com/26592315/163104275-54e6974f-5cdf-4bd5-8025-15c4e58c5b3c.png)

    


### 고도비만을 지도로 나타내기


```python
# !pip install folium
```


```python
import folium
from folium.plugins import MarkerCluster
m = folium.Map(
    location=[37.559819, 126.963895],
    zoom_start=12, 
    tiles='cartodbpositron'
)

folium.GeoJson(
    seoul_geo,
    name='지역구'
).add_to(m)

marker_cluster = MarkerCluster().add_to(m)

for lat, long in zip(df[df["BMI"] > 30]['위도'], df[df["BMI"] > 30]['경도']):
    folium.Marker([lat, long], icon = folium.Icon(color="green")).add_to(marker_cluster)

m
```

![image](https://user-images.githubusercontent.com/26592315/163105456-4ea9f7e2-5ba9-4929-a8ee-10097c947848.png)

- md파일이여서 folium을 png로 나타냄.

---


# 시도별 흡연율


```python
smoke = df[df["흡연상태"]==3].groupby("시도코드")[["흡연상태"]].count()
smoke['시도코드'] = smoke.index
smoke = smoke.reset_index(drop=True)
# smoke
```


```python
pro_smoke = pd.merge(city, smoke, left_on='시도코드', right_on='시도코드', how='outer')
pro_smoke = pd.merge(pro_smoke, pop_count, left_on='시도코드', right_on='시도코드', how='outer')
pro_smoke['흡연율'] = pro_smoke["흡연상태"]/pro_smoke["총인원 수"]*100
pro_smoke
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
      <th>시도코드</th>
      <th>시도명</th>
      <th>흡연상태</th>
      <th>총인원 수</th>
      <th>흡연율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11</td>
      <td>서울특별시</td>
      <td>27091</td>
      <td>166231</td>
      <td>16.297201</td>
    </tr>
    <tr>
      <th>1</th>
      <td>42</td>
      <td>강원도</td>
      <td>5794</td>
      <td>32023</td>
      <td>18.093245</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26</td>
      <td>부산광역시</td>
      <td>12450</td>
      <td>69025</td>
      <td>18.036943</td>
    </tr>
    <tr>
      <th>3</th>
      <td>43</td>
      <td>충청북도</td>
      <td>6573</td>
      <td>34009</td>
      <td>19.327237</td>
    </tr>
    <tr>
      <th>4</th>
      <td>27</td>
      <td>대구광역시</td>
      <td>8874</td>
      <td>48413</td>
      <td>18.329787</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44</td>
      <td>충청남도</td>
      <td>8634</td>
      <td>42582</td>
      <td>20.276173</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28</td>
      <td>인천광역시</td>
      <td>12012</td>
      <td>58345</td>
      <td>20.587882</td>
    </tr>
    <tr>
      <th>7</th>
      <td>45</td>
      <td>전라북도</td>
      <td>6359</td>
      <td>38066</td>
      <td>16.705196</td>
    </tr>
    <tr>
      <th>8</th>
      <td>29</td>
      <td>광주광역시</td>
      <td>4736</td>
      <td>28532</td>
      <td>16.598906</td>
    </tr>
    <tr>
      <th>9</th>
      <td>46</td>
      <td>전라남도</td>
      <td>6016</td>
      <td>38041</td>
      <td>15.814516</td>
    </tr>
    <tr>
      <th>10</th>
      <td>30</td>
      <td>대전광역시</td>
      <td>5197</td>
      <td>30057</td>
      <td>17.290481</td>
    </tr>
    <tr>
      <th>11</th>
      <td>47</td>
      <td>경상북도</td>
      <td>9965</td>
      <td>54438</td>
      <td>18.305228</td>
    </tr>
    <tr>
      <th>12</th>
      <td>31</td>
      <td>울산광역시</td>
      <td>5701</td>
      <td>26001</td>
      <td>21.926080</td>
    </tr>
    <tr>
      <th>13</th>
      <td>48</td>
      <td>경상남도</td>
      <td>12971</td>
      <td>68530</td>
      <td>18.927477</td>
    </tr>
    <tr>
      <th>14</th>
      <td>36</td>
      <td>세종특별자치시</td>
      <td>1070</td>
      <td>6460</td>
      <td>16.563467</td>
    </tr>
    <tr>
      <th>15</th>
      <td>49</td>
      <td>제주특별자치도</td>
      <td>2339</td>
      <td>11878</td>
      <td>19.691867</td>
    </tr>
    <tr>
      <th>16</th>
      <td>41</td>
      <td>경기도</td>
      <td>47929</td>
      <td>247369</td>
      <td>19.375508</td>
    </tr>
  </tbody>
</table>
</div>




```python
pro_smoke = pd.merge(pro_smoke, korea, left_on='시도코드', right_on='시도코드', how='outer')
```


```python
import matplotlib.pyplot as plt
import seaborn as sns
plt.figure(figsize=(15,8))
plt.rcParams['font.family'] = 'Malgun Gothic'

sns.barplot(y="시도명",x="흡연율",data = pro_smoke.sort_values(by="흡연율"))

```




    <AxesSubplot:xlabel='흡연율', ylabel='시도명'>




    
![output_30_1](https://user-images.githubusercontent.com/26592315/163104278-c7eb2ea1-279b-451f-a91c-bade90c9ea9b.png)
    


## 흡연자 지도로 나타내기


```python

import folium
from folium.plugins import MarkerCluster
m = folium.Map(
    location=[37.559819, 126.963895],
    zoom_start=12, 
    tiles='cartodbpositron'
)

folium.GeoJson(
    seoul_geo,
    name='지역구'
).add_to(m)

marker_cluster = MarkerCluster().add_to(m)

for lat, long in zip(df[df["흡연상태"] == 3]['위도'], df[df["흡연상태"] == 3]['경도']):
    folium.Marker([lat, long], icon = folium.Icon(color="green")).add_to(marker_cluster)

m
```

![image](https://user-images.githubusercontent.com/26592315/163105508-5038baf7-2cbc-4d0b-803f-22bf9f134b1b.png)

- md파일이여서 folium을 png로 나타냄.

```python
df["BMI_결과"] = df["BMI"]
df.loc[df[df["BMI"] >= 30].index, "BMI_결과"] = "고도비만"
df.loc[df[((df["BMI"] >= 25) & (df["BMI"] < 30))].index, "BMI_결과"] = "과체중"
df.loc[df[((df["BMI"] >= 18.5) & (df["BMI"] < 25))].index, "BMI_결과"] = "정상체중"
df.loc[df[df["BMI"] < 18.5].index, "BMI_결과"] = "저체중"

# 혈압 결과 범주화
df["혈압_결과"] = df["수축기 혈압"]
df.loc[df[(df["수축기 혈압"] < 100)].index, "혈압_결과"] = "저혈압"
df.loc[df[(df["수축기 혈압"] >= 100) & (df["수축기 혈압"] < 120)].index, "혈압_결과"] = "정상"
df.loc[df[(df["수축기 혈압"] >= 120) & (df["수축기 혈압"] < 145)].index, "혈압_결과"] = "주의"
df.loc[df[(df["수축기 혈압"] >= 145)].index, "혈압_결과"] = "고혈압"


# 간기능 결과 범주화
df["간기능_결과"] = df["(혈청지오티)ALT"]
df.loc[df[((df["(혈청지오티)AST"] < 32))].index, "간기능_결과"] = "정상"
df.loc[df[((df["(혈청지오티)AST"] >= 32))].index, "간기능_결과"] = "주의"
df.loc[df[((df["(혈청지오티)AST"] >= 51))].index, "간기능_결과"] = "검사 필요"

df["당뇨병_결과"] = df["식전혈당(공복혈당)"] #  당뇨병
df.loc[df[((df["식전혈당(공복혈당)"] <= 120) & (df["식전혈당(공복혈당)"] >= 70))].index, "당뇨병_결과"] = "정상"
df.loc[df[((df["식전혈당(공복혈당)"] > 120) & (df["식전혈당(공복혈당)"] < 126))].index, "당뇨병_결과"] = "주의"
df.loc[df[((df["식전혈당(공복혈당)"] >= 126) | (df["식전혈당(공복혈당)"] < 70))].index, "당뇨병_결과"] = "검사 필요"

df["연령대"] = df["연령대 코드(5세단위)"]
df.loc[df[(df["연령대 코드(5세단위)"] == 9) | (df["연령대 코드(5세단위)"] == 10)].index, "연령대"] = "40대"
df.loc[df[(df["연령대 코드(5세단위)"] == 11) | (df["연령대 코드(5세단위)"] == 12)].index, "연령대"] = "50대"
df.loc[df[(df["연령대 코드(5세단위)"] == 13) | (df["연령대 코드(5세단위)"] == 14)].index, "연령대"] = "60대"
df.loc[df[(df["연령대 코드(5세단위)"] == 15) | (df["연령대 코드(5세단위)"] == 16)].index, "연령대"] = "70대"
df.loc[df[(df["연령대 코드(5세단위)"] == 17) | (df["연령대 코드(5세단위)"] == 18)].index, "연령대"] = "80대"
```

## 당뇨병 환자율


```python
당뇨환자 = df[df["당뇨병_결과"]=="주의"].groupby("시도코드")[["당뇨병_결과"]].count()
당뇨환자['시도코드'] = 당뇨환자.index
당뇨환자 = 당뇨환자.reset_index(drop=True)
당뇨환자
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
      <th>당뇨병_결과</th>
      <th>시도코드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4472</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2036</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1241</td>
      <td>27</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1678</td>
      <td>28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>907</td>
      <td>29</td>
    </tr>
    <tr>
      <th>5</th>
      <td>750</td>
      <td>30</td>
    </tr>
    <tr>
      <th>6</th>
      <td>706</td>
      <td>31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>148</td>
      <td>36</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6747</td>
      <td>41</td>
    </tr>
    <tr>
      <th>9</th>
      <td>907</td>
      <td>42</td>
    </tr>
    <tr>
      <th>10</th>
      <td>874</td>
      <td>43</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1249</td>
      <td>44</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1109</td>
      <td>45</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1259</td>
      <td>46</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1551</td>
      <td>47</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1849</td>
      <td>48</td>
    </tr>
    <tr>
      <th>16</th>
      <td>304</td>
      <td>49</td>
    </tr>
  </tbody>
</table>
</div>




```python
당뇨환자 = pd.merge(city, 당뇨환자, left_on='시도코드', right_on='시도코드', how='outer')
당뇨환자 = pd.merge(당뇨환자, pop_count, left_on='시도코드', right_on='시도코드', how='outer')
당뇨환자['당뇨환자율'] = 당뇨환자["당뇨병_결과"] / 당뇨환자["총인원 수"] * 100
당뇨환자
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
      <th>시도코드</th>
      <th>시도명</th>
      <th>당뇨병_결과</th>
      <th>총인원 수</th>
      <th>당뇨환자율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11</td>
      <td>서울특별시</td>
      <td>4472</td>
      <td>166231</td>
      <td>2.690232</td>
    </tr>
    <tr>
      <th>1</th>
      <td>42</td>
      <td>강원도</td>
      <td>907</td>
      <td>32023</td>
      <td>2.832339</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26</td>
      <td>부산광역시</td>
      <td>2036</td>
      <td>69025</td>
      <td>2.949656</td>
    </tr>
    <tr>
      <th>3</th>
      <td>43</td>
      <td>충청북도</td>
      <td>874</td>
      <td>34009</td>
      <td>2.569908</td>
    </tr>
    <tr>
      <th>4</th>
      <td>27</td>
      <td>대구광역시</td>
      <td>1241</td>
      <td>48413</td>
      <td>2.563361</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44</td>
      <td>충청남도</td>
      <td>1249</td>
      <td>42582</td>
      <td>2.933164</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28</td>
      <td>인천광역시</td>
      <td>1678</td>
      <td>58345</td>
      <td>2.875996</td>
    </tr>
    <tr>
      <th>7</th>
      <td>45</td>
      <td>전라북도</td>
      <td>1109</td>
      <td>38066</td>
      <td>2.913361</td>
    </tr>
    <tr>
      <th>8</th>
      <td>29</td>
      <td>광주광역시</td>
      <td>907</td>
      <td>28532</td>
      <td>3.178887</td>
    </tr>
    <tr>
      <th>9</th>
      <td>46</td>
      <td>전라남도</td>
      <td>1259</td>
      <td>38041</td>
      <td>3.309587</td>
    </tr>
    <tr>
      <th>10</th>
      <td>30</td>
      <td>대전광역시</td>
      <td>750</td>
      <td>30057</td>
      <td>2.495259</td>
    </tr>
    <tr>
      <th>11</th>
      <td>47</td>
      <td>경상북도</td>
      <td>1551</td>
      <td>54438</td>
      <td>2.849113</td>
    </tr>
    <tr>
      <th>12</th>
      <td>31</td>
      <td>울산광역시</td>
      <td>706</td>
      <td>26001</td>
      <td>2.715280</td>
    </tr>
    <tr>
      <th>13</th>
      <td>48</td>
      <td>경상남도</td>
      <td>1849</td>
      <td>68530</td>
      <td>2.698088</td>
    </tr>
    <tr>
      <th>14</th>
      <td>36</td>
      <td>세종특별자치시</td>
      <td>148</td>
      <td>6460</td>
      <td>2.291022</td>
    </tr>
    <tr>
      <th>15</th>
      <td>49</td>
      <td>제주특별자치도</td>
      <td>304</td>
      <td>11878</td>
      <td>2.559353</td>
    </tr>
    <tr>
      <th>16</th>
      <td>41</td>
      <td>경기도</td>
      <td>6747</td>
      <td>247369</td>
      <td>2.727504</td>
    </tr>
  </tbody>
</table>
</div>




```python
import matplotlib.pyplot as plt
import seaborn as sns
plt.figure(figsize=(15,8))
plt.rcParams['font.family'] = 'Malgun Gothic'

sns.barplot(y="시도명",x="당뇨환자율",data = 당뇨환자.sort_values(by="당뇨환자율"))
```




    <AxesSubplot:xlabel='당뇨환자율', ylabel='시도명'>




    
![output_37_1](https://user-images.githubusercontent.com/26592315/163104280-6898268f-7e8e-4c99-97bb-fca23f22fca4.png)

    



```python
import seaborn as sns

re_df = df.groupby(['연령대','간기능_결과'])[['시도코드']].count()
plt.figure(figsize=(20,10))

sns.lineplot( data = re_df,  x = '연령대', y= '시도코드', hue = '간기능_결과', palette = 'hls')
plt.show()
```


    
![output_38_0](https://user-images.githubusercontent.com/26592315/163104281-6cc9d11b-e4ed-4d7b-be1f-ec520e855847.png)




```python
re_df2 = re_df
re_df2.reset_index(level=['간기능_결과'], inplace = True)
re_df2.reset_index(level=['연령대'], inplace = True)

df_per = df['연령대'].value_counts().to_frame()
df_per.rename(columns = {'연령대':'총 인구'},inplace=True)
df_per["연령대"] = df_per.index

re_df2 = pd.merge(re_df2, df_per, left_on='연령대', right_on='연령대', how='left')

re_df2.rename(columns = {"시도코드" :"수"}, inplace =True)

re_df2["간기능_비율"] = re_df2["수"] / re_df2["총 인구"] * 100

import seaborn as sns

plt.figure(figsize=(20,10))

sns.lineplot( data = re_df2,  x = '연령대', y= '간기능_비율', hue = '간기능_결과', palette = 'hls')
plt.show()

```


![output_39_0](https://user-images.githubusercontent.com/26592315/163104282-6a2b51df-7dde-456b-9d5e-bfae0dcd88fb.png)




```python
re_df2
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
      <th>연령대</th>
      <th>간기능_결과</th>
      <th>수</th>
      <th>총 인구</th>
      <th>간기능_비율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>40대</td>
      <td>검사 필요</td>
      <td>13136</td>
      <td>300442</td>
      <td>4.372225</td>
    </tr>
    <tr>
      <th>1</th>
      <td>40대</td>
      <td>정상</td>
      <td>245188</td>
      <td>300442</td>
      <td>81.609096</td>
    </tr>
    <tr>
      <th>2</th>
      <td>40대</td>
      <td>주의</td>
      <td>42118</td>
      <td>300442</td>
      <td>14.018679</td>
    </tr>
    <tr>
      <th>3</th>
      <td>50대</td>
      <td>검사 필요</td>
      <td>14784</td>
      <td>317794</td>
      <td>4.652070</td>
    </tr>
    <tr>
      <th>4</th>
      <td>50대</td>
      <td>정상</td>
      <td>248944</td>
      <td>317794</td>
      <td>78.335022</td>
    </tr>
    <tr>
      <th>5</th>
      <td>50대</td>
      <td>주의</td>
      <td>54066</td>
      <td>317794</td>
      <td>17.012908</td>
    </tr>
    <tr>
      <th>6</th>
      <td>60대</td>
      <td>검사 필요</td>
      <td>12433</td>
      <td>241749</td>
      <td>5.142938</td>
    </tr>
    <tr>
      <th>7</th>
      <td>60대</td>
      <td>정상</td>
      <td>181512</td>
      <td>241749</td>
      <td>75.082834</td>
    </tr>
    <tr>
      <th>8</th>
      <td>60대</td>
      <td>주의</td>
      <td>47804</td>
      <td>241749</td>
      <td>19.774229</td>
    </tr>
    <tr>
      <th>9</th>
      <td>70대</td>
      <td>검사 필요</td>
      <td>4776</td>
      <td>110377</td>
      <td>4.326988</td>
    </tr>
    <tr>
      <th>10</th>
      <td>70대</td>
      <td>정상</td>
      <td>85331</td>
      <td>110377</td>
      <td>77.308678</td>
    </tr>
    <tr>
      <th>11</th>
      <td>70대</td>
      <td>주의</td>
      <td>20270</td>
      <td>110377</td>
      <td>18.364333</td>
    </tr>
    <tr>
      <th>12</th>
      <td>80대</td>
      <td>검사 필요</td>
      <td>851</td>
      <td>29638</td>
      <td>2.871314</td>
    </tr>
    <tr>
      <th>13</th>
      <td>80대</td>
      <td>정상</td>
      <td>24458</td>
      <td>29638</td>
      <td>82.522437</td>
    </tr>
    <tr>
      <th>14</th>
      <td>80대</td>
      <td>주의</td>
      <td>4329</td>
      <td>29638</td>
      <td>14.606249</td>
    </tr>
  </tbody>
</table>
</div>



# 당뇨병


```python
import seaborn as sns

re_df = df.groupby(['연령대','당뇨병_결과'])[['시도코드']].count()
plt.figure(figsize=(20,10))

sns.lineplot( data = re_df,  x = '연령대', y= '시도코드', hue = '당뇨병_결과', palette = 'hls')
plt.show()
```


    
![output_42_0](https://user-images.githubusercontent.com/26592315/163104285-6f7ade64-324c-4d5d-9236-6351ed7b64fa.png)

    



```python
re_df2 = re_df
re_df2.reset_index(level=['당뇨병_결과'], inplace = True)
re_df2.reset_index(level=['연령대'], inplace = True)

df_per = df['연령대'].value_counts().to_frame()
df_per.rename(columns = {'연령대':'총 인구'},inplace=True)
df_per["연령대"] = df_per.index

re_df2 = pd.merge(re_df2, df_per, left_on='연령대', right_on='연령대', how='left')

re_df2.rename(columns = {"시도코드" :"수"}, inplace =True)

re_df2["당뇨병_비율"] = re_df2["수"] / re_df2["총 인구"] * 100

import seaborn as sns

plt.figure(figsize=(20,10))

sns.lineplot( data = re_df2,  x = '연령대', y= '당뇨병_비율', hue = '당뇨병_결과', palette = 'hls')
plt.show()
```


    
![output_43_0](https://user-images.githubusercontent.com/26592315/163104286-d0c3f3e9-910e-4061-a1ac-e57d35253e7b.png)



### 당뇨(혈당) 정상인 환자의 수가 급격하게 줄어서 마치 나이가 들수록 당뇨병에 걸리는 것 처럼 보이지만 비율로 살펴보면 나이가 들수록 정상의 비율이 감소하지 않은 것으로 보아 나이와 당뇨의 관계는 강한 상관관계는 아니다. 

---

## 혈압환자 & 간 환자 & 당뇨병 환자 를 지도로 나타내기


```python
problem = df[(df['혈압_결과'] == '주의') & (df['간기능_결과'] == '주의') & (df['당뇨병_결과'] == '주의')]

import folium
from folium.plugins import MarkerCluster
m = folium.Map(
    location=[37.559819, 126.963895],
    zoom_start=12, 
    tiles='cartodbpositron'
)

folium.GeoJson(
    seoul_geo,
    name='지역구'
).add_to(m)

marker_cluster = MarkerCluster().add_to(m)

for lat, long in zip(problem['위도'], problem['경도']):
    folium.Marker([lat, long], icon = folium.Icon(color="green")).add_to(marker_cluster)

m
```
![image](https://user-images.githubusercontent.com/26592315/163107267-c22463f0-172b-4093-a9cc-ead983cd73bc.png)

- md파일이여서 folium을 png로 나타냄.


```python
hospital = pd.read_csv("./의료기관_및_병상수_20220408104132.csv", encoding='euc-kr')

```


```python
hospital = hospital[hospital['행정구역별(2)'] == '소계']
hospital= hospital.drop(2)

```


```python
hospital = hospital[['행정구역별(1)','2018.1']]
hospital.rename(columns = {"2018.1" :"병원 수"}, inplace =True)
hospital.rename(columns = {"행정구역별(1)" :"시도명"}, inplace =True)

```


```python
# hospital = pd.merge(hospital, city, left_on='시도명', right_on='시도명', how='outer')
```


```python
hospital
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
      <th>시도명</th>
      <th>병원 수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>서울특별시</td>
      <td>17387</td>
    </tr>
    <tr>
      <th>29</th>
      <td>부산광역시</td>
      <td>5134</td>
    </tr>
    <tr>
      <th>46</th>
      <td>대구광역시</td>
      <td>3723</td>
    </tr>
    <tr>
      <th>55</th>
      <td>인천광역시</td>
      <td>3284</td>
    </tr>
    <tr>
      <th>66</th>
      <td>광주광역시</td>
      <td>2099</td>
    </tr>
    <tr>
      <th>72</th>
      <td>대전광역시</td>
      <td>2244</td>
    </tr>
    <tr>
      <th>78</th>
      <td>울산광역시</td>
      <td>1350</td>
    </tr>
    <tr>
      <th>84</th>
      <td>세종특별자치시</td>
      <td>257</td>
    </tr>
    <tr>
      <th>85</th>
      <td>경기도</td>
      <td>14211</td>
    </tr>
    <tr>
      <th>117</th>
      <td>강원도</td>
      <td>1590</td>
    </tr>
    <tr>
      <th>136</th>
      <td>충청북도</td>
      <td>1874</td>
    </tr>
    <tr>
      <th>148</th>
      <td>충청남도</td>
      <td>2273</td>
    </tr>
    <tr>
      <th>164</th>
      <td>전라북도</td>
      <td>2375</td>
    </tr>
    <tr>
      <th>179</th>
      <td>전라남도</td>
      <td>2003</td>
    </tr>
    <tr>
      <th>202</th>
      <td>경상북도</td>
      <td>2791</td>
    </tr>
    <tr>
      <th>226</th>
      <td>경상남도</td>
      <td>3645</td>
    </tr>
    <tr>
      <th>245</th>
      <td>제주특별자치도</td>
      <td>860</td>
    </tr>
  </tbody>
</table>
</div>




```python
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
      <th>기준년도</th>
      <th>가입자 일련번호</th>
      <th>시도코드</th>
      <th>성별코드</th>
      <th>연령대 코드(5세단위)</th>
      <th>신장(5Cm단위)</th>
      <th>체중(5Kg 단위)</th>
      <th>허리둘레</th>
      <th>시력(좌)</th>
      <th>시력(우)</th>
      <th>...</th>
      <th>음주여부</th>
      <th>구강검진 수검여부</th>
      <th>위도</th>
      <th>경도</th>
      <th>BMI</th>
      <th>BMI_결과</th>
      <th>혈압_결과</th>
      <th>간기능_결과</th>
      <th>당뇨병_결과</th>
      <th>연령대</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020</td>
      <td>1</td>
      <td>36</td>
      <td>1</td>
      <td>9</td>
      <td>165</td>
      <td>60</td>
      <td>72.1</td>
      <td>1.2</td>
      <td>1.5</td>
      <td>...</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.525640</td>
      <td>127.268516</td>
      <td>22.04</td>
      <td>정상체중</td>
      <td>주의</td>
      <td>정상</td>
      <td>정상</td>
      <td>40대</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020</td>
      <td>110</td>
      <td>36</td>
      <td>2</td>
      <td>17</td>
      <td>145</td>
      <td>55</td>
      <td>81.0</td>
      <td>0.6</td>
      <td>0.4</td>
      <td>...</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.525640</td>
      <td>127.268516</td>
      <td>26.16</td>
      <td>과체중</td>
      <td>정상</td>
      <td>정상</td>
      <td>정상</td>
      <td>80대</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020</td>
      <td>455</td>
      <td>36</td>
      <td>1</td>
      <td>10</td>
      <td>170</td>
      <td>75</td>
      <td>88.0</td>
      <td>0.7</td>
      <td>1.0</td>
      <td>...</td>
      <td>1.0</td>
      <td>1</td>
      <td>36.525640</td>
      <td>127.268516</td>
      <td>25.95</td>
      <td>과체중</td>
      <td>주의</td>
      <td>정상</td>
      <td>정상</td>
      <td>40대</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020</td>
      <td>481</td>
      <td>36</td>
      <td>2</td>
      <td>13</td>
      <td>150</td>
      <td>60</td>
      <td>80.0</td>
      <td>0.6</td>
      <td>0.3</td>
      <td>...</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.525640</td>
      <td>127.268516</td>
      <td>26.67</td>
      <td>과체중</td>
      <td>주의</td>
      <td>정상</td>
      <td>정상</td>
      <td>60대</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020</td>
      <td>574</td>
      <td>36</td>
      <td>1</td>
      <td>10</td>
      <td>170</td>
      <td>80</td>
      <td>90.0</td>
      <td>0.8</td>
      <td>1.0</td>
      <td>...</td>
      <td>1.0</td>
      <td>0</td>
      <td>36.525640</td>
      <td>127.268516</td>
      <td>27.68</td>
      <td>과체중</td>
      <td>주의</td>
      <td>검사 필요</td>
      <td>정상</td>
      <td>40대</td>
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
      <td>...</td>
    </tr>
    <tr>
      <th>999995</th>
      <td>2020</td>
      <td>999693</td>
      <td>49</td>
      <td>1</td>
      <td>10</td>
      <td>160</td>
      <td>85</td>
      <td>99.0</td>
      <td>0.9</td>
      <td>1.2</td>
      <td>...</td>
      <td>1.0</td>
      <td>0</td>
      <td>33.392688</td>
      <td>126.494894</td>
      <td>33.20</td>
      <td>고도비만</td>
      <td>고혈압</td>
      <td>주의</td>
      <td>검사 필요</td>
      <td>40대</td>
    </tr>
    <tr>
      <th>999996</th>
      <td>2020</td>
      <td>999710</td>
      <td>49</td>
      <td>1</td>
      <td>10</td>
      <td>170</td>
      <td>70</td>
      <td>88.0</td>
      <td>1.5</td>
      <td>1.5</td>
      <td>...</td>
      <td>1.0</td>
      <td>0</td>
      <td>33.392688</td>
      <td>126.494894</td>
      <td>24.22</td>
      <td>정상체중</td>
      <td>고혈압</td>
      <td>주의</td>
      <td>정상</td>
      <td>40대</td>
    </tr>
    <tr>
      <th>999997</th>
      <td>2020</td>
      <td>999750</td>
      <td>49</td>
      <td>1</td>
      <td>12</td>
      <td>165</td>
      <td>75</td>
      <td>95.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>1.0</td>
      <td>1</td>
      <td>33.392688</td>
      <td>126.494894</td>
      <td>27.55</td>
      <td>과체중</td>
      <td>주의</td>
      <td>주의</td>
      <td>정상</td>
      <td>50대</td>
    </tr>
    <tr>
      <th>999998</th>
      <td>2020</td>
      <td>999802</td>
      <td>49</td>
      <td>1</td>
      <td>10</td>
      <td>170</td>
      <td>70</td>
      <td>92.0</td>
      <td>0.2</td>
      <td>1.0</td>
      <td>...</td>
      <td>1.0</td>
      <td>1</td>
      <td>33.392688</td>
      <td>126.494894</td>
      <td>24.22</td>
      <td>정상체중</td>
      <td>정상</td>
      <td>주의</td>
      <td>정상</td>
      <td>40대</td>
    </tr>
    <tr>
      <th>999999</th>
      <td>2020</td>
      <td>999828</td>
      <td>49</td>
      <td>1</td>
      <td>9</td>
      <td>175</td>
      <td>100</td>
      <td>101.0</td>
      <td>0.8</td>
      <td>0.7</td>
      <td>...</td>
      <td>1.0</td>
      <td>0</td>
      <td>33.392688</td>
      <td>126.494894</td>
      <td>32.65</td>
      <td>고도비만</td>
      <td>주의</td>
      <td>정상</td>
      <td>정상</td>
      <td>40대</td>
    </tr>
  </tbody>
</table>
<p>1000000 rows × 32 columns</p>
</div>




```python
df = pd.merge(df, city, left_on='시도코드', right_on='시도코드', how='outer')
```


```python
sick = df[(df['혈압_결과'] == '주의') | (df['간기능_결과'] == '주의') | (df['당뇨병_결과'] == '주의')].groupby('시도명')[['시도코드']].count()
sick
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
      <th>시도코드</th>
    </tr>
    <tr>
      <th>시도명</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>강원도</th>
      <td>20899</td>
    </tr>
    <tr>
      <th>경기도</th>
      <td>155557</td>
    </tr>
    <tr>
      <th>경상남도</th>
      <td>41930</td>
    </tr>
    <tr>
      <th>경상북도</th>
      <td>35868</td>
    </tr>
    <tr>
      <th>광주광역시</th>
      <td>16771</td>
    </tr>
    <tr>
      <th>대구광역시</th>
      <td>29766</td>
    </tr>
    <tr>
      <th>대전광역시</th>
      <td>19298</td>
    </tr>
    <tr>
      <th>부산광역시</th>
      <td>41121</td>
    </tr>
    <tr>
      <th>서울특별시</th>
      <td>103293</td>
    </tr>
    <tr>
      <th>세종특별자치시</th>
      <td>3990</td>
    </tr>
    <tr>
      <th>울산광역시</th>
      <td>16920</td>
    </tr>
    <tr>
      <th>인천광역시</th>
      <td>37524</td>
    </tr>
    <tr>
      <th>전라남도</th>
      <td>25276</td>
    </tr>
    <tr>
      <th>전라북도</th>
      <td>24054</td>
    </tr>
    <tr>
      <th>제주특별자치도</th>
      <td>7534</td>
    </tr>
    <tr>
      <th>충청남도</th>
      <td>27809</td>
    </tr>
    <tr>
      <th>충청북도</th>
      <td>21693</td>
    </tr>
  </tbody>
</table>
</div>




```python
sick.reset_index(level=['시도명'], inplace = True)
sick.rename(columns = {"시도코드" :"수"}, inplace =True)
sick
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
      <th>시도명</th>
      <th>수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>강원도</td>
      <td>20899</td>
    </tr>
    <tr>
      <th>1</th>
      <td>경기도</td>
      <td>155557</td>
    </tr>
    <tr>
      <th>2</th>
      <td>경상남도</td>
      <td>41930</td>
    </tr>
    <tr>
      <th>3</th>
      <td>경상북도</td>
      <td>35868</td>
    </tr>
    <tr>
      <th>4</th>
      <td>광주광역시</td>
      <td>16771</td>
    </tr>
    <tr>
      <th>5</th>
      <td>대구광역시</td>
      <td>29766</td>
    </tr>
    <tr>
      <th>6</th>
      <td>대전광역시</td>
      <td>19298</td>
    </tr>
    <tr>
      <th>7</th>
      <td>부산광역시</td>
      <td>41121</td>
    </tr>
    <tr>
      <th>8</th>
      <td>서울특별시</td>
      <td>103293</td>
    </tr>
    <tr>
      <th>9</th>
      <td>세종특별자치시</td>
      <td>3990</td>
    </tr>
    <tr>
      <th>10</th>
      <td>울산광역시</td>
      <td>16920</td>
    </tr>
    <tr>
      <th>11</th>
      <td>인천광역시</td>
      <td>37524</td>
    </tr>
    <tr>
      <th>12</th>
      <td>전라남도</td>
      <td>25276</td>
    </tr>
    <tr>
      <th>13</th>
      <td>전라북도</td>
      <td>24054</td>
    </tr>
    <tr>
      <th>14</th>
      <td>제주특별자치도</td>
      <td>7534</td>
    </tr>
    <tr>
      <th>15</th>
      <td>충청남도</td>
      <td>27809</td>
    </tr>
    <tr>
      <th>16</th>
      <td>충청북도</td>
      <td>21693</td>
    </tr>
  </tbody>
</table>
</div>




```python
sick = pd.merge(sick, hospital, left_on='시도명', right_on='시도명', how='left')
```


```python
sick['병원 수'] = sick['병원 수'].astype('int64')
```


```python
sick['비율'] = sick["수"] / sick['병원 수'] * 100
sick.sort_values(by='비율')
```


## 병원 하나의 예비 환자 수


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
      <th>시도명</th>
      <th>수</th>
      <th>병원 수</th>
      <th>비율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>서울특별시</td>
      <td>103293</td>
      <td>17387</td>
      <td>594.081785</td>
    </tr>
    <tr>
      <th>4</th>
      <td>광주광역시</td>
      <td>16771</td>
      <td>2099</td>
      <td>798.999524</td>
    </tr>
    <tr>
      <th>5</th>
      <td>대구광역시</td>
      <td>29766</td>
      <td>3723</td>
      <td>799.516519</td>
    </tr>
    <tr>
      <th>7</th>
      <td>부산광역시</td>
      <td>41121</td>
      <td>5134</td>
      <td>800.954422</td>
    </tr>
    <tr>
      <th>6</th>
      <td>대전광역시</td>
      <td>19298</td>
      <td>2244</td>
      <td>859.982175</td>
    </tr>
    <tr>
      <th>14</th>
      <td>제주특별자치도</td>
      <td>7534</td>
      <td>860</td>
      <td>876.046512</td>
    </tr>
    <tr>
      <th>13</th>
      <td>전라북도</td>
      <td>24054</td>
      <td>2375</td>
      <td>1012.800000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>경기도</td>
      <td>155557</td>
      <td>14211</td>
      <td>1094.623883</td>
    </tr>
    <tr>
      <th>11</th>
      <td>인천광역시</td>
      <td>37524</td>
      <td>3284</td>
      <td>1142.630938</td>
    </tr>
    <tr>
      <th>2</th>
      <td>경상남도</td>
      <td>41930</td>
      <td>3645</td>
      <td>1150.342936</td>
    </tr>
    <tr>
      <th>16</th>
      <td>충청북도</td>
      <td>21693</td>
      <td>1874</td>
      <td>1157.577375</td>
    </tr>
    <tr>
      <th>15</th>
      <td>충청남도</td>
      <td>27809</td>
      <td>2273</td>
      <td>1223.449186</td>
    </tr>
    <tr>
      <th>10</th>
      <td>울산광역시</td>
      <td>16920</td>
      <td>1350</td>
      <td>1253.333333</td>
    </tr>
    <tr>
      <th>12</th>
      <td>전라남도</td>
      <td>25276</td>
      <td>2003</td>
      <td>1261.907139</td>
    </tr>
    <tr>
      <th>3</th>
      <td>경상북도</td>
      <td>35868</td>
      <td>2791</td>
      <td>1285.130777</td>
    </tr>
    <tr>
      <th>0</th>
      <td>강원도</td>
      <td>20899</td>
      <td>1590</td>
      <td>1314.402516</td>
    </tr>
    <tr>
      <th>9</th>
      <td>세종특별자치시</td>
      <td>3990</td>
      <td>257</td>
      <td>1552.529183</td>
    </tr>
  </tbody>
</table>
</div>



# 세종시에 병원이 제일 부족, 서울이 병원이 여유

- 결론: 병원을 지을거면 세종시.

# BMI 파헤치기


```python
# 성별 열 추가
df["성별"] = df["성별코드"]
df.loc[df[df["성별코드"] == 1].index, "성별"] = "남성"
df.loc[df[df["성별코드"] == 2].index, "성별"] = "여성"
```


```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.rcParams['axes.spines.top'] = False # 위쪽 축 제거
plt.figure(figsize=(15,8))
fig, ax = plt.subplots()
ax2 = ax.twinx()

sns.barplot(ax = ax, data = df.sort_values(by="연령대 코드(5세단위)"), x = '연령대', y = 'BMI', hue = '성별', palette = 'hls')
# sns.lineplot(ax = ax2, data = df2, x = '연령대', y = '건당금액', hue = '성별', palette = ['red', 'blue'], marker = 'o')
plt.title('연령대 별 BMI 수치')
plt.grid(axis = 'y', color = 'lightgray', linestyle = '--', linewidth = 1.5)
plt.show()

```


    <Figure size 1080x576 with 0 Axes>




![output_62_1](https://user-images.githubusercontent.com/26592315/163104287-c218d867-43c8-4b79-b070-b71425e99646.png)




```python
plt.figure(figsize=(15,8))
sns.boxplot(data=df,  x = '연령대', y = 'BMI', hue = '성별')
plt.show()
```


    
![output_63_0](https://user-images.githubusercontent.com/26592315/163104268-fd7858b4-c668-45fb-93c7-1bc08b55a4c2.png)




```python
df = pd.merge(df, city, left_on='시도코드', right_on='시도코드', how='outer')
```


```python

```


```python
df_bmi = df.pivot_table(index="연령대", columns="시도명", values="BMI", aggfunc="mean")
plt.figure(figsize=(20,10))
sns.heatmap(df_bmi, annot=True, fmt=".1f")
plt.show()
```


    
![output_66_0](https://user-images.githubusercontent.com/26592315/163104271-8a0201fa-6755-417a-b998-7405c10fa691.png)

    



```python
plt.figure(figsize=(20,5))
sns.boxplot(data=df, x="시도명", y="BMI")  
```




    <AxesSubplot:xlabel='시도명', ylabel='BMI'>




    
![output_67_1](https://user-images.githubusercontent.com/26592315/163104273-f68bbfe4-2677-4a97-b676-d3ff808889a0.png)



> # 평균적인 비만율은 제주도가 높지만 BMI가 가장 높은 시도는 경기도다


```python

```
