---
layout: wiki
title: 4.1 서브쿼리
wiki_name: sql
parent: sql/04.SQL-활용
order: 1
---

## 4.1 서브쿼리**

SQL문 안에는 DBMS가 제공하는 다양한 함수뿐만 아니라 **또 다른 SQL문을 포함**할 수도 있다.

이처럼 **SQL문 내부에 포함되는 또 다른 독립적인 SQL문**을 **서브쿼리(Subquery)** 라고 한다.

---

### **1. 서브쿼리의 종류**

#### **서브쿼리가 위치하는 곳에 따른 분류**

| 종류                        | 위치                          |
| ------------------------- | --------------------------- |
| 스칼라 서브쿼리(Scalar Subquery) | SELECT절의 컬럼 위치 (반환 컬럼 1개)   |
| 인라인 뷰(Inline View)        | FROM절의 테이블 위치 (반환 컬럼 2개 이상) |
| 중첩 서브쿼리(Nested Subquery)  | WHERE절, HAVING절 등의 조건식      |

---

#### **메인쿼리와의 관계에 따른 분류**

| 종류                     | 설명                     |
| ---------------------- | ---------------------- |
| 연관(Correlated) 서브쿼리    | 메인쿼리의 컬럼을 서브쿼리에서 참조한다. |
| 비연관(Uncorrelated) 서브쿼리 | 메인쿼리의 컬럼을 참조하지 않는다.    |

---

### **2. 스칼라 서브쿼리(Scalar Subquery)**

스칼라 서브쿼리는 **SELECT절처럼 컬럼이 들어가는 위치**에 사용하는 서브쿼리이다.

컬럼 위치에 들어가기 때문에 **반드시 하나의 컬럼만 반환**해야 한다.

#### **예제**

```sql
SELECT
    E.EMPNO,
    E.ENAME,
    (
        SELECT D.DNAME
        FROM DEPT D
        WHERE D.DEPTNO = E.DEPTNO
    ) AS DNAME
FROM EMP E;
```

사원(EMP) 정보를 조회하면서 부서(DEPT) 테이블에서 해당 부서명을 함께 조회한다.

#### **해설**

1. 서브쿼리에서 `DEPTNO`가 같은 `DNAME`을 조회한다.
2. 조회된 부서명을 `DNAME`이라는 별칭으로 SELECT절에 출력한다.
3. 최종적으로 사원번호, 사원명, 부서명을 함께 조회한다.

---

### **3. 인라인 뷰(Inline View)**

인라인 뷰는 **FROM절의 테이블 위치**에 사용하는 서브쿼리이다.

실행 시 일시적으로 생성되는 **가상의 테이블(View)** 처럼 동작한다.

인라인 뷰를 사용하면

* 복잡한 SQL을 단계적으로 작성할 수 있고,
* 필요한 컬럼만 먼저 추출하여 비교 대상이 줄어들므로 성능 향상에 도움이 될 수 있다.

#### **예제**

```sql
SELECT
    E.EMPNO,
    E.ENAME,
    D.DEPTNO,
    D.DNAME,
    D.LOC
FROM EMP E,
(
    SELECT DEPTNO, DNAME, LOC
    FROM DEPT
) D
WHERE E.DEPTNO = D.DEPTNO;
```

부서 테이블에서 필요한 컬럼만 먼저 추출한 후 사원 테이블과 조인한다.

#### **해설**

1. 서브쿼리에서 `DEPTNO`, `DNAME`, `LOC`만 조회한다.
2. 조회 결과에 `D`라는 별칭을 부여한다.
3. `EMP`와 `D`의 `DEPTNO`가 같은 행만 조회한다.
4. 사원번호, 사원명, 부서번호, 부서명, 지역을 출력한다.

---
