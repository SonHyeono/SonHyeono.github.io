---
title: "SQLTest-Tip (Oracle)"
layout: post
date: 2022-07-03 10:24:00 +0900
category: CodingTest
---

꿀팁.

- "년, 월, 성별 별로 상품을 구매한 회원수를 집계 ~ " 이런 문제의 경우 회원수 이기 때문에 중복을 제거해야한다. 즉 1월에 두번 구매한 회원의 경우 한명으로 쳐야하기때문에 DISTINCT로 중복을 제거 해야함!

1. rownum을 이용할 경우 밖에 꺼내서 조건 만들기

```oracle
select *
from ( )
where rownum < 4;
```

2. LIKE의 경우 대문자 소문자 구분 잘하기 (문자열의 경우 찾고자 하는 문자열의 대소문자를 구분해야함.)

```oracle

SELECT ANIMAL_ID, ANIMAL_TYPE, NAME
FROM ANIMAL_OUTS
WHERE SEX_UPON_OUTCOME LIKE 'S%' OR SEX_UPON_OUTCOME LIKE 'N%'
--- LIKE 여러개 쓰는 법
```

3. subQuery의 경우 안에서 ORDER BY하지말자

```oracle
--- 이러면 에러난다. subQuery안에서는 정렬 X
SELECT *
FROM (
    SELECT TO_CHAR(DATETIME, 'HH24') AS HOUR
    FROM ANIMAL_OUTS
    ORDER BY HOUR ASC;
    )
```

4. BETWEEN은 앞뒤 포함.

```oracle
--- 9부터 19까지 포함.
BETWEEN 9 AND 19
```

5. DATETIME

- DATETIME의 날짜 형식 뽑아내는 방법 ( [참고](https://m.blog.naver.com/giriyo/221361292295) )

```oracle
--- HH24는 날짜 데이터에서 24시간을 뽑아낸다.
SELECT TO_CHAR(DATETIME, 'HH24') AS HOUR
FROM ANIMAL_OUTS


-------
--- 날짜의 경우 오늘에 가까울 수록 크기가 큼. 그래서 대소 비교할 때 과거일수록 값이 작음.

---

SELECT TO_CHAR(SALES_DATE, 'YYYY') AS Month
-- 2022가 나오고
SELECT TO_CHAR(SALES_DATE, 'YY') AS Month
-- 22가 나옴.
-- MM도 마찬가지 -> 월이 2자로 나옴.
```

6. 계층형 쿼리

- 계층형 쿼리란?

  계층형 쿼리는 테이블에 저장된 데이터를 계층형 구조로 반환하는 쿼리를 말합니다.
  START WITH 조건으로 최상위 노드를 설정하고,
  CONNECT BY 절로 계층형 구조에서의 연결조건을 설정할 수 있습니다.

```oracle


```

7. as alias

- as alias는 하지말자. left join 할때 as 쓰니깐 에러남.

```oracle
--- 에러
LEFT JOIN ANIMAL_OUTS AS O

--- 오류 없음.
LEFT JOIN ANIMAL_OUTS O

```

8. COUNT

```oracle
SELECT ~
FROM ~
GROUP BY ~
HAVING COUNT(*) = (
  SELECT ~
  FROM ~
  GROUP BY ~
) ORDER BY ~;
```

- 이런식으로 HAVING COUNT(\*) = () 으로 이용 가능

9. IN

```oracle
WHERE ANIMAL_ID NOT IN (
)
WHERE ANIMAL_ID IN (
)

--- IN으로 여러 칼럼 비교

WHERE (CATEGORY, PRICE) IN (
    SELECT CATEGORY, MAX(PRICE)
    FROM FOOD_PRODUCT
    GROUP BY CATEGORY
    HAVING CATEGORY IN ('과자', '국', '김치', '식용유')
)
```

10. GROUP BY

- GROUP BY 에서는 group by 한 칼럼외에는 sum, max, count, avg 등과 같은 집계함수를 이용해야지 다른 칼럼 값을 가져올 수 있음.

```oracle
--group 함수 문장 속 조건문은 having절로 적용
-- 실행 순서 : from -> group by -> having -> select
select deptno, count(*), count(comm), avg(sal)
from emp
group by deptno
having avg(sal) >= 2000;


```

11. DISTINCT

```oracle

SELECT DISTINCT depart_no , family_name FROM emp;

```

12. NULL

- NULL은 NULL로 해야함. ( 'NULL' x )

```oracle
WHERE GENDER IS NOT NULL
-- NULL인지 확인 할때 IS NULL / IS NOT NULL
```
