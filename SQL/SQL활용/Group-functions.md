---
layout: wiki
title: 4.3 그룹함수
wiki_name: sql
parent: sql/04.SQL-활용
order: 3
---

## **4.3 그룹 함수(Group Function)**

그룹 함수는 **GROUP BY절로 생성된 각 그룹을 대상으로 연산을 수행하는 함수**이다.

대표적인 집계 함수(`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) 외에도 **ROLLUP**, **CUBE**, **GROUPING SETS**, **GROUPING** 등이 있다.

---

### **1. ROLLUP**

`ROLLUP`은 **GROUP BY에 지정한 컬럼을 기준으로 계층적인 그룹핑을 수행하는 함수**이다.

주로 **소계(Subtotal)** 와 **총계(Grand Total)** 를 구할 때 사용한다.

예를 들어,

```sql
GROUP BY ROLLUP(날짜, 이름)
```

은 다음 순서로 그룹핑을 수행한다.

```text
(날짜, 이름)
    ↓
(날짜)
    ↓
(전체)
```

#### **예제 ①**

```sql
SELECT CYL, COUNT(*)
FROM MTCARS
GROUP BY ROLLUP(CYL)
ORDER BY CYL;
```

실린더 수(CYL)별 개수와 총계를 조회한다.

**실행 결과**

| CYL  | COUNT(*) |
| ---- | -------: |
| 4    |       11 |
| 6    |        7 |
| 8    |       14 |
| NULL |       32 |

---

#### **예제 ②**

```sql
SELECT CYL, GEAR, COUNT(*)
FROM MTCARS
GROUP BY ROLLUP(CYL, GEAR)
ORDER BY CYL, GEAR;
```

실린더 수와 기어 수별 개수, 실린더별 소계, 전체 총계를 조회한다.

**실행 결과**

| CYL  | GEAR | COUNT(*) |
| ---- | ---: | -------: |
| 4    |    3 |        1 |
| 4    |    4 |        8 |
| 4    |    5 |        2 |
| 4    | NULL |       11 |
| 6    |    3 |        2 |
| 6    |    4 |        4 |
| 6    |    5 |        1 |
| 6    | NULL |        7 |
| 8    |    3 |       12 |
| 8    |    5 |        2 |
| 8    | NULL |       14 |
| NULL | NULL |       32 |

---

### **2. CUBE**

`CUBE`는 **가능한 모든 그룹 조합에 대한 소계와 총계**를 생성하는 함수이다.

예를 들어,

```sql
GROUP BY CUBE(날짜, 이름)
```

은 다음 순서의 그룹을 생성한다.

```text
(날짜, 이름)
(날짜)
(이름)
(전체)
```

즉, ROLLUP보다 더 많은 소계를 생성한다.

#### **예제**

```sql
SELECT CYL, GEAR, COUNT(*)
FROM MTCARS
GROUP BY CUBE(CYL, GEAR)
ORDER BY CYL, GEAR;
```

실린더별, 기어별, 실린더+기어별, 전체 총계를 모두 조회한다.

**실행 결과**

| CYL  | GEAR | COUNT(*) |
| ---- | ---: | -------: |
| 4    |    3 |        1 |
| 4    |    4 |        8 |
| 4    |    5 |        2 |
| 4    | NULL |       11 |
| 6    |    3 |        2 |
| 6    |    4 |        4 |
| 6    |    5 |        1 |
| 6    | NULL |        7 |
| 8    |    3 |       12 |
| 8    |    5 |        2 |
| 8    | NULL |       14 |
| NULL |    3 |       15 |
| NULL |    4 |       12 |
| NULL |    5 |        5 |
| NULL | NULL |       32 |

---

### **3. GROUPING SETS**

`GROUPING SETS`는 **원하는 그룹만 선택하여 그룹핑**하는 함수이다.

ROLLUP이나 CUBE처럼 모든 소계를 생성하지 않고, **지정한 그룹에 대해서만 집계를 수행**한다.

또한 `GROUPING SETS`의 인자로 `ROLLUP`이나 `CUBE`를 사용할 수도 있다.

#### **예제**

```sql 
SELECT CYL, GEAR, COUNT(*)
FROM MTCARS
GROUP BY GROUPING SETS (CYL, GEAR)
ORDER BY CYL, GEAR;
```

실린더별 집계와 기어별 집계만 조회한다.

**실행 결과**

| CYL  | GEAR | COUNT(*) |
| ---- | ---: | -------: |
| 4    | NULL |       11 |
| 6    | NULL |        7 |
| 8    | NULL |       14 |
| NULL |    3 |       15 |
| NULL |    4 |       12 |
| NULL |    5 |        5 |

> `GROUPING SETS(CYL, GEAR)`는 **(CYL, GEAR)** 그룹을 만드는 것이 아니라, **(CYL)** 과 **(GEAR)** 를 각각 별도로 그룹핑한다.

---

### **4. GROUPING**

`GROUPING` 함수는 **ROLLUP**, **CUBE**, **GROUPING SETS**와 함께 사용된다.

소계 또는 총계로 생성된 행인지 여부를 구분할 수 있다.

| 반환값 | 의미         |
| --- | ---------- |
| 0   | 일반 데이터 행   |
| 1   | 소계 또는 총계 행 |

이를 이용하면 `CASE`문으로 **"소계"**, **"총계"** 와 같은 문구를 출력할 수 있다.

#### **예제**

```sql 
SELECT
    CASE GROUPING(CYL)
        WHEN 1 THEN '총계'
        ELSE TO_CHAR(CYL)
    END AS CYL,
    COUNT(*)
FROM MTCARS
GROUP BY ROLLUP(CYL)
ORDER BY CYL;
```

**실행 결과**

| CYL | COUNT(*) |
| --- | -------: |
| 4   |       11 |
| 6   |        7 |
| 8   |       14 |
| 총계  |       32 |

---

### **정리**

| 함수            | 설명                    |
| ------------- | --------------------- |
| ROLLUP        | 계층적으로 소계와 총계를 생성      |
| CUBE          | 가능한 모든 조합의 소계와 총계를 생성 |
| GROUPING SETS | 지정한 그룹에 대해서만 집계 수행    |
| GROUPING      | 소계·총계 여부를 0 또는 1로 반환  |

> **SQLD 핵심**
>
> * `ROLLUP` : **계층적 소계 + 총계**
> * `CUBE` : **모든 조합의 소계 + 총계**
> * `GROUPING SETS` : **원하는 그룹만 집계**
> * `GROUPING` : **소계/총계 행 판별**
