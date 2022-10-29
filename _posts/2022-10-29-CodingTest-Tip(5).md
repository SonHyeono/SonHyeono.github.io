---
title: "CodingTest Tip(Ex) (Python)"
layout: post
date: 2022-10-29 12:34:00 +0900
category: CodingTest
---

```
10월 29일 농협은행 5급 IT 코딩테스트 후기

코테 3문제, sql 2문제가 나왔다.
5문제 다 풀수 있었는데 너무 아쉽다..
1번 7분만에 풀고, 2번 23분만에 풀었다. 시간도 넉넉했지만 3번문제에서 많이 날렸다.
가장 큰 이유, dict(sorted(dic.items(), key=lambda x:x[1])) 여기서 key 없이 바로 lambda를 적었다. 그러니깐 sort에서 인자가 2개라고 에러가 계속 났다.
하.. "key=lambda x:" 왜 이걸 그냥 lambda라고 했을까 진짜 정신차리자.

근데 더 문제는 사실 dict으로 접근 안해도 됐다.

예를 들어 값을 다 구하고 두개의 배열이 있다.
a = [2,4, 5]
b = [0.75, 0.3, 0.5]
실질적으로는 { 2: 0.75, 4 : 0.3, 5 : 0.5 } 가 맞는 데이터 형식인데 여기서 암튼 최대 값이 2니깐 2값을 return한다고 생각하면

e = dict(zip(a,b))
e_ = dict(sorted(e.items(),key=lambda x: -x[1]))
print(next(iter(e_)))

이렇게 접근했어햐 했다. val값 max말고 후순위로 (val 값이 동점일 때) key값의 내림차순이라고 할때에는
e_ = dict(sorted(e.items(),key=lambda x: (-x[1], x[0] ))
이렇게 하면 된다.

만약 딕셔너리말고 배열 두개를 이용해서 값을 구하는 것은
솔직히 코드도 길어지고 복잡하다. 딕셔너리를 이용하자.

```
