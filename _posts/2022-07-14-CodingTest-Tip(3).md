---
title: "CodingTest-Tip 2 (Python)"
categories:
  - CodingTest
feature_text: The History of the CodingTest
---

## 꿀팁

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
