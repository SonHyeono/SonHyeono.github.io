---
title: "Data Analyst 기본기"
categories:
  - Data_Analyst
feature_text: The History of the Data_Analyst
---

# Data Analyst 기본기

- 전처리

```python

pd.DataFrame(total_corr.values, index= total_corr.index, columns = ['Corr'])
# 다음과 같이 dataframe으로 만들고자 할때, list주고 index와 columns 명을 지정해주면 원하는대로 만들어진다.

# 데이터 프레임 순서바꾸기
df_pred = df_pred[['ID','Class']]

```

- 데이터 저장

```python
df_sample.to_csv("sample.csv",index=False)
# data frame저장 할때 index까지 같이 이중으로 저장이 되기에 index= False를 해줘야함.
```
