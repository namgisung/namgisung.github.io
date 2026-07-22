---
layout: wiki
title: 4.2 집합연산자
wiki_name: sql
parent: sql/04.SQL-활용
order: 2
---

## **4.2 집합연산자**

집합연산자는 **두 테이블에 대해 집합 연산을 수행하는 연산자**이다.

JOIN이 기준 키(PK/FK 등)를 이용하여 테이블을 연결하는 것과 달리, 집합연산자는 **기준 키 없이 두 테이블의 레코드 자체를 대상으로 집합 연산**을 수행한다.

> 집합연산자를 사용하려면 **두 테이블의 컬럼 개수와 데이터 타입(스키마)이 동일**해야 한다.

---

### **1. UNION ALL / UNION**

두 테이블의 **합집합(Union)***을*반환한다.

두 테이블의 모든 레코드를 합쳐서 조회하며, **중복 레코드 처리 방식**에 따라 `UNION ALL`과 `UNION`으로 구분된다.

| 연산자       | 설명                       |
| --------- | ------------------------ |
| UNION ALL | 중복 레코드를 제거하지 않고 모두 반환한다. |
| UNION     | 중복 레코드를 제거한 후 반환한다.      |

> **주의**
> `UNION`은 두 테이블 간의 중복뿐만 아니라 **각 테이블 내부의 중복 레코드도 제거**한다.

#### **UNION ALL 예제**

```sql
SELECT NAME, TEL, CLASS
FROM CLUB1

UNION ALL

SELECT NAME, TEL, CLASS
FROM CLUB2;
```

**해설**

1. CLUB1과 CLUB2의 데이터를 병합한다.
2. 중복된 레코드도 그대로 모두 출력한다.

---

#### **UNION 예제**

```sql
SELECT NAME, TEL, CLASS
FROM CLUB1

UNION

SELECT NAME, TEL, CLASS
FROM CLUB2;
```

**해설**

1. CLUB1과 CLUB2의 데이터를 병합한다.
2. 중복된 레코드는 하나만 남기고 제거한다.

---

### **2. INTERSECT**

두 테이블의 **교집합(Intersection)***을*반환한다.

두 테이블에 **공통으로 존재하는 레코드만 조회**한다.

#### **예제**

```sql id="u0w5tp"
SELECT NAME, TEL, CLASS
FROM CLUB1

INTERSECT

SELECT NAME, TEL, CLASS
FROM CLUB2;
```

**해설**

1. CLUB1과 CLUB2를 비교한다.
2. 두 테이블에 공통으로 존재하는 레코드만 출력한다.

---

### **3. MINUS / EXCEPT**

두 테이블의 **차집합(Difference)***을*반환한다.

왼쪽 테이블에는 존재하지만 오른쪽 테이블에는 존재하지 않는 레코드만 조회한다.

> Oracle에서는 `MINUS`, SQL Server에서는 `EXCEPT`를 사용한다.

#### **예제**

```sql
SELECT NAME, TEL, CLASS
FROM CLUB1

MINUS

SELECT NAME, TEL, CLASS
FROM CLUB2;
```

**해설**

1. CLUB1의 데이터를 기준으로 한다.
2. CLUB2와 공통되는 레코드를 제거한다.
3. CLUB1에만 존재하는 레코드만 출력한다.

---

### **집합연산자 비교**

| 연산자            | 의미  | 중복 처리                |
| -------------- | --- | -------------------- |
| UNION ALL      | 합집합 | 중복 허용                |
| UNION          | 합집합 | 중복 제거                |
| INTERSECT      | 교집합 | 공통 레코드만 반환           |
| MINUS / EXCEPT | 차집합 | 왼쪽 테이블에만 존재하는 레코드 반환 |

> SQLD에서는 **UNION과 UNION ALL의 차이**, **INTERSECT**, **MINUS(EXCEPT)***의 결과를 묻는 문제가 자주 출제된다.
