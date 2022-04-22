---
title: "데이터 분석을 위한 머신러닝 (2)"
categories:
  - KB 국민은행 IT 아카데미
feature_text: |
  The History of the KB 국민은행 IT 아카데미 IT's Your Life
---


## 평가

```python

# 학습, 평가 데이터로  R-squared, MSE, MAE 확인
from sklearn.metrics import r2_score
from sklearn.metrics import mean_squared_error
from sklearn.metrics import mean_absolute_error

pred_train = model.predict(X_train)
pred_test = model.predict(X_test)
print('Load')
print('R squared : ', r2_score(Y_train,pred_train), r2_score(Y_test,pred_test) )
print('Mean Squared Error: ', mean_squared_error(Y_train,pred_train), mean_squared_error(Y_test, pred_test))
print('Mean Absolute Error: ', mean_absolute_error(Y_train,pred_train), mean_absolute_error(Y_test,pred_test) )

```

## 기본지식


- predict의 경우 2차원이여야 한다고 늘 상 생각하기. [[ ]]

Logistic Regression에서는 문자형 안되기에, Label Encoding (부호화) 을 해서 숫자로 바꿔줘야한다.
```python
# 라벨 인코딩
from sklearn.preprocessing import LabelEncoder

for col in encoding_cols :
    df[col] = encoder.fit_transform(df[col])

df.head()
```
- One Hot Encoding : 
    - 문자열 범주형을 숫자로 바꿔줌.
    - 해당 열만 1로 바꿔주기에 나머지는 0으로 답에 영향을 안 미친다. 
    - pandas의 get_dummies 함수를 통해 사용 가능
    - get_dummies
        - 숫자형 열은 그대로 두고 문자형 열은 새로운 DataFrame으로 One Hot Encoding 해준다.
        - 숫자형도 바꾸고 싶으면, get_dummies(df, columns=['열이름'])을 이용해서 숫자형도 바꿔줄 수 있다.
    ```python
    # One Hot Encoding
    import pandas as pd
    X = pd.get_dummies(X, columns=['pclass','sex'])
    ````

- 시간은 범주형으로 처리

## 분류 분석

- AUC, Curve 영역의 면적이 분류 성능


## Decision Tree

```python
from sklearn.tree import DecisionTreeClassifier
model = DecisionTreeClassifier(max_depth= ).fit(x_train, y_train)
model.score(x_train, y_train), model.score(x_test, y_test)

model.feature_importances_

