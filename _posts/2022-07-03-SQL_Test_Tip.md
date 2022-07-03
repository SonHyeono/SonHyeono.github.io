---
title: "SQLTest-Tip (Oracle)"
categories:
  - CodingTest
feature_text: The History of the CodingTest
---

1. rownum을 이용할 경우 밖에 꺼내서 조건 만들기

```oracle
select *
from ( )
where rownum < 4;
```

2. LIKE의 경우 대문자 소문자 구분 잘하기 (문자열의 경우 찾고자 하는 문자열의 대소문자를 구분해야함.)

```oracle

SELECT I.ANIMAL_ID
FROM ANIMAL_INS I LEFT OUTER JOIN ANIMAL_OUTS O
ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.SEX_UPON_INTAKE LIKE '%Intact%' AND (O.SEX_UPON_OUTCOME LIKE '%Spayed%' OR O.SEX_UPON_OUTCOME LIKE '%Neutered%')

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

5. DATETIME의 날짜 형식 뽑아내는 방법 ( [참고](https://m.blog.naver.com/giriyo/221361292295) )

```oracle
--- HH24는 날짜 데이터에서 24시간을 뽑아낸다.
SELECT TO_CHAR(DATETIME, 'HH24') AS HOUR
FROM ANIMAL_OUTS
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
