---
title: "CodingTest-Tip (Java)"
categories:
  - CodingTest
feature_text: |
  The History of the CodingTest
---



## Python

## Dictionary 이용
```python
answer = []
a = list(set(report))
dictionary2 = {name : 0 for name in id_list}
dictionary = {name : [] for name in id_list}
for i in a:
    dictionary[i.split()[1]].append(i.split()[0])

print(dictionary)
for i in dictionary:
    print(dictionary[i])

# {'muzi': ['apeach'], 'frodo': ['muzi', 'apeach'], 'apeach': [], 'neo': ['muzi', 'frodo']}

# ['apeach']
# ['muzi', 'apeach']
# []
# ['muzi', 'frodo']

#----

answer = [0] * len(id_list)

answer[id_list.index(i.split()[0])] 
# 이렇게 하면 answer(배열) 원하는 index에 담을 수 있다. 


# ---

wd = {'NNG':'일반명사', 'JKS':'주격조사'}
[(p1, wd.get(p2,'없음')) for p1, p2 in pos]  
# dictionary를 이용할 때 없을 경우를 대비하고 있으면, get을 이용하면 된다. get(df, ''), 두번째 인자에 대신할 값을 넣어주면 됨.
```


## for 문 이용

```python
for inst_idx, note in itertools.product(range(10)), range(50)):
  print('inst_idx: {}, note: {}'.format(inst_idx, note))
# 이렇게 itertools의 product를 이용하면,  출력으로 inst_idx: 0, note: 0 ~ 49 이 나오고 그 다음에
# inst_idx: 1, note: 0 ~ 49  이런 식으로 inst_idx: 9, note: 0 ~ 49 나온다.

```

[itertools — 효율적인 루핑을 위한 이터레이터를 만드는 함수](https://docs.python.org/ko/3/library/itertools.html)