import pandas as pd
fi = pd.Series(model.feature_importances_, index=boston['feature_names'])
fi[fi!=0].sort_values(ascending=False).plot(kind='bar', figsize=(10,5))
# 특성 중요도가 0인 데이터를 제외하고 높은 순서대로 시각화 코드
```

- 좋은 분류 결과를 계싼하기 위해서 불순도(impurity)를 계산
- 불순도
    - Gini 계수 값, 불순도 ( 쪼개기 전의 불순도 값과 쪼갠 후의 불순도 값의 차이가 크면 클수록 좋다.)
        - 가장 불순도가 낮아지는 방향을 제일 먼저 잡는다.

    - Entropy 
        - log를 사용하는 계수

    - Gini를 선택하던지 Entropy를 선택하던지

    - 두 범주가 각각 반반씩 섞여 있는 경우 불순도가 최대이며 한 범주로만 구성되는 경우 불순도가 최소.

- Decision Tree 동작 과정
    - 결과 노드의 값을 이용하여 Gini 불순도를 계산
    - 불순도가 가장 낮은 값으로 분할을 하고 그 다음 낮은 값의 기준으로 또 분할을 하면서 Tree의 형태를 가짐. 
    
- 과대적합이 될 가능성이 높다.
- Tree의 leaf 노드가 분류 결과
- 모델 복잡도
    - min_samples_split, min_samples_leaf ( 정비례 , Parameter의 값이 일반화 )
    - max_depth, max_leaf_nodes ( 반비례 , Parameter의 값이 커질수록 과대 적합 )

- 가지치기(Pruning)
    - 과대적합을 막아줌. ( 너무 과도한 가지치기는 모델의 성능이 하락 )

- Regression Tree

    - 분할 기준 생성 과정
        - 분할 기준을 생성하기 위해서 가장 간단한 방법인 데이터를 2개의 그룹으로 만들고
        - 순서대로 2개의 학습 데이터를 선정 후 평균 값을 계산하여 분할 기준으로 지정
        - 지정된 기준으로 데이터를 분할하여 분할된 결과의 잔차 제곱합을 계산
        - 잔차의 제곱합이 가장 낮은 값을 Root 노드로 지정.





## Ensemble

- Voting(보팅)
    - 여러가지 알고리즘을 놓고, 같은 데이터를 다른 알고리즘에 집어 넣습니다.
        - Hard voting(직접 투표)
            - 각 모델의 예측 결과 중 많은 것을 선택
        - Soft voting( 간접 투표 )
            - 일반적으로 Soft Voting이 결과가 좋고
            - 각 모델의 클래스 확률 평균에서 평균 높은 확률을 선택

    ```python
    from sklearn.neighbors import KNeighborsClassifier
    from sklearn.linear_model import LogisticRegression
    from sklearn.tree import DecisionTreeClassifier

    knn1 = KNeighborsClassifier(n_neighbors=5)
    knn2 = KNeighborsClassifier(n_neighbors=3)
    lr = LogisticRegression(max_iter=10000)
    dt3 = DecisionTreeClassifier(max_depth=3)
    dt5 = DecisionTreeClassifier(max_depth=5)

    from sklearn.ensemble import VotingClassifier
    hard = VotingClassifier([('knn1', knn1), ('knn2', knn2), ('lr',lr), 
                            ('dt3',dt3), ('dt5',dt5)])
    soft = VotingClassifier([('knn1', knn1), ('knn2',knn2), ('lr',lr), 
                            ('dt3',dt3), ('dt5',dt5)], voting='soft')

    names = ['hard', 'soft', 'knn1', 'knn2', 'lr', 'dt3', 'dt5']
    for idx, model in enumerate([hard, soft, knn1, knn2, lr, dt3, dt5]):
        model.fit(x_train, y_train)
        name = names[idx]
        train_score = model.score(x_train, y_train) * 100
        test_score = model.score(x_test, y_test) * 100
        print(f'{name} Train Accuracy:{train_score:.2f}%')
        print(f'{name} Test Accuracy:{test_score:.2f}%')    
        print()

    # hard Train Accuracy:98.12%
    # hard Test Accuracy:95.10%

    # soft Train Accuracy:99.53%
    # soft Test Accuracy:95.10%

    # knn1 Train Accuracy:94.60%
    # knn1 Test Accuracy:91.61%

    # knn2 Train Accuracy:95.77%
    # knn2 Test Accuracy:91.61%

    # lr Train Accuracy:96.71%
    # lr Test Accuracy:93.71%

    # dt3 Train Accuracy:97.65%
    # dt3 Test Accuracy:93.01%

    # dt5 Train Accuracy:100.00%
    # dt5 Test Accuracy:90.91%

    ```

- Bagging(배깅)
    - 샘플을 여러 번 뽑아(Bootstrap) 각 모델을 학습시켜 결과물을 집계(Aggregation)
    - 분류 모델에서는 Voting을 히귀 모델에선 평균으로 집계 ( 중복 추출 허용 )

    - Random Forest
        ```python
        from sklearn.ensemble import RandomForestClassifier
        model = RandomForestClassifier(max_depth=5).fit(x_train, y_train)
        model.score(x_train, y_train), model.score(x_test, y_test)
        ```
        - 성능이 좋다. max_depth로 과대적합 조절
        - 단점
            - 시간이 다소 걸릴 수 있음.
            -  텍스트 데이터 같이 매우 차원이 높고 희소한(sparse) 데이터에는 잘 작동하지 않음.

    

- Boosting(부스팅)
    ```python
    from sklearn.ensemble import GradientBoostingClassifier
    model = GradientBoostingClassifier(max_depth=5).fit(x_train, y_train)
    model.score(x_train, y_train), model.score(x_test, y_test)
    ```
    - 여러 개의 약한 학습기(weak learner)를 순차적으로 연결하여 이전 모델에서 발생한 오류에 대해 높은 가중치를 부여하는 방법
    - Adaptive Boosting과 Gradient Boosting이 존재

- Stacking(스택킹)
    ```python
    from sklearn.ensemble import StackingClassifier
    estimators = [('rf', RandomForestClassifier()),
                ('gb', GradientBoostingClassifier())]
    model = StackingClassifier(estimators = estimators, final_estimator=LogisticRegression())

    model.fit(x_train, y_train).score(x_test, y_test)
    ```
    - 여러 모델이 예측한 결과 값을 다른 모델의 학습 데이터로 입력하여 재학습

## Grid Search

- 모델에 가장 적합한 하이퍼 파라미터(Hyper Parameter)를 찾기 위해서 사용
- 일반화 성능 향상을 통해 과대적합 현상을 개선할 수 있기 때문에 모델의 Hyper Parameter 튜닝 중요
- 최적의 Hyper Parameter 튜닝을 위해서는 실험 가능한 모든 조합을 학습하고 평가가 필요

```python
from sklearn.datasets import load_digits
digits = load_digits(as_frame=True)

