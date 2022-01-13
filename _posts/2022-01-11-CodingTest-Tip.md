---

title: "CodingTest-Tip"
categories:

- CodingTest
  feature_text: |
  The History of the CodingTest

---

- [Chapter 1](#chapter1) CodingTest Tip
  - [Section 1.1](#section_1_1) 기본 Tip
  - [Section 1.2](#section_1_2) 실수 방지
  - [Section 1.2](#section_1_3) Rank를 정해야 하는 경우

# Chapter 1 <a class="anchor" id="chapter1"></a> : Coding Test Tip

## Section 1.1 <a class="anchor" id="section_1_1"></a> 기본 Tip

- 실행 속도를 위해서 for문에서 break 고려 하기.

---

## Section 1.1 <a class="anchor" id="section_1_1"></a> 실수 방지

- 묶어서 계산할 것을 혼동하지말기 (ex: x-a+b (x) , x-(a+b) (o)) 더한 것을 따로 변수로 저장하고 하던지

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

### 이런 경우 if나 case로 두지말고

```java
int[] answer = {Math.min(7 - x, 6)};
```

### 이렇게 Math를 이용해서 마지막 등수의 한계점을 정해버리면 조건을 안 따져도 가능함.
