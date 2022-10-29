---
title: "CodingTest-Algorithm (Python)"
layout: post
date: 2022-09-23 23:56:00 +0900
category: CodingTest
---

## 알고리즘

1. 합의 경우의 수 (DP)

```python
def n_list(N):
    dp = [0] * (N+1)
    for i in range(1, N):
        for j in range(N, i, -1):
            for k in range(j-i,1,-i):
                dp[j] += dp[k]
        for j in range(i+1, N+1):
            dp[j] += 1
    return dp

# n이 10일 경우
# [0, 0, 1, 2, 4, 6, 10, 14, 21, 29, 41]
# 다음과 같이 나타남. 즉 합으로 10구성하는 경우의 수는 41개다.
# 합이 5인 경우의 수는 1 + 1 + 1 + 1 + 1 , 1 + 1 + 1 + 2 , 1 + 1 + 3 ... 이렇게 총 6가지 이다.
```

2. While

- 경우의 수와 주어진 숫자가 엄청나면 While문으로 접근!

```python
# 조건에서 단순히 While(True): 으로 하지말고 조건을 걸어두면 코드의 길이가 줄어든다. break말고 while()안에 조건을 걸어두자!
```

3. 배열과 문자열

- 문자열에서 replace보다 문자열 슬라이싱이 훨씬 빠르다. ( str = str[:x] + str[x+1:])

- 대용량의 list가 테스트 케이스로 주어질 경우 Stack을 많이 참고하자. 즉 새로운 배열을 이용해서 pop등을 이용. 기존 배열을 잘라서 움직이면 시간이 오래걸린다.

```python
str_list = ['There', 'is', 4, "items"]
result = ' '.join(str(s) for s in str_list)
# There is 4 items 라고 나온다. join을 이용! ( 배열을 그대로 쓰는 것이 아닌 for문을 통해 해결 )


# ---

def solution(ingredient):
    s = []
    cnt = 0
    for i in ingredient:
        s.append(i)
        if s[-4:] == [1, 2, 3, 1]:
            cnt += 1
            for i in range(4):
                s.pop()
    return cnt
# 이 경우처럼 새로운 배열을 이용해서 append해주고 조건에 맞다면 pop해서 해결하는 등으로! 생각. 그저 find, replace, 문자열 슬라이싱에 의존하지 말고
# stack개념처럼 새로운 배열을 이용하면 시간이 훨씬 빠름.

```

4. 딕셔너리

- (sort를 통해 정렬된 ) 딕셔너리의 첫번째 인자 값을 가져와야할 경우 next(iter())를 이용해서 접근하자. 왜냐하면 딕셔너리를 리스트로 변환 후에 index로 접근하는 것은 딕셔너리가 엄청 큰 경우 속도가 느려서!

```python
e_ = {2: 0.5, 3 :0.7}
print(next(iter(e_)))
# 딕셔너리의 첫번째 인자를 가져오고 싶으면 next(iter())를 하면 된다. 딕셔너리를 리스트로 변환하고 index로 접근해도 되지만 딕셔너리가 엄청 클경우 next(iter())이 훨씬 빠르다!

```
