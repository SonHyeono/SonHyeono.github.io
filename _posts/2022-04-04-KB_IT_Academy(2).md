---
title: "Numpy와 Pandas 기본"
categories:
  - KB 국민은행 IT 아카데미
feature_text: |
  The History of the KB 국민은행 IT 아카데미 IT's Your Life
---



- [기본 데이터](#기본-데이터)

- [결측치](#결측치)

- [numpy](#numpy)

- [pandas](#pandas)

- [원하는 행 뽑기(특정문자로 찾기)](#원하는-행-뽑기-특정문자로-찾기)

- [sum](#sum)

- [where](#where)

## 꿀팁

```python

# 리스트 차집합
lst1 = ['A', 'B', 'C', 'D']
lst2 = ['C', 'D', 'E', 'F']
complement = list(set(lst1) - set(lst2))
print( complement ) # ['B', 'A']
complement = list(set(lst1).difference(lst2))
print( complement ) # ['A', 'B']

# 에러 끄기
pd.set_option('mode.chained_assignment',  None) 

# 열 별 고윳값 수 확인
df.nunique()

# 특정 열 타입 변경
df = df.astype({'meter_reading':'int'})

# groupby로 만든 DataFrame의 index 값을 열로 넣고 싶을 때
df2 = df.groupby('primary_use')[['meter_reading']].mean()  # 혹은 .to_frame()
df2.reset_index(level=['primary_use'], inplace = True)

# primary_use 열을 정수로 변환 (Label Encoding)
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()
label = df['primary_use']
le.fit(label)
label_encoded = le.transform(label)
df['primary_use'] = pd.DataFrame(label_encoded, columns=['label_encoded'])

# sns로 barplot
sns.barplot(x='cloud_coverage', y='meter_reading',data=df3)
plt.xticks(rotation=45) # x축 기울기 조절
plt.show()

# drop 열
df = df.drop('cloud_coverage',axis=1)

# min, max, mean, median, std, count
df.groupby('=')[''].agg(['min', 'max', 'mean', 'median', 'std', 'count'])

# timestamp를 datetime64로 변경
df['timestamp'] = df['timestamp'].astype('datetime64')

# timestamp에서 년, 분기, 월, 일, 요일, 시간을 추출하여 새 열 생성
df['year'] = df['timestamp'].dt.year
df['quarter'] = df['timestamp'].dt.quarter
df['month'] = df['timestamp'].dt.month
df['day'] = df['timestamp'].dt.day
df['dayofweek'] = df['timestamp'].dt.dayofweek
df['hour'] = df['timestamp'].dt.hour


reverse_word_index = dict([(value, key) for (key, value) in word_index.items()])
# ***(꿀팁)***
# 만약 word_index( dictionary )의 key, value의 위치를 바꾸고 싶을 때 하는 법 

reverse_word_index.get(i-3, '?') # 만약 dictionary에 없을 경우, '?'로 대체

```

## 기본


- 컬럼의 범위를 줘서 뽑아내고 싶으면 df.loc[: , "plcass" : "sex"] , loc를 이용한 범위 추출을 줄 수 있고, fancy indexing으로도 가능. 
- delimiter나 sep로 구분자를 설정해서 pd.read 가능
- df.['col'] 하면 Series가 나오고
- df.[['col']] 하면 DataFrame으로 나온다. (즉, list에 담으면 DataFrame 형태)
- 함수에서 inplace는 원본 데이터를 바꿀 것이냐 마냐이다.
- Shift+Tap 을 누르면 함수의 설명이 나온다
- datetime 타입에서는 dt 접근자로 날짜 속성에 접근 가능 ( df["date"].dt.year )
- 문자열 열(columns)의 함수 호출시 .str 사용 ( df["name"].str.문자열함수() )
- %whos : 매직 커맨드 ( 변수명, 유형, 데이터 정보를 상세히 반환합니다. )
- ascending=False 하면 내림차순. 기본은 오름차순
- 값이 return이 된다면 원본이 안 바뀐 것이기에, inplace를 True로 하거나 값을 덮어씌우기
- [범주형 데이터 url](https://runebook.dev/ko/docs/pandas/user_guide/categorical)
- 만약 (사용자)모듈을 import 하고나면 이미 메모리에 모듈이 올라가있기에 모듈을 수정을 해도 변경이 된 것이 적용이 안된다. 그래서 kernel Restart를 해야한다.
- DataFrame에서 변경을 할 때 DataFrame.loc[] 에 값을 넣어야한다~ 그 행을 찾아서 넣기
- sort_values에서 Series( [] )면 컬럼을 안줘도 되지만 DataFrame( [[]] )이면 컬럼을 by로 꼭 줘야한다.

## 기본 데이터 

```python
# 타이타닉 데이터 
# 1. 함수로 뽑기
import seaborn as sns
sns.load_dataset("titanic")
# 2. github raw에서 데이터 값 가져오기, 이건 메모리에 저장해서 실행
url = 'https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv'
pd.read_csv(url)
```

## numpy

np.bincount() : 정수데이터의 0부터 최대값까지의 빈도수

np.unique(문자/정수배열, return_counts=True) 하면 문자열 빈도수 나옴( 이때 return_counts=True를 해야한다)

```pthon
arr1.reshape(-1,3,2) # -1은 적절하게 단 한번만 알아서 나타내줌. (즉 나누어서 값을 제대로 적기 귀찮을 때 -1 로 하면 됨.)
```

## pandas

```python

# 데이터 읽기

import pandas as pd
apt_price = pd.read_csv(
    "./아파트(매매)__실거래가_20220401113837.csv",
    skiprows= 15,          # 몇번째 줄까지 생략할 것인지, skip하고 데이터 읽기 위해서
    encoding="euc-kr",
    thousands=",") # thousands=","를 하면 숫자에 찍힌 comma를 지움.

# -------------------------------------------

df.info() # 정보 확인
df.columns # 열 확인
df.head()  # 데이터 상위 확인, tail은 하위
df.describe() # 요약 통계 
df['columns 명'].value_counts() # 개별 컬럼별로 각각의 값의 횟수
df['columns 명'].quantile() # 분위, 동등한 크기로 분할하는 지점 .quantile(0.8) 이면 80%
df['columns 명'].mode()[0] # 최빈값 뽑기

df['columns'] = True # 새로운 컬럼 추가 (임의의 값을 대입해서 새로운 컬럼을 추가가능)
apt_price["평"] = apt_price["전용면적(㎡)"] / 3.03 # 새로운 컬럼 추가 예시

df_copy = df.copy() # 복사본 만들기
df.corr()   # 상관관계, -1에 가까울수록 반비례 관계, 1에 가까울수록 정비례 관계 
df.corr()["survived"] # Series로 해당하는 열에 관한 다른 열과의 상관관계
df.corr()[["survived"]] # DataFrame으로 해당하는 열에 관한 다른 열과의 상관관계

# ------------------------------------------
titanic.corr()["survived"]['age']  # Series의 경우는 column을 주면 되고
titanic.corr()[["survived"]].loc['age','survived']  #DataFrame의 경우는 loc로 해야한다.
# ------------------------------------------

df.count() # DataFrame 전체의 개수를 구하는 경우

df['age'].count()  # 단일 column의 데이터 개수

df.shape() # 데이터의 (행, 열) 크기

df['age'].unique() # 열에서 유일한 값

b = titanic['who'] == 'child'
titanic[b].count() # who 컬럼에서 child 인 행의 개수 
# titanic.loc[b, 'who'].count()   # 위의 조건에서 who 컬럼의 개수만 구하기  

#데이터 삭제
titanic.drop(titanic.index[titanic[titanic['sex'] == 'male'].index]) # 남성인 데이터 삭제하기, male인 index를 지우기
df.drop(df.index[0:10])  # 0~9까지 index 데이터 지우기

# 열 삭제
df.drop('class', axis=1)
df.drop(['first', 'second'], axis=1) # 열 여러개 삭제

# e notation 표현 방식 변경
pd.options.display.float_format = '{:..2f}'.format 


# split한 값을 이용하고 싶으면 항상 str로 접근해야한다. str[1]을 하면 분할 된것들의 1번째 값들이 다 나온다.
apt_price["시군구"].str.split().str[1]



```

## 결측치

```python
df.isnull()
df.isna()
df.notnull()
df.fillna(10)  # 결측치에 ()괄호안의 값으로 채워넣음. ex) 열의 평균을 구하고 그 값을 채워넣기 
df.fillna(10, inplace=True)  # 원본에 반영시키는 방법 : 1. inplace 속성을 True로 해주기 2. 값을 덮어씌우기
df.dropna()  # 결측치 제거하기, any가 기본이고 any(nan이 1개라도 존재시 drop), all(모두 nan이면 drop)

# 칼럼별 걸측치 개수
titanic.isna().sum()

# 비정상 데이터 출력
df.loc[df['age'].isnull()]  # 참이 나오는 것이 결측치

# 결측치 index 뽑기
b = titanic["age"].isna()
age_na_idx = titanic[b].index
age_na_idx
# titanic.loc[age_na_idx, :] # 해당 index의 데이터 값들 뽑기

```

## 원하는 행 뽑기( 특정문자로 찾기 )

```python
b = df["행정구역"].str.contains("면")  
#  내가 원하는 값이 들어가 있는 행 뽑을 때 쓰는 방법! 
df[b]
```

## sum

```python
sum() 
np.sum()  # sum 보다 컴파일 시간이 빠르다. ( numpy가 C기반의 라이브러리 ) 
np.cumsum() # np.sum과 비슷하고 축에 따라서 누적 합계   

# 제일 빠르고 강력한 sum은 CPU 병렬화 or GPU 병렬화 이다.
```


## where

- numpy.where()
    `np.where(조건, 참, 거짓)`
    ```python
    df['predict'] = np.where(df['predict'] == -1, 1, 0)
    ```

- pandas.where()

    `df.where(cond, other=nan, inplace=False, axis=None, level=None, errors='raise',try_cast=False)`
    
    `df.where(조건, 조건이 거짓일 경우 대체 값, 원본을 수정할 것인가?(inplace) ... )`



## Series

```python
# 문자열

# 각 문자열 항목에 len을 대신 호출하기 위해서 Series에서는 str을 사용
df.who.str.len()  # who라는 열에서 각 행의 문자열 길이를 구하기

apt_price["시군구"].str.split()  # Series 항목별로 split()을 하기 위해서는 str이 필요하다. str은 컬럼의 항목들이 문자열이여야함.

```

## datetime

- ***datetime 타입에서는 dt 접근자로 날짜 속성에 접근 가능***

```python
# datetime 타입에서는 dt 접근자로 날짜 속성에 접근 가능
import numpy as np

apt_price["계약일"] = np.where( apt_price["계약일"] < 10,
"0"+apt_price["계약일"].astype(str),
apt_price["계약일"].astype(str) )
apt_price["계약년월일"] = apt_price["계약년월"].astype(str) + apt_price["계약일"]
apt_price["계약년월일"] = pd.to_datetime( apt_price["계약년월일"] )
apt_price.info()

# 다은과 같이 년월일로 문자열(혹은 년-월-일)을 맞쳐주고 pd.to_datetime으로 datetime으로 변환가능하다.

df['date'].dt.dayofweek # 요일이 계산이 됨. ( 0 이 월요일 )

```

## 데이터 구간 분할

```python
# 카테고리 타입(범주)로 나눠주는 cut 함수를 이용해서 데이터를 구분지어줍니다.
apt_price["평형"] = pd.cut(
    apt_price["평"],
    bins=[0,10,20,30,40,50,60,1000], # 구간경계값
    labels=['10평이하', '10평대', '20평대', '30평대', '40평대', '50평대','50평이상']
)
# Series 형식으로 나오기에 새로운 컬럼에 더한다. 

apt_price["평형"].value_counts() # 평수대로 개수가 나온다.  

```

## groupby

- ***연속형일 경우는 cut으로 잘라서 범주형으로 바꾸고 groupby를 지어야한다.***

- ***계층적 index가 편하다.***

```python
df.groupby("columns 명")  # 컬럼을 기준으로 group을 지어준다.

# 그룹별로 통계

df.groupby("columns").mean()  # group을 지어준 것 끼리 컬럼을 기준으로 통계 ( 모든 열 )

# 생존율

titanic.groupby("who")["survived"].mean()  # who 열에서 group을 지어주고 생존율, 즉 위의 그룹별로 통계에서 열을 선택한 것.

# 같은 성별별로 좌석 등급을 나눈다.
titanic.groupby(['sex','pclass'])['survived'].mean()

titanic.groupby(["sex","pclass"])[["survived","age"]].mean() # 선택할 열이 여러개면 [[]] 로 묶기

# 여러가지 통계 값을 적용할 때는 agg()를 사용! 
titanic.groupby(["sex","pclass"])[["survived","age"]].agg(["mean","max"])


```

![image](https://user-images.githubusercontent.com/26592315/161486642-6fd8d5f4-5f0a-4ff3-8064-cee82abbd219.png){: width="100%" height="100%"}{: .center}

![image](https://user-images.githubusercontent.com/26592315/161489191-8ce0f713-5b8e-41a9-af7f-0168bc5c50ae.png){: width="100%" height="100%"}{: .center}    


## pivot_table

```python
df.pivot_table(index="column", values= "") # 세로로 표가 만들어지고 values에는 통계 대상이 되는 column
df.pivot_table(columns="column", values="") # 가로로 표가 만들어짐, values에는 통계 대상이 되는 column

# pivot은 통계 대상을 직접 정해줘야합니다.

# index가 main이고 만약, index와 columns를 둘다 쓰게 되면 메인인 index 기준으로 먼저 나누고, 각각을 columns기준으로 다시 나눈다.

df.pivot_talbe(index="column", columns="column", values="", aggfunc=['sum','mean'])  # 다중 통계 함수 적용할 때, pivot에서는 aggfunc


```


## apply

```python
# 시리즈 타입에 apply를 적용하면, 시리즈의 항목들이 전달이 됨.
df['who'].apply(함수명)  # apply 괄호 안에는 함수가 들어가는데 ()를 뒤에 적으면 안된다. ()를 적으면 return값이 넘어가기에.  apply(함수명()) ( X )


def f1(x):
    if x=="man": return "남자"
    elif x=="woman": return "여자"
    elif x=="child": return "아이"
    
titanic['who'].apply(f1)

'''
0      남자
1      여자
2      여자
3      여자
4      남자
       ..
886    남자
887    여자
888    여자
889    남자
890    남자
Name: who, Length: 891, dtype: object
'''

~.apply(f, axis= 0)  # apply에서 axis=0, 1을 줄 수 있다.
# axis = 0 은 행 방향, 1은 열 방향


# 데이터 양이 많을 경우  apply를 이용하면 한번만 훑는다.
def get_date(x):                        
    return x[0:4] + x[6:8] + x[9:11] 
w["날짜"].apply(get_date)

```

## concat

- 기본 값은 axis=0, axis=1을 하게되면 옆으로 연결 됨.
- concat은 pandas에 있는 함수, append는 DataFrame에 있는 함수.

```python
gas3 = pd.concat([gas1, gas2]) # 하면 index 그대로 DataFrame이 연결이 된다.
gas3.reset_index() # 그렇기에 reset_index 해줘야한다. (그러나 그 전 index가 있어서 그걸 삭제해줘야함.)

# ------- reset_index가 번거로우면
pd.concat([gas1, gas2], ignore_index=True)  # ignore_index를 하게 되면 새롭게 concat해도 새롭게 index가 생김.

# ---------------------
# 열 병합에서 index가 중요

# concat에도 join이 있다.

```

## merge

- 기본적으로 같은 column을 연결한다. (column명이 같은 것을 기준으로)

```python
pd.merge(score1, score2)  # 만약 같은 column이 없으면 error가 난다.
# 병합하려는 컬럼의 이름이 다른 경우
# left_on, right_on에 각각의 컬럼명을 지정해주면 그것이 기준이 되어서 합병이 된다.
pd.merge(score1, score2, left_on="이름",right_on="학생이름")

# column이름이 동일한 것들이 여러개 있으면, error가 나고 on에 지정을 해줘야한다.
pd.merge(score1, score2, on="이름")

```
## lambda


```python

titanic['who'].apply(
    lambda x: "남자" if x=="man" else 
    "여자" if x=="woman" else "아이").value_counts()
```

## table 뽑기

```python
pd.read_html(url) # url의 table을 뽑아내진다. (웹사이트 마다 헤더가 필요한 경우도 있다. )

```














