Q.
- Students

|Column|Type|
|------|----|
|ID|Integer|
|Name|String|
|Marks|Integer|

- Grades

|Column|Type|
|--------|----|
|Grade|Integer|
|Min_Mark|Integer|
|Max_Mark|Integer|

Ketty는 Eve에게 Name, Grade, Mark를 포함한 리포트 작성하는 일을 준다. Ketty는 8보다 작은 등급을 받은 학생들의 이름을 원하지 않는다. 알고싶지 않다. 리포트는 등급 내림차순으로 정렬 한다. 

등급이 8보다 낮다면 null로 표시해라.
같은 등급끼리는 오름 차순으로 정렬하라.

GRADES 테이블의 값

    Your Output (stdout)
    1 0 9
    2 10 19
    3 20 29
    4 30 39
    5 40 49
    6 50 59
    7 60 69
    8 70 79
    9 80 89
    10 90 100


A.

정답 코드
``` SQL
SELECT
    CASE
        WHEN G.GRADE < 8 THEN 'NULL'
        ELSE S.NAME
    END,
    G.GRADE,
    S.MARKS
FROM STUDENTS S, GRADES G
WHERE S.MARKS BETWEEN G.MIN_MARK AND G.MAX_MARK
ORDER BY G.GRADE DESC, S.NAME ASC, S.MARKS ASC;
```

안되는 코드
```SQL
SELECT
    CASE
        WHEN G.GRADE < 8 THEN 'NULL'
        ELSE S.NAME
    END,
    G.GRADE,
    S.MARKS
FROM STUDENTS S, GRADES G
WHERE S.MARKS > G.MIN_MARK 
AND S.MARKS < G.MAX_MARK
ORDER BY G.GRADE DESC, S.NAME ASC, S.MARKS ASC;
```

아래 코드로 진행하다가 왜 안되지 하다가 닫힌 비교 ( = )의 차이를 간과했다는 것을 알았다. 
