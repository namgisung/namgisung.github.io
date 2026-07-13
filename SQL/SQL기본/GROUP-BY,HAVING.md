---
layout: wiki
title: 3.5 GROUP BY, HAVIG절
wiki_name: sql
parent: sql/03.SQL-기본
order: 5
---

## **1. GROUP BY절**

`GROUP BY`절은 **특정 칼럼을 기준으로 데이터를 그룹화(Grouping)** 할 때 사용하는 절이다.

그룹별로 데이터를 묶은 후 집계 함수를 이용하여 합계, 평균, 개수 등의 통계 값을 계산할 수 있다.

> `GROUP BY` 연산은 부하가 큰 연산이므로, 조건을 적용해야 하는 경우에는 가능하면 `WHERE`절을 먼저 사용하여 데이터를 필터링한 후 `GROUP BY`를 수행하는 것이 효율적이다.

---

### **기본 문법**

```sql
SELECT 그룹핑할_칼럼, 집계함수(칼럼)
FROM 테이블명
GROUP BY 그룹핑할_칼럼;
```

---

### **예제**

```sql
SELECT DEPTNO, SUM(SAL) AS SALS
FROM EMP
GROUP BY DEPTNO;
```

#### **해설**

1. `EMP` 테이블에서
2. `DEPTNO`를 기준으로 그룹화한 후,
3. 부서별 `SAL`의 합계를 조회한다.

---

## **2. 집계 함수(Aggregate Function)**

집계 함수는 `GROUP BY`절로 생성된 각 그룹에 대해 통계 값을 계산하는 함수이다.

| 함수    | 설명                     |
| ----- | ---------------------- |
| COUNT | NULL을 제외한 행의 개수를 반환한다. |
| SUM   | 합계를 반환한다.              |
| AVG   | 평균을 반환한다.              |
| MIN   | 최솟값을 반환한다.             |
| MAX   | 최댓값을 반환한다.             |

---

### **DISTINCT**

`DISTINCT`는 **중복된 값을 제거**하는 키워드이다.

집계 함수의 인자로 사용하면 **중복을 제거한 값만을 대상으로 집계 함수가 수행**된다.

#### **예제**

```sql
SELECT COUNT(DISTINCT DEPTNO)
FROM EMP;
```

위 예제는 중복된 부서번호를 제외한 개수를 반환한다.

---

## **3. HAVING절**

`HAVING`절은 **그룹화된 결과에 조건을 지정**할 때 사용하는 절이다.

`WHERE`절과 달리 **집계 함수를 사용할 수 있다.**

`GROUP BY`절과 함께 사용하면 그룹화가 완료된 이후 조건을 만족하는 그룹만 조회한다.

---

### **기본 문법**

```sql
SELECT 그룹핑할_칼럼
FROM 테이블명
GROUP BY 그룹핑할_칼럼
HAVING 조건식;
```

---

### **예제**

```sql
SELECT ID
FROM TBL
GROUP BY ID
HAVING COUNT(*) = 2;
```

#### **해설**

1. `TBL` 테이블에서
2. `ID`를 기준으로 그룹화한 후,
3. 각 그룹의 행 개수가 `2`인 그룹만 선택하여
4. `ID`를 조회한다.

---

## **4. WHERE와 HAVING의 차이**

| 구분       | WHERE       | HAVING      |
| -------- | ----------- | ----------- |
| 실행 시점    | GROUP BY 이전 | GROUP BY 이후 |
| 집계 함수 사용 | 불가능         | 가능          |
| 필터링 대상   | 개별 행(Row)   | 그룹(Group)   |

---

### **추가 정리**

| 절        | 역할                   |
| -------- | -------------------- |
| GROUP BY | 데이터를 그룹화한다.          |
| COUNT    | 행의 개수를 계산한다.         |
| SUM      | 합계를 계산한다.            |
| AVG      | 평균을 계산한다.            |
| MIN      | 최솟값을 계산한다.           |
| MAX      | 최댓값을 계산한다.           |
| HAVING   | 그룹화된 결과를 조건으로 필터링한다. |
| DISTINCT | 중복된 값을 제거한다.         |

> SQLD에서는 **WHERE와 HAVING의 차이**, **집계 함수**, **GROUP BY *행 순서**, **DISTINCT와 집계 함*의 사용 방법**이 자주 출제된다.
