---
title: "KOVO 한국배구연맹 V 리그 예측"
layout: post
date: 2022-04-20 22:46:00 +0900
category: KB-IT-Academy
---

- ## 프로젝트 설명
  - 5시즌의 KOVO 한국배구연맹 V 리그 기록을 크롤링해서 긁어온 후에 21/22시즌 3, 4월 경기를 구단 명과 스타팅멤버만을 가지고 예측하기.

## KOVO 한국배구연맹 V 리그 크롤링

- [소스 코드](https://github.com/SonHyeono/KB_IT_Academy/blob/main/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B6%84%EC%84%9D/KOVO%20%ED%95%9C%EA%B5%AD%EB%B0%B0%EA%B5%AC%EC%97%B0%EB%A7%B9%20V%EB%A6%AC%EA%B7%B8%20%EC%98%88%EC%B8%A1/KOVO%20%ED%95%9C%EA%B5%AD%EB%B0%B0%EA%B5%AC%EC%97%B0%EB%A7%B9%20V%EB%A6%AC%EA%B7%B8%20%ED%81%AC%EB%A1%A4%EB%A7%81%EC%BD%94%EB%93%9C.md)

- Selenium을 이용

- 5시즌 동안의 경기당 [ 팀명, 경기날짜, 결과, 이름, 공격종합_성공률, 오픈_성공률, 후위_성공률, 속공_성공률, 퀵오픈_성공률, 서브_성공률, 디그_시도, 디그_성공, 세트_시도, 세트_성공, 블로킹_시도, 블로킹_성공, 범실_범실, 포지션, 득점점유율, 스타팅멤버 ] 을 뽑아냄.

---

## KOVO 한국배구연맹 V 리그 예측

![image](https://user-images.githubusercontent.com/26592315/164896065-19ffc6a8-cedd-46f9-b07f-bf4f7024ea6f.png)

V 리그 남자부, 여자부 22년 3,4월 경기를 예측 코드

- [소스 코드](<https://github.com/SonHyeono/KB_IT_Academy/blob/main/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B6%84%EC%84%9D/KOVO%20%ED%95%9C%EA%B5%AD%EB%B0%B0%EA%B5%AC%EC%97%B0%EB%A7%B9%20V%EB%A6%AC%EA%B7%B8%20%EC%98%88%EC%B8%A1/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D_%EB%AF%B8%EB%8B%88%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8(%EB%82%A8%EC%9E%90)_%EC%86%90%ED%98%84%EC%98%A4.md>)

- [ 17/18시즌, 18/19시즌, 19/20시즌, 20/21시즌, 21/22시즌 ]

총 5년치의 데이터를 학습 (21/22시즌 3,4월 데이터 제외)

포지션 별로 해당 성공률을 측정,

| 범위           | 가중치 점수 |
| -------------- | ----------- |
| 하위 0 ~ 25%   | 1점         |
| 하위 25 ~ 50%  | 2점         |
| 상위 25% ~ 50% | 3점         |
| 상위 0 ~ 25%   | 4점         |

- 선수 별 등급

![image](https://user-images.githubusercontent.com/26592315/165033667-d949a624-b7c7-4777-acb1-e24501fc071d.png)

선수 별로 등급을 매긴 후, One-hot-Encoding으로 구단별로 상대한 선수들을 학습.

![image](https://user-images.githubusercontent.com/26592315/165034639-3e352ea9-69f5-4b44-b0ad-2b18232caa7b.png)

```python

# 구단 별 상대 선수를 추려내고 one-hot-encoding 함수
def df_train(club_name, df_v2, check = False, e = []):
    club = df_v2[df_v2['팀명'] == club_name]['경기번호'].to_frame()

    club_score = []
    for i in club['경기번호']:
        x = df_v2[(df_v2[ '경기번호'] == i) & (df_v2['팀명'] != club_name )]
        club_score.append({'경기날짜' : x['경기날짜'].values[0],'팀명' : x['팀명'].values[0] , '이름' : x['이름'].values[0],
                          '결과' : x['결과'].values[0],'경기번호':x['경기번호'].values[0]})

    club_score = pd.DataFrame(club_score)

    club_score.loc[:, player] = 0


    for i in range(len(club_score)):
        for j in club_score['이름'][i].split():
            try:

                club_score[j][i] = level_dict[j][0]
            except:
                continue

    club_score = pd.get_dummies(club_score, columns=['팀명'])

    club_score = club_score.drop(['경기날짜','경기번호','이름'], axis=1)

    club_score['결과'] = np.where(club_score['결과'] == True , 0, 1)

    if check == True:
        x_col = e.columns
        y_col = club_score.columns
        complement = list(set(x_col).difference(y_col))
        print(len(complement))

        club_score.loc[:, complement]  = 0



    return(club_score)
```

```python
df_Capital = df_train('현대캐피탈', df_v2)
df_korea = df_train('대한항공', df_v2)
df_KB = df_train('KB손해보험', df_v2)
df_Sam = df_train('삼성화재', df_v2)
df_OK = df_train('OK금융그룹', df_v2)
df_KoreaE = df_train('한국전력', df_v2)
df_Woori = df_train('우리카드', df_v2)
```

---

- pycaret으로 모델 선정

![image](https://user-images.githubusercontent.com/26592315/165034053-d8629bfd-f72b-4e6b-a84e-9662672f1a07.png)

```python

# 학습 모델 만들기 함수

def make_model(df_club):
    X = df_club.drop('결과',axis=1)
    y = df_club['결과']

    from sklearn.model_selection import train_test_split

    X_train, X_test, y_train, y_test = train_test_split(
        X,
        y,
    )

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
        model.fit(X_train, y_train)
        name = names[idx]
        train_score = model.score(X_train, y_train) * 100
        test_score = model.score(X_test, y_test) * 100
        print(f'{name} Train Accuracy:{train_score:.2f}%')
        print(f'{name} Test Accuracy:{test_score:.2f}%')
        print()

    return(X, y)

```

---

# 결과 21/22시즌 3, 4월 경기 예측 (남자부)

- ### 예측 데이터에서 주어진 값 : 구단명(2개), 스타팅멤버

---

# 현대캐피탈 3, 4월 예측 값

hard Train Accuracy:74.72%
hard Test Accuracy:71.43%
hard 예측값: [1 0 0 1 1 1 1]

knn1 Train Accuracy:70.22%
knn1 Test Accuracy:71.43%
knn1 예측값: [0 0 1 1 0 0 1]

lr Train Accuracy:89.33%
lr Test Accuracy:71.43%
lr 예측값: [1 0 0 1 1 1 1]

dt3 Train Accuracy:70.79%
dt3 Test Accuracy:71.43%
dt3 예측값: [1 0 0 1 1 1 1]

dt5 Train Accuracy:73.03%
dt5 Test Accuracy:71.43%
dt5 예측값: [1 0 0 1 1 1 1]

### 총 7경기 정확도 71.43%

---

# 대한항공 3, 4월 예측 값

soft Train Accuracy:79.12%
soft Test Accuracy:72.73%
soft 예측값: [1 1 1 0 1 1 1 1 1 1 1]

dt3 Train Accuracy:75.82%
dt3 Test Accuracy:72.73%
dt3 예측값: [1 1 1 0 1 1 1 1 1 1 1]

dt5 Train Accuracy:76.92%
dt5 Test Accuracy:72.73%
dt5 예측값: [1 1 1 0 1 1 1 1 1 1 1]

### 총 11경기 정확도 72.73%

---

# KB손해보험 3, 4월 예측 값

hard Train Accuracy:79.53%
hard Test Accuracy:72.73%
hard 예측값: [1 1 1 0 0 0 0 0 0 0 0]

knn2 Train Accuracy:78.36%
knn2 Test Accuracy:72.73%
knn2 예측값: [1 1 1 0 0 0 0 0 0 0 0]

lr Train Accuracy:94.74%
lr Test Accuracy:72.73%
lr 예측값: [1 1 1 0 0 0 0 0 0 0 0]

### 총 11경기 정확도 72.73%

---

# 삼성화재 3, 4월 예측 값

soft Train Accuracy:85.96%
soft Test Accuracy:75.00%
soft 예측값: [0 0 0 0 1 0 1 1]

dt3 Train Accuracy:61.99%
dt3 Test Accuracy:87.50%
dt3 예측값: [0 0 0 0 0 0 0 0]

### 총 8경기 정확도 87.50%

---

# OK금융그룹 3, 4월 예측 값

knn2 Train Accuracy:76.16%
knn2 Test Accuracy:71.43%
knn2 예측값: [0 0 0 1 1 0 0]

dt3 Train Accuracy:59.88%
dt3 Test Accuracy:71.43%
dt3 예측값: [0 0 0 0 0 0 0]

### 총 7경기 정확도 71.43%

---

# 한국전력 3, 4월 예측 값

knn2 Train Accuracy:80.36%
knn2 Test Accuracy:70.00%
knn2 예측값: [0 0 1 0 1 1 0 1 0 0]

lr Train Accuracy:95.24%
lr Test Accuracy:80.00%
lr 예측값: [1 0 1 1 1 1 0 1 0 1]

### 총 10경기 정확도 80.00%

---

# 우리카드 3, 4월 예측 값

hard Train Accuracy:83.71%
hard Test Accuracy:62.50%
hard 예측값: [0 0 0 0 1 1 1 1]

soft Train Accuracy:84.27%
soft Test Accuracy:62.50%
soft 예측값: [0 0 0 0 1 1 1 1]

knn1 Train Accuracy:76.97%
knn1 Test Accuracy:62.50%
knn1 예측값: [0 0 0 0 1 1 1 1]

knn2 Train Accuracy:78.09%
knn2 Test Accuracy:62.50%
knn2 예측값: [0 0 0 0 1 1 1 1]

lr Train Accuracy:91.57%
lr Test Accuracy:62.50%
lr 예측값: [0 0 0 0 1 1 1 1]

### 총 8경기 정확도 62.50%

---