x_data = digits.data
y_data = digits.target

# digits['data'].shape, digits['target'].shape

import pandas as pd
digits = pd.concat([x_data, y_data],axis=1)

from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import GridSearchCV
model = KNeighborsClassifier()
params = {
    'n_neighbors' : range(1,10),
}
gs = GridSearchCV(model, params).fit(digits.iloc[:, :-1], digits.iloc[:, -1])
report = pd.DataFrame(gs.cv_results_)
print( gs.best_score_ )
print( gs.best_params_ )
print( gs.best_estimator_ )
```

## 교차 검증 ( Cross Validation, CV )

- 고정적인 학습 데이터 세트로 모델을 만드는 경우 과대적합이 발생할 수 있고 이런 문제를 교차 검증을 통해 해결 가능.
- 단점으로는 데이터가 순차적으로 들어가 있는 경우 shuffle을 하지않는 경우 성능이 매우 나쁨.

```python
from sklearn.model_selection import cross_val_score
cross_val_score(model, digits.iloc[:, :-1], digits.iloc[:, -1],cv=5)

from sklearn.model_selection import cross_val_predict
cross_val_predict(model,digits.iloc[:, :-1], digits.iloc[:, -1], cv=5)
```

- k-겹 교차 검증(K-Fold Cross Validation)

    - 데이터를 동일한 개수인 K개의 Fold로 분할
    - 최적의 파라미터를 구하기 위한 모델 튜닝에서 주로 사용됨.

## XGBOOST ( Extreme Gradient Boost )

- pip install xgboost를 통해서 가능 

- Gradient 계열 답게 성능이 좋으나 과적합이 심함.

```python
import xgboost as xgb
from sklearn.datasets import load_boston
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score

boston = load_boston()

x_train, x_test, y_train, y_test = train_test_split(boston['data'],
                                                   boston['target'],
                                                   random_state=0)
model = xgb.XGBRegressor(objective='reg:linear')
model.fit(x_train, y_train)

p_train = model.predict(x_train)
p_test = model.predict(x_test)

r2_score(y_train, p_train), r2_score(y_test, p_test)

# ---

from xgboost import XGBClassifier

model = XGBClassifier().fit(X_train, y_train)
model.score(X_train, y_train), model.score(X_test, y_test)
```

## LightGBM

- pip install lightgbm 으로 설치 가능

- 10,000개 이상의 행을 가진 데이터에 사용하는 것을 권유 

```python
import lightgbm as lgb
from sklearn.datasets import load_boston
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score

boston = load_boston()

x_train, x_test, y_train, y_test = train_test_split(boston['data'],
                                                   boston['target'],
                                                   random_state=0)
lgb_train = lgb.Dataset(x_train, y_train)
lgb_eval = lgb.Dataset(x_test, y_test, reference=lgb_train)

params = {
    'objective':'regression',
}

model = lgb.train(params, lgb_train, valid_sets=lgb_eval,
                 early_stopping_rounds=5)

p_train = model.predict(x_train, num_iteration=model.best_iteration)
p_test = model.predict(x_test, num_iteration=model.best_iteration)

r2_score(y_train, p_train), r2_score(y_test, p_test)

# ---------------
from lightgbm import LGBMClassifier

