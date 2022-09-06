---
title: "데이터 분석을 위한 머신러닝/딥러닝"
layout: post
date: 2022-04-11 20:46:00 +0900
category: KB 국민은행 IT 아카데미
---

## 데이터 분석 기본

- 시각화 - 데이터의 패턴찾기(머신러닝으로 상세한 패턴 찾기 가능) -

## 기본 지식

- stratify 인자는 train과 test 데이터 세트의 범주 비율을 동일하게 유지해 줌.
- train 데이터와 test 데이터를 나누기 위해서 사용하는 train_test_split 함수에서 파라미터인 random_state의 경우는 성능에 영향을 미치기도 하지만 실제 개발에 있어서 값을 주지는 않는다. 다만 결과값이 상대방과 똑같고 싶으면 random_state를 줘서 결과값을 같게 한다.

- Feature : 칼럼(특성)이다. ( 독립변수, Attribute라고도 함 )
- Label : 우리가 최종적으로 알아내고 싶은 값 ( 독립변수에 따라서 값이 변하기에 종속변수 , Class라고도 함.)
- Scikit-learn : Object Detection이 필요, 간단한 이미지의 분류는 가능하지만 이미지 안에 뭐가 있고 등 복잡한 일은 못한다. 그래서 딥러닝이 복잡한 일을 해야한다.
- keras와 pytorch가 인기있다.
- Bunch 타입 : 딕셔너리 타입과 같다. (Key와 Value 존재)
- CPU는 정수 연산, 메모리는 실수 연산 ( 그래서 실수 연산에서는 그래픽카드가 중요 )
- numpy array 끼리 하면 항목별로 계산이 반복 ( numpy에는 자동 반복 기능이 내장 )
- column이 많으면(차원이 많으면) 계산량이 많기에 차원을 축소해서 계산량을 줄이기.
- 대표값을 뽑아내는 것을 모수적, 원래값이 뭔지 몰라~ 이러면 비모수적
- k: 가장 가까운 이웃의 개수, 홀수로 준다.
- 거리: 맨하탄과 유클리드 거리가 있고, ( 두점사이의 직선 거리: 유클리드 ), ( 두점 사이의 거리를 면따라 가는 것이 맨하탄 거리 )
- model.score(x_test, y_test) 를 이용하면, 정답율이 나온다.
- 표준화(평균 0, 표준편차 1), 정규화(0~1 사이의 값으로 바꿈) 중요

  ```python
    # 표준화
    from sklearn.preprocessing import StandardScaler
    scaler = StandardScaler()
    x_train_sc = scaler.fit_transform(x_train) # numpy ndarray 형태로 바뀜
    x_test_sc = scaler.transform(x_test)
    # 정규화
    from sklearn.preprocessing import MinMaxScaler
    scaler = MinMaxScaler()
    x_train_sc = scaler.fit_transform(x_train)  # numpy ndarray 형태로 바뀜
    x_test_sc = scaler.transform(x_test)

    # 결과
    from sklearn.neighbors import KNeighborsClassifier
    model = KNeighborsClassifier(n_neighbors=3).fit(x_train_sc, y_train)
    model.score(x_train_sc, y_train), model.score(x_test_sc, y_test)

  ```

  - numpy ndarray 형태가 되면 iloc 등 안됨.

- KNN -> estimator (예측기)
- 훈련데이터를 fit으로 세팅하고, 예측을 함.
- fit_transform(x_train) : fit하고 transform까지 한꺼번에 x_train의 min, max값으로 변환
- scaler.transfrom(x_test) : 0~1사이를 벗어나는 값이 생길수 있다. train과 test의 최대, 최소값이 다르기 때문에
- 값들이 한쪽에 치중되면 학습이 잘 안되고, 정규화가 되어야지 학습이 잘 된다.
- 잔차: 예측 값과 실제 값의 차이
- 편향 : 절편
- CV: 교차 검증

## 매개변수 지식

```python
x_train , x_test, y_train, y_test = train_test_split(
    iris.data,
    iris.target,
    random_state=20220411,
    stratify=iris.target)
```

- random_state를 설정하면 난수가 같아짐. -> 임의 값을 선택하는 기준, 결과가 같아짐
- stratify : 내가 배분하고 싶은 비율의 값(즉 y의 값)을 비슷하게 만들어줌. (비율의 층) stratify를 주지 않으면 배분의 비율이 임의이다.
- 모델의 파라미터 : (verbose=1)를 하면 학습할 때 로그를 찍어줌.

