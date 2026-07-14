---
layout: wiki
title: 3.7 join
wiki_name: sql
parent: sql/03.SQL-기본
order: 7
---


## **3.7 JOIN**
---
### **1. JOIN의 개념**

JOIN은 **두 개 이상의 테이블을 하나의 결과로 병합**하는 연산이다.

일반적으로 두 테이블 간 **기본키(PK)** 와 **외래키(FK)** 의 관계를 이용하여 조인이 이루어지지만, PK/FK 관계가 아니더라도 논리적으로 연관된 값이 있다면 조인이 가능하다.

> JOIN은 많은 CPU 연산이 필요한 작업이다.
> 조회 성능을 높이기 위해서는 불필요한 JOIN을 줄이는 것이 중요하며, 이를 위해 **반정규화(Denormalization)** 를 적용하기도 한다.

---

### **2. EQUI JOIN**

EQUI JOIN은 **등호(`=`)를 조건으로 사용하는 JOIN**이다.

WHERE절 또는 ON절에서 두 테이블의 값이 정확히 일치하는 경우에 수행된다.

---

### **3. Non EQUI JOIN**

Non EQUI JOIN은 **등호(`=`)가 아닌 비교 연산자**를 이용하는 JOIN이다.

주로 `BETWEEN`, `>`, `>=`, `<`, `<=` 등을 사용하여 범위 조건으로 조인을 수행한다.

> 설계에 따라 실행이 불가능한 경우도 있으므로 주의해야 한다.

---

### **4. 3개 이상의 TABLE JOIN**

N개의 테이블을 JOIN하면 **N-1개의 JOIN**이 발생한다.

예를 들어,

* 2개 테이블 → JOIN 1회
* 3개 테이블 → JOIN 2회
* 4개 테이블 → JOIN 3회

3개 이상의 테이블을 JOIN할 경우 연산량이 크게 증가하므로 조회 성능이 저하될 수 있다.

이러한 경우 **반정규화**를 통해 JOIN 대상 테이블 수를 줄여 성능을 최적화할 수 있다.

---

### **5. OUTER JOIN의 개념**

앞에서 살펴본 EQUI JOIN과 Non EQUI JOIN은 **조건을 만족하는 행만 조회**하는 JOIN이며, 이를 **INNER JOIN**이라고 한다.

집합의 개념으로 보면 **교집합(∩)** 에 해당한다.

반면 **OUTER JOIN**은 조건에 맞지 않는 행도 함께 조회하는 JOIN이다.

집합의 개념으로 보면 **합집합(∪)** 에 가깝다.

OUTER JOIN의 종류는 다음과 같다.

* LEFT OUTER JOIN
* RIGHT OUTER JOIN
* FULL OUTER JOIN

#### **Oracle (+) 문법**

Oracle에서는 WHERE절에서 `(+)`를 사용하여 OUTER JOIN을 표현할 수 있다.

```sql
SELECT A.DNAME, B.ENAME
FROM DEPT A, EMP B
WHERE A.DEPTNO = B.DEPTNO(+);
```

`(+)`가 없는 테이블이 기준 테이블이 된다.

위 SQL은 다음과 같다.

```sql
A LEFT OUTER JOIN B
```

---

### **6. ANSI 표준 JOIN**

ANSI SQL에서는 WHERE절 대신 **ON절**을 사용하여 JOIN 조건을 작성한다.

#### **기본 문법**

```sql
FROM 테이블1
JOIN 테이블2
ON 조건식;
```

| 구성   | 설명                                                           |
| ---- | ------------------------------------------------------------ |
| 테이블1 | 왼쪽 테이블                                                       |
| 테이블2 | 오른쪽 테이블                                                      |
| JOIN | INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER, NATURAL, CROSS 등 |
| ON   | JOIN 조건                                                      |

두 테이블을 JOIN할 때 대응되는 값이 없는 경우 해당 컬럼은 **NULL**로 출력된다.

---

### **7. INNER JOIN**

INNER JOIN은 **조건을 만족하는 행만 조회**하는 JOIN이다.

집합의 개념으로 보면 **교집합**이다.

#### **예제**

```sql
SELECT
    A1.ACTOR_NO AS ACT_NO1,
    A2.ACTOR_NO AS ACT_NO2,
    A2.MOVIE_NO,
    A1.NAME,
    A1.GENDER
FROM ACTOR A1
INNER JOIN APPR A2
ON A1.ACTOR_NO = A2.ACTOR_NO;
```

#### **해설**

1. ACTOR와 APPR 테이블을 INNER JOIN한다.
2. ACTOR_NO가 같은 행만 조회한다.

