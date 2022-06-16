---
title: "CodingTest-Tip (Python)"
categories:
  - CodingTest
feature_text: The History of the CodingTest
---

## Python

## 인지 할 점

- 문제를 보고 탐색문제인지 빠르게 인지를 하고 재귀를 통해서 빠르게 전부 다 탐색하자.
- [백트래킹 문제](https://programmers.co.kr/learn/courses/30/lessons/87946)

## 주의 할 점

- zip 함수를 사용할 때 길이가 다를 경우 가장 짧은 인자를 기준으로 엮이고 나머지는 버려짐.
- round를 함부로 하지 말자. 보기에 편하라고 round를 하지만 실제 코딩테스트에서는 소수점 10번째 자리까지 비교할 수도 있다. round를 하지말자.

## 꿀팁

```python
# 리스트 원소들 count 쉽게 하기
from collections import Counter

counter = Counter(stages)  # stages는 리스트
# counter는 딕셔너리 형태로 나옴
# {"1":1,"2":3,"3":2,"4":1,"6":1} 다음과 같이

Counter(list).most_common() # 하면 딕셔너리형태로 ('이름','빈도') 순으로 내림차순 정렬됨

def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]
# collections는 객체 빼기가 가능하다. 그러면 둘이의 차이점이 나오고, keys를 뽑을수 있다.


# ---

# remove 함수는 특정한 값을 갖는 원소를 하나만 제거 한다. 모든 원소를 제거 하고 싶다면 아래와 같은 방법을 사용하자.

a =[1,2,3,4,5,5,5]
remove_set = {3,5}

result = [i for i in a if i not in remove_set]
print(result)
# [1,2,4]


#---

# 배열 벗기기
sum(sizes, [])
# [[14, 4], [19, 6], [6, 16], [18, 7], [7, 11]]   # 이것이 sizes인데
# [14, 4, 19, 6, 6, 16, 18, 7, 7, 11]  # sum을 실행하면 이렇게 됨.

print(* sizes)
# [14, 4] [19, 6] [6, 16] [18, 7] [7, 11] # 이건 이렇게!


# ---

# 이차원 배열 중복 제거

d = [[30, 20], [20,20], [40,30], [10,10], [10,10], [30,20]]

d = list(map(list,set(map(tuple,d))))
print(d)

# [[10, 10], [30, 20], [20, 20], [40, 30]]
# 일차원 배열은 set을 이용하고 이차원부터는 map을 이용해서 tuple로 변환하여 set해야한다.

#--

queue =  [(i,p) for i,p in enumerate(priorities)]
# [1, 1, 9, 1, 1, 1] 이거를 아래처럼 만들어준다.
# [(0, 1), (1, 1), (2, 9), (3, 1), (4, 1), (5, 1)]



#---

# any() : 리스트에서 하나라도 True인게 있으면 True
# all() : 리스트 모두 True여야 True 반환
```

## 꿀팁 2

- 1212 와 123을 문자열로 비교하면 123이 더 크다
- 만약 여러 조건에서 음수이면 0으로 return 해야할 경우 max(0, 조건) 하면 된다. if문 쓰지말고
- 등차 수열의 합 공식 ( 코드로 작성 할때 int일 경우 //을 이용해서 몫으로 해결)

$Sn$ = $n(a1 + an)\over 2$

## Dictionary 이용

```python
# key는 같으면 안된다!

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

wd.get('NNG')
# 값이 있으면 해당 value값이 나오고 없으면 None


# ---
# dictionary 쉽게 만들기!
keys = [1, 2, 3]
values = ["A", "B", "C"]
dict(zip(keys, values))
# {1: 'A', 2: 'B', 3: 'C'}


# ----

# key 값을 기준으로 오름차순 정렬하여 리스트 출력
sorted(dic)
# key 값을 기준으로 내림차순 정렬한 리스트 출력
sorted(dic, reverse=True)

# key 값을 기준으로 정렬된 (key,value) 원소쌍을 가진 리스트 출력
sorted(dic.items())

# key 값을 기준을 정렬된 딕셔너리 생성
dict(sorted(dic.items()))

# value 값을 기준으로 오름차순 정렬하여 (k, v) 리스트 반환
sorted(dic.items(), key=lambda x : dic[1])
# 위 값을 딕셔너리로 변환
dict(sorted(dic.items(), key=lambda x:x[1]))

# value 값을 기준으로 오름차순 정렬하여 key값 list 반환
sorted(dic,key=lambda x:dic[x])

```

## for 문 이용

```python
for inst_idx, note in itertools.product(range(10)), range(50)):
  print('inst_idx: {}, note: {}'.format(inst_idx, note))
# 이렇게 itertools의 product를 이용하면,  출력으로 inst_idx: 0, note: 0 ~ 49 이 나오고 그 다음에
# inst_idx: 1, note: 0 ~ 49  이런 식으로 inst_idx: 9, note: 0 ~ 49 나온다.

```

[itertools — 효율적인 루핑을 위한 이터레이터를 만드는 함수](https://docs.python.org/ko/3/library/itertools.html)

```python

[a for a in stages if a>=i]
# 이렇게도 가능

v = [list(range(10)),[10,11,12]]
[j for i in v for j in i]
# 	[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
[j for j in i for i in v ]
# 이렇게 하면 NameError: name 'i' is not defined 에러남. 즉, for문이 두개 일때는 먼저 해야하는 것이 앞으로 가야한다. (실제로 풀어 쓸 때랑 마찬가지로)
```

## map , filter

```python
 a = [1.2, 2.5, 3.7, 4.6]
 a = list(map(int, a))
# [1, 2, 3, 4]

# ---
a = list(map(str, range(10)))
# ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']


# filter -------

def is_man(user):
  return user["sex"] == "M"

for man in filter(is_man, users):
print(man)
# {'mail': 'gregorythomas@gmail.com', 'name': 'Brett Holland', 'sex': 'M'}
# {'mail': 'wwagner@gmail.com', 'name': 'Michael Jenkins', 'sex': 'M'}

# 위의 것을 람다로
for woman in filter(lambda u: u["sex"] != "M", users):
print(woman)
# {'mail': 'ujackson@gmail.com', 'name': 'Amber Rhodes', 'sex': 'F'}


#------------filter() 함수의 결과값을 list로 변환하는 가장 쉬운 방법은 list() 내장 함수를 사용하는 것입니다.
list(filter(A, B))

#-- 사실 파이썬에서는 filter() 함수를 사용하는 것보다 더 파이썬답게(pythonic) 데이터를 추려내는 방법이 있습니다. 바로 파이썬의 🌼이라고 불리는 list comprehension을 사용하는 방법


check_list = [[0] * n for _ in range(n)]
# nXn 행렬 만들기





```

## Asterisk(\*)

```python

numbers = [(1,2), (3, 4)]
print(*numbers)
# (1, 2) (3, 4)
# list가 벗겨짐

# ---

numbers = [1, 2, 3, 4, 5, 6]

# unpacking의 좌변은 리스트 또는 튜플의 형태를 가져야하므로 단일 unpacking의 경우 *a가 아닌 *a,를 사용
*a, = numbers
# a = [1, 2, 3, 4, 5, 6]

*a, b = numbers
# a = [1, 2, 3, 4, 5]
# b = 6

a, *b, = numbers
# a = 1
# b = [2, 3, 4, 5, 6]

a, *b, c = numbers
# a = 1
# b = [2, 3, 4, 5]
# c = 6

```

## 투 포인터, 슬라이딩 윈도우

- 투 포인터

```python
# 백준 2003
import sys
input = lambda : sys.stdin.readline().rstrip()

N, M = map(int,input().split())
arr = list(map(int,input().split()))

res = 0
sum = 0
l = 0
h = 0

while True:
    if sum >= M:
        sum -= arr[l]
        l += 1
    elif h == N:
        break
    else:
        sum += arr[h]
        h += 1
    if sum == M:
        res += 1

print(res)
```

- 슬라이딩 윈도우

[투 포인터, 슬라이딩 윈도우 참고 주소](https://velog.io/@kshired/%ED%88%AC-%ED%8F%AC%EC%9D%B8%ED%84%B0-%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%94%A9-%EC%9C%88%EB%8F%84%EC%9A%B0)

---

## 정렬

```python

arr_ = sorted(arr_)
arr_.sort()
# 리스트 정렬할때, sorted라고 하면 다시 리스트에 저장해야하고, .sort() 하면 바로 적용

# --

#  이차원 리스트의 첫번째 인덱스에 대해서 정렬해 보기
lst = [[2, 1], [3, 4], [1, 2], [1, 3], [3, 2]]
lst.sort(key=lambda x:x[0])
print(lst)
# [[1, 2], [1, 3], [2, 1], [3, 4], [3, 2]]
#  lambda를 이용했고, x:x[0] 으로 0번째 인덱스에 대해서 정렬시켰다.
# - 0번째 인덱스에 대해서 오름차순 정렬은 되었지만 동일한 0번째 인덱스를 가진 1번째 인덱스에 대해서는 정렬이 되지 않았음을 알 수 있다.

# -----------

# 이차원 배열에서 두번째 인덱스를 기준으로 정렬하기
lst = [[2, 1], [3, 4], [1, 2], [1, 3], [3, 2]]
lst.sort(key=lambda x: (x[0], -x[1]))
print(lst)
# [[1, 3], [1, 2], [2, 1], [3, 4], [3, 2]]

#  - x: ( ) 의 괄호안에 튜플 형식으로 집어넣는다. 이 때 -를 하게되면 역으로 정렬시킬 수 있다. 여기서는 먼저 0번째 인덱스에 대해서 오름차순으로 정렬한 뒤, 동일한 값의 경우 내림차순으로 재정렬된다.




```

## 정리하기

- functools.cmp_to_key

## 꿀팁까지는 아니지만 기본

```python
row = 0
col = 0
for a, b in sizes:
    if a < b:
        a, b = b, a
    row = max(row, a)
    col = max(col, b)

#---




```