## 머신러닝 알고리즘 종류

- (데이터의 패턴 인식방법)
  - 데이터끼리의 거리 ( 분류 - 종류예측 , ex) 승패예측, 승진여부예측 ... )
  - 직선방정식 ( 회귀- 숫자 예측 , ex) 연봉예측, 승률예측 ... )
  - 확률 ( 분류 ) { 딥러닝에서 가장 많이 이용 }

## 이상치(Outlier) 처리

```python
Q1 = x_train['sepal width (cm)'].quantile(0.25)
Q3 = x_train['sepal width (cm)'].quantile(0.75)
IQR = Q3 - Q1
MIN = Q1 - 1.5 * IQR

MAX = Q3 + 1.5 * IQR
MIN, MAX

target = x_train[(x_train['sepal width (cm)'] < MIN) | (x_train['sepal width (cm)'] <MAX>) ]
target

x_train = x_train.drop(target.index)
y_train = y_train.drop(target.index)
```

## 로그 변환(Log Trasnfromation)

- 데이터의 분포가 극단적으로 모였을 때 로그 변환을 적용하여 왜도를 제거할 수 있음.(이외에도 루트, Box-Cox 변환 가능)
- 로그 변환시 데이터가 0인 경우 -inf로 변환되기에 인지.
  - 해결 방안 : np.log 함수가 아니라 np.log1p 함수를 이용하여 해결 가능
  - 원래 값으로 변환하기 위해서 np.expm1함수를 사용
  - np.log1p : log(1 + x)
  - np.expm1 : exp(x) - 1

## K-Nearest Neighbor (KNN)

- scikit-learn 범주의 개수가 동일 한 경우 첫번째 레이블로 예측
- 분류 모델: KNeighborsClassifier ( 종류를 파악 )
- 회귀 모델: KNeighborsRegressor ( 숫자를 파악 )
- target이 들어와야 계산, KNN은 학습만(fit을 이용)
- model.predict로 계산.
- KNeighborsClassifier의 파라미터
  - n_jobs : 동시 실행할 CPU 개수
  - n_neighbors : 목표점에 가까운 값을 몇개로 기준을 하겠는가?

## 회귀분석

- 단순 회귀(1개이며, 직선)
- 다중 회귀(개수가 N개이면서 패턴이 선형)
- 다항 회귀(개수가 N개이면서 패턴이 비선형)
- 비선형 회귀 분석(비선형)

- 회귀선 => 예측선
- 오차를 최소화 할수 있는 직선의 방정식
- 회귀 분석 성능 평가 척도

  - R-Squared : 1에 가까울수록 성능이 좋다. (실제 값의 분산 대비 예측 값의 분산 비율)
  - Mean Absolute Error : 실제 값과 예측 값의 차이를 절댓값으로 변환해 평균 계산( 작을 수록 좋지만 과적합 가능성 O )
  - Mean Squared Error : 실제 값과 예측 값의 차이를 제곱해서 평균 계싼 ( 작을 수록 좋지만 과적합 가능성 O , 이상치에 민감)
  - RMSE : 제곱을 하면 값이 커지기에 루트를 씌움(너무 크면 log를 씌워서 비교하는 방법도 있음), 모델 간의 잔차를 비교(이상치에 덜 민감함, 큰 오류값 차이에 크게 패널티)

