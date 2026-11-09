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

### **0. 예제 테이블 (MTCARS)**

이후 모든 예제는 아래 `MTCARS` 테이블(32행)을 기준으로 한다. (실습용 자동차 데이터에서 예제에 쓰는 컬럼만 발췌했다.)

| NAME                | CYL | GEAR |
| ------------------- | --: | ---: |
| Mazda RX4           |   6 |    4 |
| Mazda RX4 Wag       |   6 |    4 |
| Datsun 710          |   4 |    4 |
| Hornet 4 Drive      |   6 |    3 |
| Hornet Sportabout   |   8 |    3 |
| Valiant             |   6 |    3 |
| Duster 360          |   8 |    3 |
| Merc 240D           |   4 |    4 |
| Merc 230            |   4 |    4 |
| Merc 280            |   6 |    4 |
| Merc 280C           |   6 |    4 |
| Merc 450SE          |   8 |    3 |
| Merc 450SL          |   8 |    3 |
| Merc 450SLC         |   8 |    3 |
| Cadillac Fleetwood  |   8 |    3 |
| Lincoln Continental |   8 |    3 |
| Chrysler Imperial   |   8 |    3 |
| Fiat 128            |   4 |    4 |
| Honda Civic         |   4 |    4 |
| Toyota Corolla      |   4 |    4 |
| Toyota Corona       |   4 |    3 |
| Dodge Challenger    |   8 |    3 |
| AMC Javelin         |   8 |    3 |
| Camaro Z28          |   8 |    3 |
| Pontiac Firebird    |   8 |    3 |
| Fiat X1-9           |   4 |    4 |
| Porsche 914-2       |   4 |    5 |
| Lotus Europa        |   4 |    5 |
| Ford Pantera L      |   8 |    5 |
| Ferrari Dino        |   6 |    5 |
| Maserati Bora       |   8 |    5 |
| Volvo 142E          |   4 |    4 |

**CYL × GEAR 별 행 수 (미리 집계한 표)**

| CYL \ GEAR |  3 |  4 |  5 | 합계 |
| ---------- | -: | -: | -: | -: |
| 4          |  1 |  8 |  2 | 11 |
| 6          |  2 |  4 |  1 |  7 |
| 8          | 12 |  0 |  2 | 14 |
| **합계**     | 15 | 12 |  5 | 32 |

* 표의 안쪽 칸은 `(CYL, GEAR)` 조합별 개수, 오른쪽 합계는 `(CYL)`별 소계, 아래쪽 합계는 `(GEAR)`별 소계, 오른쪽 아래는 전체 총계이다.
* `(CYL 8, GEAR 4)` 조합은 데이터가 **0건**이므로 GROUP BY 결과에 행이 만들어지지 않는다.
* Oracle에서는 오름차순 정렬 시 **NULL이 가장 마지막**에 출력된다. 아래 결과에서 소계/총계 행이 각 그룹의 맨 아래에 나오는 이유이다.

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

> `ROLLUP(CYL, GEAR)`는 **(CYL, GEAR) → (CYL) → ()** 3종류의 그룹을 만든다. **(GEAR)만의 소계는 생성되지 않는다.** (컬럼 순서가 바뀌면 결과도 달라진다.)

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

> ROLLUP 결과(12행)에 **(GEAR)별 소계 3행**(15, 12, 5)이 더해져 CUBE 결과는 15행이다.

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

> 원본 데이터에 실제 NULL 값이 있으면 소계 행의 NULL과 구분할 수 없다. 이때 `GROUPING` 함수로 소계/총계 행인지 판별한다.

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