model = LGBMClassifier().fit(X_train, y_train)
model.score(X_train, y_train), model.score(X_test, y_test)
```



## 군집 분석

- 주어진 데이터들을 특성에 따라 유사한 것끼리 묶음으로서 각 유형별 특징을 분석하는 기법
- 같은 군집 내 데이터들의 거리를 최소화하거나 다른 군집 간의 거리를 최대화하는 군집을 형성
    - 거리 척도는 유클리드 거리가 보편적으로 많이 사용됨.
- 거리만 잘 적용되면 모든 유형의 데이터에 적용이 가능하나 거리와 가중치 정의가 어렵고 결과 해석이 어려운 단점이 있음.

- 군집 방법론
    - 계층적 방법
    - 비계층적 방법

- 군집 분석의 예
    - 고객분류
    - 이상치 탐지
    - 이외에도 검색엔진, 차원 축소, 준지도 학습, 이미지 분할과 같은 영역에서도 사용 가능

- K-Means
    - 비지도 학습 기반의 대표적인 비계층적 군집 알고리즘
    - 사전에 정의된 군집 수 K개로 데이터를 분할
    - 최적의 군집 수 K를 정의하는 것이 많이 어려움
    - 군집 형성 과정
        - Step 1 : 랜덤하게 K개(사전의 정의)의 중앙점을 지정
        - Step 2 : 유클리드 거리를 이용하여 군집의 중심점과의 거리 계산,
                   가장 거리가 가까운 군짐으로 군집 할당
        - Step 3 : 군집 내 데이터의 평균을 계산 후 새로운 중심점으로 배정, 중심점이 더 이상 이동 안할 때까지 반복

    ```python
    from sklearn.datasets import make_blobs
    import matplotlib.pyplot as plt

    x,y = make_blobs(
        random_state=10, 
        n_samples=100,  # 행 개수
        n_features=2,   # 열 개수
        centers=3       # 중심 개수(그룹 개수)
    )
    # x[:5], y[:5]

    # plt.scatter(x[:, 0], x[:, 1], c=y)
    from sklearn.cluster import KMeans
    color = ['orange', 'green', 'red']
    K = KMeans(n_clusters=3).fit(x)      # color를 없애고, n_clusters의 개수는 데이터 개수만큼 가능하다.
    plt.scatter(x[:,0], x[:, 1], s=40, label='Sample')

    centers = K.cluster_centers_

    for idx, center in enumerate(centers):
        plt.scatter(center[0], center[1], s=100,
                label=f'Center {idx+1}', c=color[idx], marker='^')

    plt.legend()
    plt.show()

    # ----- 
    from sklearn.datasets import make_moons
    x, y = make_moons(200, noise=0.05, random_state=0)
    plt.scatter(x[:, 0], x[:, 1], c=y, s=50)

    from sklearn.cluster import KMeans

    labels = KMeans(n_clusters=2, random_state = 0).fit_predict(x)
    plt.scatter(x[:,0], x[:,1], c=labels, s=50)
    ```

- DBSCAN ( density-based spatial clustering of applications with noise )

    - 가까이에 있는 것들을 묶음, 밀집 기반 Clustering 
    - 클러스터의 개수를 미리 지정할 필요가 없다.
    - 복잡한 형상도 찾을 수 있으며, 어떤 클래스에서 속하지 않는 포인트를 구분할 수있음.
    - 병합군집이나 K-Means보다는 느리지만 비교적 큰 데이터셋에도 적용 가능
    - min_sampes와 eps에 값 변화에 따른 군집 결과를 분석해서 적정한 값 찾기

    ```python
    from sklearn.cluster import DBSCAN
    labels = DBSCAN().fit_predict(x)
    plt.scatter(x[:, 0], x[:, 1], c=labels, s=50)

    from sklearn.preprocessing import StandardScaler
    x_scaled = StandardScaler().fit_transform(x)

    labels = DBSCAN().fit_predict(x_scaled)
    plt.scatter(x_scaled[:, 0], x_scaled[:, 1], c=labels, s=50)

    # ---
    from sklearn.cluster import DBSCAN

    dbscan = DBSCAN(eps=6, min_samples=20)
    dbscan_labels = dbscan.fit_predict(df.iloc[:, :-1])

    # eps값과 min_samples의 값을 바꾸면서 군집을 확인한다.
    # 하이퍼 파라미터를 조절하면서 DBSCAN 모델을 학습
    # eps가 반지름, 군집형성을 잘 해야함.
    ```

## Confusion Matrix

```python
# 정답과 비교하여 confusion matrix를 구하세요. (그대로 실행)
from sklearn.metrics import confusion_matrix

