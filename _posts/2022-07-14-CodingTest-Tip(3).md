---
title: "CodingTest-Tip 2 (Python)"
layout: post
date: 2022-07-14 17:15:00 +0900
category: CodingTest
---

## 꿀팁

- mutable: list, dictionary, set

- immutable: number, string, tuple

- 개수가 몇십만개 이러면 dfs 보다 while문이 더 속도가 빠르다.

- 개수가 몇십만개 이러면 반복문 돌리면서 계속 sum(list) 하는 것 보다 sum을 변수에 저장해두고 거기에 + , - 하면서 조건 비교하는게 훨씬 빠르다.

- del이 가장 빠르고 pop()과 remove()는 비슷한 수행시간을 가지며 슬라이싱이 가장 느리다.

- 합을 비교할 경우 무조건 적으로 두개의 합을 구하지 말고 전체 합에서 빼는등 다양한 방법을 생각. 단순하게 쳐다보지 말자.

```python
from itertools import combinations as cb

cb(nums, 3)
# nums라는 list에서 조합 3개를 골라줌.
for i in cb(nums, 3):
        print(i)
        # (1, 2, 3)
        # (1, 2, 4)
        # (1, 3, 4)
        # (2, 3, 4)     이렇게 튜플형식으로 나옴.
# cb(nums,3)을 바로 이용하기는 어려움. 왜냐면 itertools이기에 for문을 이용하여 값을 뽑아내야 함.

#-------
# if else문을 줄이는 법

if num % 2:
    num = num * 3 + 1
else:
    num /= 2
# 위의 것을 아래 줄 처럼 줄일 수 있다.
num = num / 2 if num % 2 == 0 else num*3 + 1
# -----------

```

## 리스트

```python
e = [2,2,2,3]
f = [1,1,1,1]
print([a - b for a, b in zip(e,f)])
# 다음과 같이 리스트 끼리의 경우는 for문으로 해결해야함.
```

## 시간

- 큐를 이용하면 22,23,24 무조건 타임오버 생깁니다. 배열과 포인터를 이용해야해요. 어차피 정해진 두개의 큐를 빼고넣을뿐이므로 실제로 큐 그자체를 돌릴필요가 없어요. 하나의 큐 두개를 합친 하나의 배열만 만들어두고 그다음 큐1과 큐2 각각의 시작시점을 잡는 포인터에 해당하는 변수 두개만 변환해주면 훨신 더 효율적으로 가동합니다.

- 즉, 몇십만개가 case로 있다면 직접 큐를 이용하지말고 배열에서 투포인터처럼 포인터로 이용하는 것이 속도 측면에서 효율적.

  - 이때 투포인터를 이용하는데 비교해야하는 배열 두개를 합쳐야 한다. 왜냐하면 두개를 따로두면 포인터가 움직이는 것을 구현하기 어렵다.

```python

```

## for else 문

- for else문은 for문이 break 등으로 중간에 빠져나오지 않고 끝까지 실행 됐을 경우 else문이 실행되는 방식으로 진행됩니다.

- 만약 break로 빠져나오게 되면 else문은 수행되지 않습니다.

```python
for i in range(4):
    print(i, end=' ')
else:
    print("for문이 끝까지 실행")


 # 0 1 2 3 for문이 끝까지 실행

for i in range(4):
    if i == 2:
        break
    print(i, end=' ')
else:
    print("for문이 끝까지 실행")

# 0 1

```

## 소수 판별

- 루트를 이용! 이때 for문 조건에서 + 1 해주는 것 잊지말기!

```python
def isPrime(x):
    for i in range (2, int(math.sqrt(x) + 1): # 2부터 x의 제곱근까지의 숫자
    	if x % i == 0:		# 나눠떨어지는 숫자가 있으면 소수가 아님
        	return False
    return True

# 이 방법은 숫자 하나가 소수인지 판별하는 알고리즘인데 어떤 범위내에 있는 숫자들 중 소수를 확인 할때에는 시간 단축을 위해서 소수가 아닌것의 배수를 제거하는 등의 알고리즘을 이용하여 시간을 단축할 수 있다.
```

## 약수의 개수

- 주목해야할 점은 루트!

```python
# 만약 해당 약수의 개수가 홀수인지 짝수인지 판별하는 경우
if int(i**0.5)==i**0.5:
# 다음과 같이 루트가 정수라면 홀수개이다.
```

## lambda 식

- map을 활용!
- join을 활용!

```python
" ".join(map(lambda x: "".join([a.lower() if i % 2 else a.upper() for i, a in enumerate(x)]), s.split(" ")))
# 이것 처럼 map을 활용해서 lambda x를 s라는 배열에 적용한다.
# 이때 s.split(" ")은 공백으로 split한 배열이고, " ".join을 통해 다시 배열들 사이에 공백으로 이어지게 함.

```

## split

- 문제를 잘 읽기(하나이상의 공백이 있을 수 있기에 " " 와 ( )를 구분하기! )
- (" ")와 ()를 구분 할 것!

- 문자열을 split() 했을 때 숫자의 경우는 문자열이기에 대소 비교할때 int()로 치환해야함.

```python
# >>> s = " A  B "
# >>> s.split()
['A', 'B']
# >>> s.split(" ")
['', 'A', '', 'B', '']
# split에 " "를 하면 " "을 인식해서 띄운다.


m = "pizza 200"
m_ = m.split()
if int(m_[1]) > 30
# 이렇게 해야함. split한경우 int로 다시 치환
```

## reverse

- list에 0

```python
#	[1, 2, 0, 0]
p.sort(reverse=True)
# [2, 1, 0 , 0] 이 됨.
# 그렇기에
 p = p[::-1]
 # 이렇게 해야지  [0, 0, 2, 1] 제대로 뒤집어짐!

```

## 진법

```python
while n:
    tmp += str(n % base)
    n = n // base
# n이라는 10진법 수를 base 진법으로 변환(대신 거꾸로 임)

answer = int(tmp, base)
# int의 기능으로는 base 진법으로 구성된 str 형식의 tmp를 10진법으로 변환해줌
```

## 배열 수정

```python
dfs(q1[1:], q2.append(q1[0]), res+1, tot)
# 이렇게 하면 TypeError: 'NoneType' object is not iterable 에러가 난다.
# list가 mutable이기 때문에 이런 에러가 난다.
q2.append(q1[0])
dfs(q1[1:], q2, res+1, tot)
# 이렇게 하면 해결! append를 하고나서 원하는 작업을 진행!
# append한것을 새로 집어넣으려고 하면 에러가 난다 nontype이니깐!
```
