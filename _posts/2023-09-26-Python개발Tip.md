---
title: "개발Tip(Python)"
layout: post
date: 2023-09-26 12:34:00 +0900
category: Tip
---



1. dataframe

```python

# strip()을 사용하면 양쪽 끝 공백을 줄여주고, strip([]) 처럼 안의 값을 넣으면 양쪽 끝의 [ ]을 지워 준다. 
# 즉 strip은 중간의 공백이나 문자는 못지우고 문자열 양쪽 끝의 공백이나 특정 문자를 지워준다.
strip()





# 배열에서 최대값과 해당 인덱스 찾기
# 1번
max_value, max_index = max((value, index) for index, value in enumerate(arr))
# 2번
max_index = arr.index(max(arr))


# dataframe에서 합성 된 list 에서 가장 큰 값의 index를 추출하는 코드 
tem_dif['plus correct'] = [tem_dif.loc[a,'plus'].index(max(tem_dif.loc[a,'plus'])) +1 for a in range(0,len(tem_dif))]

# dataframe에서 map 이용

# map을 이용해서 if문 처럼 이용하기.
tem_dif['plus ox'] = (tem_dif['answer'] ==tem_dif['plus correct']).map({True: 'O', False: 'X'})

```