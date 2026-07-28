---
layout: wiki
title: 4.5 TOP N 쿼리
wiki_name: sql
parent: sql/04.SQL-활용
order: 5
---

## *4.5 *Top N 쿼리**

Top N 쿼리란 **상위 N개의 데이터를 조회**하기 위한 SQL 기법이다.

대표적으로 **빌보드 Hot 100**, **매출 상위 10명**, **급여 상위 5명**과 같은 데이터를 조회할 때 사용한다.

Top N 쿼리는 일반적으로 **ROWNUM** 또는 **순위 함수(RANK, DENSE_RANK, ROW_NUMBER)**를 이용하여 작성한다.

---

### **1. ROWNUM 함수**

`ROWNUM`은 Oracle에서 제공하는 의사 컬럼(Pseudo Column)으로, **조회되는 순서대로 행에 번호를 부여**한다.

`ROW_NUMBER()`와 달리 **정렬 결과가 아니라 현재 조회되는 순서**를 기준으로 번호가 매겨진다.

#### 특징

- 조회되는 순서대로 1부터 번호를 부여한다.
- 테이블에 저장된 순서를 기준으로 동작한다.
- 중간 번호를 건너뛰어 조회할 수 없다.
- `ORDER BY`보다 먼저 적용되므로 함께 사용할 때 주의해야 한다.

---

#### 예제 1. 상위 5행 조회

```sql
SELECT ROWNUM,
       EMPNO,
       ENAME,
       SAL
FROM EMP
WHERE ROWNUM <= 5;
```

#### 실행 결과

|ROWNUM|EMPNO|ENAME|SAL|
|---:|---:|---|---:|
|1|7369|SMITH|800|
|2|7499|ALLEN|1600|
|3|7521|WARD|1250|
|4|7566|JONES|2850|
|5|7654|MARTIN|1250|

---

#### 예제 2. 등호 비교

```sql
SELECT ROWNUM,
       ENAME,
       SAL
FROM EMP
WHERE ROWNUM = 5;
```

**결과가 출력되지 않는다.**

**이유**

- ROWNUM은 첫 번째 행부터 순차적으로 번호를 부여한다.
- 첫 번째 행의 ROWNUM은 1이며, `ROWNUM = 5` 조건을 만족하지 못한다.
- 조건이 거짓이 되는 순간 더 이상 다음 행을 조회하지 않으므로 결과가 없다.

> **ROWNUM은 `=`, `>`, `>=` 조건으로 사용할 수 없으며, `<=` 형태로 사용하는 것이 일반적이다.**

---

#### 예제 3. ORDER BY와 함께 사용

```sql
SELECT ROWNUM,
       EMPNO,
       ENAME,
       SAL
FROM EMP
WHERE ROWNUM <= 5
ORDER BY SAL;
```

#### 실행 결과

|ROWNUM|EMPNO|ENAME|SAL|
|---:|---:|---|---:|
|1|7369|SMITH|800|
|3|7521|WARD|1250|
|5|7654|MARTIN|1250|
|2|7499|ALLEN|1600|
|4|7566|JONES|2850|

번호가 **1, 3, 5, 2, 4**처럼 뒤섞여 보이는 이유는 **ROWNUM이 먼저 부여된 후 `ORDER BY`가 수행되기 때문**이다.

따라서 **정렬 후 순위를 부여하려면 `ROW_NUMBER()`를 사용하는 것이 좋다.**

---

### **2. 윈도우 함수와 순위 함수**

윈도우 함수를 이용하면 **정렬이 완료된 결과에 순위를 부여**할 수 있다.

---

#### 예제 1. RANK()

```sql
SELECT *
FROM (
    SELECT RANK() OVER(ORDER BY SAL DESC) AS RANK,
           EMPNO,
           ENAME,
           SAL
    FROM EMP
)
WHERE RANK <= 5;
```

- 급여(`SAL`)를 내림차순으로 정렬한다.
- `RANK()`로 순위를 부여한다.
- **상위 5순위까지** 조회한다.
- 공동 순위가 있으면 다음 순위는 건너뛴다.

---

#### 예제 2. DENSE_RANK()

```sql
SELECT *
FROM (
    SELECT DENSE_RANK() OVER(ORDER BY SAL DESC) AS D_RANK,
           EMPNO,
           ENAME,
           SAL
    FROM EMP
)
WHERE D_RANK <= 5;
```

- `RANK()`와 동일한 방식이다.
- 공동 순위가 있어도 다음 순위를 건너뛰지 않는다.
- 따라서 **상위 5순위**를 조회하면 **5명을 초과하여 출력될 수도 있다.**

---

#### 예제 3. ROW_NUMBER()

```sql
SELECT *
FROM (
    SELECT ROW_NUMBER() OVER(ORDER BY SAL DESC) AS R_NUM,
           EMPNO,
           ENAME,
           SAL
    FROM EMP
)
WHERE R_NUM <= 5;
```

- 급여 기준으로 내림차순 정렬한다.
- `ROW_NUMBER()`로 순번을 부여한다.
- 공동 순위가 있어도 **각 행마다 고유한 번호**를 부여한다.
- **항상 정확히 상위 N명만 조회**된다.

---

### **정리**

|방법|특징|추천 상황|
|---|---|---|
|`ROWNUM`|조회 순서대로 번호 부여|단순히 앞의 N행 조회|
|`RANK()`|공동 순위 허용, 다음 순위 건너뜀|공동 순위를 인정하는 순위|
|`DENSE_RANK()`|공동 순위 허용, 다음 순위 유지|공동 순위를 인정하면서 순위를 연속적으로 표시|
|`ROW_NUMBER()`|모든 행에 고유 번호 부여|정확히 Top N명을 조회할 때 가장 많이 사용|
