---
title: "CodingTest-Tip (Java)"
categories:
  - CodingTest
feature_text: |
  The History of the CodingTest
---

- [Chapter 1](#chapter1) CodingTest Tip
  - [Section 1.1](#section_1_1) 기본 Tip
  - [Section 1.2](#section_1_2) 실수 방지
  - [Section 1.3](#section_1_3) Rank를 정해야 하는 경우
  - [Section 1.4](#section_1_4) 이진법
  - [Section 1.5](#section_1_5) Long과 int
  - [Section 1.6](#section_1_6) 배열
  - [Section 1.7](#section_1_7) java의 람다식 표현
  - [Section 1.8](#section_1_8) 백트래킹

# Chapter 1 <a class="anchor" id="chapter1"></a> : Coding Test Tip

## Section 1.1 <a class="anchor" id="section_1_1"></a> 기본 Tip

- 실행 속도를 위해서 for문에서 break 고려 하기.

- 프로그래머스에서 import java.util.*; 으로 하게 되면 Entry를 사용하는 경우 문제가 발생함으로 import java.util.Map.Entry; 으로 하자. 정말 시간 없을때만 *로 하고 웬만하면 util 뒤에 적어주기.

- Math.pow(x, 얼마나제곱할지) , Math.sqrt(x) : 제곱근

- Math.round() : 반올림 , Math.ceil() : 올림 , Math.floor() : 내림 함수

- Math.max 이용할 때 3개를 비교해야하는 경우 Math.max(arr[0], Math.max(arr[1], arr[2])) 이렇게 이용.

- `이차원 배열에서 대각선인지 체크하려면 기울기 양인 대각선의 경우는 (행+열)이 같은 것들이고, 기울기가 음인 대각선의 경우는 (행-열)이 같은 것 들이다.`

- 형 변환
  | 처음 | 결과 | 문법|
  |----|----|----|
  |String|Int|Integer.parseInt(str) or Integer.valueOf(str) `두개의 차이는 기본 int 가 필요하면 parseInt() , Integer 래퍼 객체가 필요하면 valueOf() 를 사용하면 된다`|

- HashSet과 List의 관계: (중복의 유무) List의 경우는 순서가 중요하지만 HashSet의 경우는 순서를 보장할 필요가 없기에 검색시간이 매우 짧다. 그렇기에 동작의 차이가 없다면 HashSet을 쓰자!

- str.substring(a,b)를 하면 index a부터 b-1까지이다. ( python에서 list [포함:미포함] 이랑 마찬가지 ) `str.substring(0, 0)이면 아무것도 안 나온다.`

---

## Section 1.1 <a class="anchor" id="section_1_1"></a> 실수 방지

- 묶어서 계산할 것을 혼동하지말기 (ex: x-a+b (x) , x-(a+b) (o)) 더한 것을 따로 변수로 저장하고 하던지

- String 값 비교할 때 equals (== 은 주소 값)

---

## Section 1.3 <a class="anchor" id="section_1_3"></a> Rank를 정해야 하는 경우

- Ex) 로또의 경우(실제 로또랑 차이가 있음)
- [프로그래머스 로또의 최고 순위와 최저 순위](https://programmers.co.kr/learn/courses/30/lessons/77484)

| 6개의 숫자 중 일치한 개수 | 등수 |
| ------------------------- | ---- |
| 6개                       | 1등  |
| 5개                       | 2등  |
| 4개                       | 3등  |
| 3개                       | 4등  |
| 2개                       | 5등  |
| 1개 혹은 0개              | 6등  |

##### 이런 경우 if나 case로 두지말고

```java
int[] answer = {Math.min(7 - x, 6)};
```

##### 이렇게 Math를 이용해서 마지막 등수의 한계점을 정해버리면 조건을 안 따져도 가능함.

---

## Section 1.4 <a class="anchor" id="section_1_4"></a> 이진법

```java
Integer.toBinaryString(9 | 30);
```

이뜻은 십진수 두개가 들어왔을 때 그것의 이진수의 각 자리수에서 둘중에 하나라도 1이면 1이다.
즉, 01001(2) 와 11110(2)를 하면 11111(2)가 된다.

```java
Integer.toBinaryString(9 & 30);
```

이렇게 하면 둘 다 1이여야지 1이 된다.
즉, 01001(2) 와 11110(2)를 하면 01000(2)가 된다.

- Plus

`System.out.println(9|30) 을 하면 31이 나온다. 즉 알아서 이진법으로 위처럼 둘중에 하나라도 1이면 1로 되어진 최종 이진수가 다시 십진수로 나온다.`

---

## Section 1.5 <a class="anchor" id="section_1_5"></a> Long과 int

타입이 Long 으로 알고리즘 문제가 나오면 주의해야한다.
만약 int로 long을 받게 되면 문제가 생길 가능성이 많다.
특히 long으로 파라미터가 주어지고
그것을 long에 담아서 해결해야되면

```java
solution(int x, int n) {
         long[] answer = new long[n];
         long y = (long)x;

```

이런식으로 long으로 받거나, 파라미터를 int x에서 long x로 바꾸기

---

## Section 1.6 <a class="anchor" id="section_1_6"></a> 배열

- 등차수열을 배열에 순서대로 저장할 때,

```java
        int[] answer = new int[n];
        answer[0] = x;

        for (int i = 1; i < n; i++) {
            answer[i] = answer[i - 1] + x;
        }

```

- 배열 값 채우기

```java
Arrays.fill(array, 0);
// array 배열을 0으로 값을 채움

Arrays.fill(array, 2, 5, 0); // Replace elements from index 2 to index 4 by 0
// array 배열에서 index 2번째 부터 4번째까지를 0으로 채움.
```

---

## Section 1.7 <a class="anchor" id="section_1_7"></a> java의 람다식 표현

```
list.stream().mapToInt(i->i.intValue()).toArray();
// 1. list라는 ArrayList 안의 값들로 배열의 형태로 만들기.

```

---

## Section 1.8 <a class="anchor" id="section_1_8"></a> 백트래킹

백트래킹 : 현재 상태에서 가능한 모든 후보군을 따라 들어가며 탐색하는 알고리즘

좋은 문제:

- [백준 15649](https://www.acmicpc.net/problem/15649) 
- [프로그래머스 소수찾기](https://programmers.co.kr/learn/courses/30/lessons/42839)
- [백준 백트래킹 문제들](https://www.acmicpc.net/step/34)

---

## Section 1.8 <a class="anchor" id="section_1_8"></a> 소수

```java
public boolean isPrime(int n){
        if(n==0 || n==1) return false;
        for(int i=3; i<=(int)Math.sqrt(n); i+=2){
            if(n%i==0) return false;
        }
        return true;
    }
```

- isPrime 구현방식은 에라토스테네스의 체를 응용한 것 이고 N 까지의 소수목록을 제곱근 및 곱이 가능한 수를 제외하는 방식으로로 구하는데, 여기서는 나눗셈으로 바꾸어 소수의 목록이 아닌 소수여부만 체크한것입니다. 짝수부분을 제외하고 이를 증감식(i+=2)에도 적용. ( 이때 주의해야 할 것은 2도 소수이기에 isPrime을 쓰기전에 2를 처리해야한다.)

`소수는 n의 배수가 아니어야 하고 입력받은 수보다 작은 수 들로 나누어서 떨어지면 소수가 아니다. 그러나 모두 나누어볼 필요없이, 루트 n 까지만 나누어서 떨어지면 소수가 아니다.`



