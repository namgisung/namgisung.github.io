---
layout: wiki
title: 4.4 윈도우함수
wiki_name: sql
parent: sql/04.SQL-활용
order: 4
---

## **4.4 윈도우 함수**

윈도우 함수(Window Function)는 **행과 행 간의 관계를 분석**하기 위한 함수이다.

일반 집계 함수와 달리 **기존 행을 유지하면서 계산 결과를 함께 출력**하며, 모든 윈도우 함수는 `OVER()` 절과 함께 사용한다.

---

### **1. 순위 함수**

순위를 계산하는 함수이다.

|함수|설명|예시|
|---|---|---|
|`RANK()`|동일 순위는 같은 값을 가지며, 다음 순위는 건너뛴다.|1,2,2,4,4,4,7|
|`DENSE_RANK()`|동일 순위는 같은 값을 가지며, 다음 순위는 바로 이어진다.|1,2,2,3,3,3,4|
|`ROW_NUMBER()`|동일 순위와 관계없이 모든 행에 고유 번호를 부여한다.|1,2,3,4,5,6|

#### 예제 1. RANK()

```sql
SELECT MPG,
       COUNT(*),
       RANK() OVER(ORDER BY COUNT(*) DESC) AS RANK
FROM MTCARS
GROUP BY MPG;
```

- `GROUP BY`가 먼저 수행되므로 `COUNT(*)`는 MPG별 차량 수가 된다.
- 차량 수가 많은 순으로 순위를 부여한다.
- 동일 순위가 있으면 다음 순위는 건너뛴다.

#### 실행 결과

|MPG|COUNT(*)|RANK|
|---:|---:|---:|
|15|4|1|
|21|4|1|
|16|3|3|
|19|3|3|
|18|2|5|
|23|2|5|
|30|2|5|
|10|2|5|
|20|1|9|
|27|1|9|
|32|1|9|
|26|1|9|
|24|1|9|
|22|1|9|
|13|1|9|
|17|1|9|
|14|1|9|
|34|1|9|

---

#### 예제 2. DENSE_RANK()

```sql
SELECT MPG,
       COUNT(*),
       DENSE_RANK() OVER(ORDER BY COUNT(*) DESC) AS RANK
FROM MTCARS
GROUP BY MPG;
```

- 차량 수가 많은 순으로 순위를 부여한다.
- 동일 순위가 있어도 다음 순위는 건너뛰지 않는다.

#### 실행 결과

|MPG|COUNT(*)|RANK|
|---:|---:|---:|
|15|4|1|
|21|4|1|
|16|3|2|
|19|3|2|
|18|2|3|
|23|2|3|
|30|2|3|
|10|2|3|
|20|1|4|
|27|1|4|
|32|1|4|
|26|1|4|
|24|1|4|
|22|1|4|
|13|1|4|
|17|1|4|
|14|1|4|
|34|1|4|

---

#### 예제 3. ROW_NUMBER()

```sql
SELECT MPG,
       COUNT(*),
       ROW_NUMBER() OVER(ORDER BY COUNT(*) DESC) AS RANK
FROM MTCARS
GROUP BY MPG;
```

- 차량 수가 많은 순으로 번호를 부여한다.
- 동일한 개수라도 모든 행이 서로 다른 번호를 가진다.

---

### **2. 집계 함수**

윈도우 함수에서도 집계 함수를 사용할 수 있다.

|함수|설명|
|---|---|
|`COUNT()`|파티션별 행 개수 또는 누적 개수|
|`SUM()`|파티션별 합계 또는 누적 합계|
|`AVG()`|파티션별 평균 또는 누적 평균|
|`MIN()`|파티션별 최솟값|
|`MAX()`|파티션별 최댓값|

#### 예제 1. 파티션별 개수

```sql
SELECT NAME,
       CYL,
       COUNT(*) OVER(PARTITION BY CYL) AS PART_CYL_CNT
FROM MTCARS
WHERE CYL <= 6;
```

- CYL(실린더 수)별로 파티션을 생성한다.
- 각 파티션의 행 개수를 출력한다.

---

#### 예제 2. 파티션별 최댓값

```sql
SELECT NAME,
       CYL,
       MPG,
       MAX(MPG) OVER(PARTITION BY CYL) AS PART_MAX_MPG
FROM MTCARS
WHERE CYL <= 6;
```