---

### **8. OUTER JOIN**

OUTER JOIN은 **조건을 만족하지 않는 행도 함께 조회**하는 JOIN이다.

#### **8.1 LEFT OUTER JOIN**

왼쪽 테이블의 **모든 행**을 조회한다.

```sql
SELECT
    A1.ACTOR_NO AS ACT_NO1,
    A2.ACTOR_NO AS ACT_NO2,
    A2.MOVIE_NO,
    A1.NAME,
    A1.GENDER
FROM ACTOR A1
LEFT OUTER JOIN APPR A2
ON A1.ACTOR_NO = A2.ACTOR_NO;
```

**해설**

1. ACTOR의 모든 행을 출력한다.
2. 일치하는 APPR 데이터가 없으면 NULL을 출력한다.

---

#### **8.2 RIGHT OUTER JOIN**

오른쪽 테이블의 **모든 행**을 조회한다.

```sql
SELECT
    A1.ACTOR_NO AS ACT_NO1,
    A2.ACTOR_NO AS ACT_NO2,
    A2.MOVIE_NO,
    A1.NAME,
    A1.GENDER
FROM ACTOR A1
RIGHT OUTER JOIN APPR A2
ON A1.ACTOR_NO = A2.ACTOR_NO;
```

**해설**

1. APPR의 모든 행을 출력한다.
2. 일치하는 ACTOR 데이터가 없으면 NULL을 출력한다.

---

#### **8.3 FULL OUTER JOIN**

양쪽 테이블의 **모든 행**을 조회한다.

```sql
SELECT
    A1.ACTOR_NO AS ACT_NO1,
    A2.ACTOR_NO AS ACT_NO2,
    A2.MOVIE_NO,
    A1.NAME,
    A1.GENDER
FROM ACTOR A1
FULL OUTER JOIN APPR A2
ON A1.ACTOR_NO = A2.ACTOR_NO;
```

**해설**

1. ACTOR와 APPR의 모든 행을 출력한다.
2. 대응되는 값이 없으면 NULL을 출력한다.

---

### **9. NATURAL JOIN**

NATURAL JOIN은 **이름이 같은 컬럼을 자동으로 찾아 조인**하는 방식이다.

#### **예제**

```sql
SELECT *
FROM ACTOR
NATURAL JOIN APPR;
```

#### **해설**

1. 이름이 같은 컬럼을 자동으로 찾는다.
2. 동일한 값을 가진 행만 JOIN한다.

> SQL Server에서는 NATURAL JOIN을 지원하지 않는다.

> NATURAL JOIN은 조인 조건을 내포하고 있으므로 `ON`절을 사용할 수 없다.

Oracle에서는 `USING`절을 사용하여 원하는 컬럼만 조인 조건으로 지정할 수 있다.

```sql
SELECT *
FROM ACTOR
JOIN APPR USING (ACTOR_NO);
```

---

### **10. CROSS JOIN**

CROSS JOIN은 **두 테이블의 모든 행을 서로 조합**하는 JOIN이다.

이를 **카테시안 곱(Cartesian Product)** 이라고 한다.

왼쪽 테이블이 M행, 오른쪽 테이블이 N행이라면 결과는 **M × N행**이 된다.

> CROSS JOIN은 별도의 JOIN 조건을 사용하지 않는다.

#### **예제 ① (비표준 문법)**

```sql
SELECT S1.NAME, C1.NAME
FROM STUDENT S1, CLUB C1;
```

WHERE절이 없으면 CROSS JOIN이 수행된다.

#### **예제 ② (ANSI SQL)**

```sql
SELECT S1.NAME, C1.NAME
FROM STUDENT S1
CROSS JOIN CLUB C1;
```

---

### **11. JOIN 종류 비교**

| JOIN             | 설명                   |
| ---------------- | -------------------- |
| INNER JOIN       | 조건이 일치하는 행만 조회       |
| LEFT OUTER JOIN  | 왼쪽 테이블 전체 조회         |
| RIGHT OUTER JOIN | 오른쪽 테이블 전체 조회        |
| FULL OUTER JOIN  | 양쪽 테이블 전체 조회         |
| NATURAL JOIN     | 같은 이름의 컬럼을 자동으로 JOIN |
| CROSS JOIN       | 모든 행을 조합(M × N)      |

> SQLD에서는 **INNER JOIN과 OUTER JOIN의 차이**, **ANSI JOIN 문법**, **NATURAL JOIN**, **USING**, **CROSS JOIN**, **Oracle (+) 문법**이 자주 출제된다.