- Linear Regjoinsion(선형 회귀)의 구현 방법으로는 최소 제곱법과 경사 하강법이 존재

  - 최소 제곱법:

    잔차 제곱의 합이 최소가 되는 기울기와 편향은 편미분을 통해 도출 ( 잔차 제곱의 합이 최소가 되도록 기울기(Weight)와 편향(Bias)을 찾음 )

    장점: 간단하게 식을 유도 가능

    단점: 데이터가 많아지면 계산량이 엄청 증가, 데이터에 이상치가 있는 경우 성능 하락

    ```python
    def OLS(x,y):
        w = np.sum((x-x.mean()) * (y-y.mean())) / np.sum((x-x.mean())**2)
        b = y.mean() - w * x.mean()
        return w, b

    ```

    코드는 이렇게 되고, 모델은 제공된다.

    ```python
      from sklearn.linear_model import LinearRegression
      model = LinearRegression().fit(x.reshape(-1,1), y)  # reshape에서 -1은 알아서 계산,  즉 1열로 하고 행은 데이터에 맞추어서 지정.
      model.coef_, model.intercept_
    ```

    linear_model.LinearRegression으로 구현되어 있다.

    - coef\_ : 가중치 값 조회 가능
    - intercept\_ : 편향 값 조회 가능

    - scikit-learn의 머신 러닝 모델의 특성은 2차원 데이터만 올 수 있기 때문에 1차원 데이터를 2차원 데이터로 변환 후에 학습하고 가중치 및 편향 값 조회한다.

  - 경사 하강법:

    - 비용 함수를 미분하여 비용이 낮아지는 방향으로 가중치 값을 변경하는 알고리즘

    - 단점: 수행 시간이 오래 걸림.

    ```python
    import numpy as np
    np.random.seed(0)  # 이걸 적으면 난수의 값이 매번 같아져서 결과도 같아진다.
    X = np.arange(50)
    Y = (2 * X) + 10 * np.random.randn(50)
    plt.plot(X, Y, 'b.')

    W = 1
    W*X

    w_range = np.arange(0.1, 4.1, 0.1)

    costs = []
    for w in w_range:
        h = w * X
        cost = 1/50 * np.sum((h-Y)**2)
        costs.append(cost)

    plt.plot(w_range, costs, 'r.')

    # 오차가 커진다는 것은 답에서 멀어진다.
    # 답에 가까울 수록 기울기가 줄어든다.
    ```

    ```python
    plt.plot(w_range, costs, 'r.')
    for w, cost in zip(w_range, costs):
        h = w * X
        gradient = 2 / 50 * np.sum( (h-Y) * X)
        plt.plot(w_range, gradient*(w_range-w)+cost)
        plt.axis([0,4,0,3000])
    plt.show()   # 답은 2 , 기울기가 2였음.
    ```

    ![image](https://user-images.githubusercontent.com/26592315/162882972-601e6924-e1ea-4500-92c0-986fe1749b29.png)

    - 하강 속도를 추가하여 현재 가중치 값에서 빼는 것을 반복.

    - Stochastic Gradient Descent : 확률적 경사 하강법.
      - 답에 가까울수록 천천히 줄어들고 멀수록 많이 줄어든다.
      - 가변적으로 접근

## Logistic Regression (로지스틱 회귀)

- 선형 회귀 분석과 달리 예측하고자 하는 레이블이 범주형인 경우 사용되는 모델
- 선형 회귀 모델 기반으로 확률 모델로 접근
- Cost 함수 ( 확률이기 때문에 MSE가 아닌 Cross Entropy 사용)
- Cost 최소화 ( Cost 값이 0에 가까울 수록 이상적 값)
- 로지스틱 회귀 모델의 특징

  - 모델의 예측 값은 범주 레이블(예: 정상(0), 불량(1))으로 얻어질 수 없고, 범주별 확률값을 반환 함.
  - 분류 기준(Cut-off value)을 정의하여 확률을 레이블로 변환

- 알고리즘 동작 과정
  - Step 1: 로지스틱 회귀 모델을 학습시켜 예측 확률 P(Y=1 | X=x) 계싼
  - Step 2: 분류 기준(Cut-off value) 를 결정
  - Step 3: P(Y=1 | X=x)가 분류 기준보다 클경우 1, 작을 경우 0으로 분류

```python
import pandas as pd

# delimiter나 sep로 구분자를 설정해서 read 가능
redwine = pd.read_csv("red_wine.csv",delimiter=';')
redwine['type'] = 0
whitewine = pd.read_csv("white_wine.csv",delimiter=';')
whitewine['type'] = 1
wine = pd.concat([redwine, whitewine])
wine

X = wine.iloc[:, :-1]
Y = wine['type']
X.shape, Y.shape

# ((6497, 12), (6497,))

from sklearn.model_selection import train_test_split
x_tr, x_te, y_tr, y_te = train_test_split(
    X,
    Y,
    random_state = 0,
    test_size=0.25,
    stratify=Y
)

from sklearn.linear_model import LogisticRegression
model = LogisticRegression(max_iter=10000).fit(x_tr, y_tr)
model.score(x_tr, y_tr), model.score(x_te, y_te)

# (0.9844006568144499, 0.9852307692307692)
```

- wine 데이터에서는 stratify를 주지않는 것이 score 값이 높긴하지만 비율을 정해주는 것이 좋다.

---

## 다항 회귀 ( PolynomialFeatures )

```python

# 보스턴 데이터 세트에 2차항 변환(상수항 미포함) 적용

import pandas as pd

url = 'https://raw.githubusercontent.com/vincentarelbundock/Rdatasets/master/csv/MASS/Boston.csv'

df = pd.read_csv(url)
df.drop("Unnamed: 0", axis=1, inplace=True)

P = PolynomialFeatures(degree=2, include_bias=False)  # degree(차수)를 너무 높이면 과적합, test에서 오차가 커짐.
# 차수가 높으면 훈련 데이터에 너무 적합해서 테스트에서는 성능이 떨어진다.
# 점을 skip해가면서 학습하는 것도 과적합을 막는 방법.
x_poly = P.fit_transform(df.loc[:, 'crim':'lstat'])
x_train, x_test, y_train, y_test = train_test_split(x_poly, y, random_state=0)
df.loc[:, 'crim':'lstat'].shape, x_poly.shape

# 모델 생성 및 학습
# 다항 변환된 데이터를 학습 시 성는 향상

model = LinearRegression().fit(x_train, y_train)
model.score(x_train, y_train), model.score(x_test, y_test)

```

```python

from sklearn.preprocessing import PolynomialFeatures
P = PolynomialFeatures(degree=3, include_bias=False)
x_poly = P.fit_transform(x)
x_poly.shape  # 왜 2차가 9차로 변하냐면, (a+b)^3이라서

```

- 2개의 열을 3차로 변환하면 다음과 같이 된다. ( (a+b)^3 식을 푼 개수 )
  - ['x0', 'x1', 'x0^2', 'x0 x1', 'x1^2', 'x0^3', 'x0^2 x1', 'x0 x1^2', 'x1^3']
  - 총 9차가 된다.

```python
  from sklearn.datasets import load_boston
  boston = load_boston()
  boston_df = pd.DataFrame(boston['data'], columns = boston['feature_names'])
  boston_df["PRICE"] = boston.target
  boston_df
  x = boston_df.iloc[:, : -1]
  y = boston_df.loc[:, "PRICE"]
  x.shape

  # (506, 13)

  from sklearn.model_selection import train_test_split
  x_tr, x_te, y_tr, y_te = train_test_split(
      x, y, random_state = 0, test_size=0.25
  )

  from sklearn.linear_model import LinearRegression
  model = LinearRegression().fit(x_tr, y_tr)
  model.score(x_tr, y_tr), model.score(x_te, y_te)

  # (0.7697699488741149, 0.6354638433202129)

  from sklearn.preprocessing import PolynomialFeatures
  P = PolynomialFeatures(degree=2, include_bias=False)
  x_poly = P.fit_transform(x)
  x_poly.shape
  # P.get_feature_names()

  # (506, 104)

  from sklearn.model_selection import train_test_split
  x_tr, x_te, y_tr, y_te = train_test_split(
      x_poly, y, random_state = 0, test_size=0.25   # x 대신에 2차를 적용한 x_poly로 분할
  )

  from sklearn.linear_model import LinearRegression
  model = LinearRegression().fit(x_tr, y_tr)
  model.score(x_tr, y_tr), model.score(x_te, y_te)

  # (0.952051960903273, 0.6074721959725392)
```

- 2차로 변환한 값을 집어 넣으니깐 train 데이터에서 정확도가 올라간다.
- test 데이터에서 정확도가 낮아졌지만, 적절한 차수를 주면 test 데이터의 정확도가 높아지는 경우도 있다.

---

## 규제화 (Regularization)

- 다항 회귀 시 차수가 높아 질수록 과대 적합이 발생하여 예측 성능이 저하되는 문제 ( 모의 고사는 높은데 본 시험은 낮은 것 )
- 80점 이상이 되어야지 신뢰성이 있다.
- R-Square 값이 0.9 넘거나 가까이 있어야 신뢰.
- 규제 모델

  - L2 규제 가중치 (Ridge Regression)

    - L2를 많이 씀.
    - 가중치들의 제곱의 합이 최소가 되도록 적절한 가중치와 편향을 찾음
    - Alpha 값을 크게 주면 큰 값들이 작아져서 크기가 대체로 비슷해진다.

  - L1 규제 가중치 적용 (Lasso Regression)

    - 가중치들의 절대값의 합이 최소가 되도록 하는 적절한 가중치와 편향을 찾음.
    - Alpha 값을 크게 주면 중요도가 떨어지는 값들을 없어진다.

  - L1 + L2 규제 가중치 적용 (Elastic Net)