pd.DataFrame(confusion_matrix(y_test, pred),
             index = [['Real']*3, [0,1,2]],
             columns = [['Predict']*3, [0,1,2]])
```


## Pycaret

- 기존에 있던 scikit-learn, XGBoost, LightGBM등 여러가지 머신러닝 라이브러리와 imblearn과 같은 데이터 전처리 라이브러리를 사용하기 용이하도록 ML High-Level API로 제작한 라이브러리
- 단 몇줄 만에 데이터 분석 및 머신러닝 모델 성능 비교까지 가능하고, Log를 기본적으로 생성
    - AutoML으로써 쉬운 난이도의 문제(이진 분류)의 경우 좋은 성능을 보임
- 분류, 회귀, 군집, 이상 탐지, 자연어 처리 기능을 제공

```python
# Anaconda Prompt를 관리자 권한으로 실행을 해서
# pip install pycaret --user pycaret 
    # pycaret 설치시 --user pycaret  추가하여 실행해야함

# wordcloud는 따로 다운받아 설치

# https://www.lfd.uci.edu/~gohlke/pythonlibs/#wordcloud 에서 
# wordcloud‑1.8.1‑cp39‑cp39‑win_amd64.whl 다운로드 후
# pip install wordcloud‑1.8.1‑cp39‑cp39‑win_amd64.whl 실행하여 설치

# 만약 colab google에서 실행하게 되면 !pip install pycaret이라고 하면 됨.
# colab에서 에러가 뜨면
# !pip install -U setuptools
# !pip uninstall scikit-learn -y
# !pip install scikit-learn==0.23.2 해주면 된다. 


# 회귀형

import pandas as pd
from sklearn.datasets import load_boston
boston = load_boston()
df = pd.DataFrame(boston['data'], columns=boston['feature_names'])
df['target'] = boston['target']
df.head()

from pycaret.regression import *

df_setup = setup(data=df, target='target', fold_shuffle=True, session_id=2)

compare_models()

## 분류형 

from pycaret.classification import *
df_setup = setup(data=iris, target='species')


top3 = compare_models(n_select=3, sort='Accuracy')
top3_tuned = [ tune_model(n) for n in top3 ]
top3_blend = blend_models(estimator_list=top3_tuned)
final_model = finalize_model(top3_blend)
pred = predict_model(final_model, data = iris.iloc[-20:])

from pycaret.utils import check_metric
check_metric(pred.species, pred.Label, metric="Accuracy")

# plot

plot_model(top3_blend, plot="error")

plot_model(top3_blend, plot="confusion_matrix")

```

- 회귀

![image](https://user-images.githubusercontent.com/26592315/163746053-bf697fea-5dfa-4007-9fa6-c555a640b181.png)


- 분류

![image](https://user-images.githubusercontent.com/26592315/163754235-0994cb2c-1611-46f3-87cb-ee828bfb65ca.png)

- 



- Pycaret 이용시 발생하는 error에 대한 [Stack overflow](https://stackoverflow.com/questions/67728802/valueerror-setting-a-random-state-has-no-effect-since-shuffle-is-false-you-sh)

- [Pycaret 관련 자료](https://wiki.wikisecurity.net/faq:pycaret_error_simpleimputer)

- [Pycaret plot](https://pycaret.gitbook.io/docs/)
- python 3.8버전 가능

- 모델 조합
    - blend_models()
    - 이전 단계에서 선택한 모델을 조합하여 더욱 강력한 앙상블 모델을 만듦.
- 모델 튜닝
    - tune_model()
    - 모델을 튜닝하여 예측 성능을 향상

- 최종 모델 학습
    - finalize_model()
    - 최종모델을 만들고 다시 한번 학습
- 예측
    - predict_model()
    - 만들어진 모델로 예측

