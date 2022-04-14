---
title: "데이터 분석을 위한 머신러닝/딥러닝 (2)"
categories:
  - KB 국민은행 IT 아카데미
feature_text: |
  The History of the KB 국민은행 IT 아카데미 IT's Your Life
---



## 기본지식

- predict의 경우 2차원이여야 한다고 늘 상 생각하기. [[ ]]

Logistic Regression에서는 문자형 안되기에, Label Encoding (부호화) 을 해서 숫자로 바꿔줘야한다.

- One Hot Encoding : 
    - 문자열 범주형을 숫자로 바꿔줌.
    - 해당 열만 1로 바꿔주기에 나머지는 0으로 답에 영향을 안 미친다. 
    - pandas의 get_dummies 함수를 통해 사용 가능
    - get_dummies
        - 숫자형 열은 그대로 두고 문자형 열은 새로운 DataFrame으로 One Hot Encoding 해준다.
        - 숫자형도 바꾸고 싶으면, get_dummies(df, columns=['열이름'])을 이용해서 숫자형도 바꿔줄 수 있다.
    ```python
    import pandas as pd
    X = pd.get_dummies(X, columns=['pclass','sex'])
    ````

- 시간은 범주형으로 처리

## 분류 분석

- AUC, Curve 영역의 면적이 분류 성능


## Decision Tree

```python
from sklearn.tree import DecisionTreeClassifier
model = DecisionTreeClassifier().fit(x_train, y_train)
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