- CYL별로 파티션을 나눈다.
- 각 파티션의 최대 MPG를 출력한다.

---

### **3. 행 순서 함수**

현재 행을 기준으로 이전 또는 이후 행의 값을 참조하는 함수이다.

|함수|설명|
|---|---|
|`FIRST_VALUE()`|파티션의 첫 번째 값을 반환|
|`LAST_VALUE()`|파티션의 마지막 값을 반환|
|`LAG()`|이전 행의 값을 반환|
|`LEAD()`|이후 행의 값을 반환|

#### 예제 1. FIRST_VALUE()

```sql
SELECT NAME,
       CYL,
       MPG,
       FIRST_VALUE(MPG)
       OVER(PARTITION BY CYL) AS PART_FIRST_MPG
FROM MTCARS
WHERE CYL <= 6;
```

- CYL별 파티션을 만든다.
- 각 파티션의 첫 번째 MPG를 반환한다.

---

#### 예제 2. LAG()

```sql
SELECT NAME,
       CYL,
       MPG,
       LAG(MPG, 2)
       OVER(ORDER BY MPG) AS MPG_2
FROM MTCARS
WHERE CYL <= 6;
```

- MPG를 오름차순으로 정렬한다.
- 현재 행보다 **2행 이전**의 MPG를 출력한다.

---

### **4. 비율 함수**

누적 백분율, 순위 백분율, 등급 등을 계산하는 함수이다.

|함수|설명|
|---|---|
|`CUME_DIST()`|누적 백분율을 계산한다. 마지막 행의 값은 항상 **1**이다.|
|`PERCENT_RANK()`|순위 백분율을 계산한다. 첫 행은 **0**, 마지막 행은 **1**이다.|
|`NTILE(N)`|데이터를 N개의 그룹으로 나누어 1~N의 번호를 부여한다.|
|`RATIO_TO_REPORT()`|파티션 합계 대비 현재 값의 비율을 계산한다.|

#### 예제

```sql
SELECT NAME,
       CYL,
       MPG,
       CUME_DIST() OVER(ORDER BY MPG) AS C_DIST,
       PERCENT_RANK() OVER(ORDER BY MPG) AS P_RANK,
       NTILE(5) OVER(ORDER BY MPG) AS N_TILE,
       RATIO_TO_REPORT(MPG) OVER(PARTITION BY CYL) AS R_REPORT
FROM MTCARS
WHERE CYL <= 6;
```

- MPG 기준 누적 백분율(`CUME_DIST`)
- MPG 기준 순위 백분율(`PERCENT_RANK`)
- 데이터를 5개 그룹으로 분할(`NTILE`)
- CYL별 MPG 합계 대비 비율(`RATIO_TO_REPORT`)

#### 실행 결과

|NAME|CYL|MPG|C_DIST|P_RANK|N_TILE|R_REPORT|
|---|---:|---:|---:|---:|---:|---:|
|Valiant|6|18|0.1111|0.0000|1|0.1304|
|Merc 280C|6|18|0.1111|0.0000|1|0.1304|
|Merc 280|6|19|0.1667|0.1176|1|0.1377|
|Ferrari Dino|6|20|0.2222|0.1765|1|0.1449|
|Hornet 4 Drive|6|21|0.4444|0.2353|2|0.1522|
|Mazda RX4 Wag|6|21|0.4444|0.2353|2|0.1522|
|Mazda RX4|6|21|0.4444|0.2353|2|0.1522|
|Volvo 142E|4|21|0.4444|0.2353|2|0.0719|
|Toyota Corona|4|22|0.5000|0.4706|3|0.0753|
|Merc 230|4|23|0.6111|0.5294|3|0.0788|
|Datsun 710|4|23|0.6111|0.5294|3|0.0788|
|Merc 240D|4|24|0.6667|0.6471|3|0.0822|
|Porsche 914-2|4|26|0.7222|0.7059|4|0.0890|
|Fiat X1-9|4|27|0.7778|0.7647|4|0.0925|
|Honda Civic|4|30|0.8889|0.8235|4|0.1027|
|Lotus Europa|4|30|0.8889|0.8235|5|0.1027|
|Fiat 128|4|32|0.9444|0.9412|5|0.1096|
|Toyota Corolla|4|34|1.0000|1.0000|5|0.1164|
