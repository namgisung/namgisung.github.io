---
layout: wiki
title: 4.6 계층형 질의와 셀프 조인
wiki_name: sql
parent: sql/04.SQL-활용
order: 6
---

## **4.6 계층형 질의와 셀프 조인**

각 레코드가 하나의 노드(Node)가 되고, 노드 간의 부모-자식 관계를 정의하여 트리(Tree) 구조처럼 데이터를 표현하는 모델을 **계층형 데이터 모델(Hierarchical Data Model)**이라고 한다.

계층형 모델에서는 상위 노드(부모)에서 하위 노드(자식)로 또는 하위 노드에서 상위 노드로 데이터를 조회해야 하는 경우가 많으며, 이를 처리하는 방법으로 **계층형 질의(Hierarchical Query)**와 **셀프 조인(Self Join)**을 사용할 수 있다.

---

### **1. 계층형 질의**

계층형 질의는 계층 구조를 가지는 데이터를 조회하기 위해 Oracle에서 제공하는 전용 문법이다.

셀프 조인보다 간단한 SQL로 계층 구조를 조회할 수 있으며, 조직도·게시판·카테고리와 같은 트리 구조 데이터를 처리할 때 많이 사용된다.

|키워드|설명|
|---|---|
|`LEVEL`|현재 노드의 계층(Level)을 반환한다. 루트 노드는 1이며, 한 단계 내려갈 때마다 1씩 증가한다.|
|`SYS_CONNECT_BY_PATH`|루트 노드부터 현재 노드까지의 전체 경로를 문자열로 반환한다.|
|`START WITH`|계층 구조의 시작(루트 노드) 조건을 지정한다.|
|`CONNECT BY`|부모 노드와 자식 노드의 연결 조건을 지정한다.|
|`CONNECT_BY_ROOT`|현재 행이 속한 루트 노드의 값을 반환한다.|
|`CONNECT_BY_ISLEAF`|말단(Leaf) 노드이면 1, 그렇지 않으면 0을 반환한다.|
|`PRIOR`|부모 행을 참조하는 키워드이다.|
|`NOCYCLE`|순환(Cycle)이 발생할 경우 무한 루프를 방지한다.|
|`ORDER SIBLINGS BY`|같은 부모를 가진 형제 노드끼리 정렬한다.|

#### **순방향 전개 (부모 → 자식)**

```sql
CONNECT BY PRIOR 부모키 = 자식키
```

부모 노드에서 시작하여 자식 노드 방향으로 계층을 조회한다.

#### **역방향 전개 (자식 → 부모)**

```sql
CONNECT BY PRIOR 자식키 = 부모키
```

자식 노드에서 시작하여 부모 노드 방향으로 계층을 조회한다.

#### **예제 1. 순방향 전개 (부모 → 자식)**

```sql
SELECT LEVEL,
       EMPNO,
       ENAME,
       MGR
FROM EMP
START WITH MGR IS NULL
CONNECT BY PRIOR EMPNO = MGR;
```

- `START WITH MGR IS NULL` : 최상위 관리자(루트 노드)부터 시작한다.
- `CONNECT BY PRIOR EMPNO = MGR` : 부모의 사원번호(`EMPNO`)와 자식의 관리자번호(`MGR`)를 연결하여 **부모 → 자식** 방향으로 조회한다.
- `LEVEL`을 이용하여 현재 계층의 깊이를 확인할 수 있다.

#### 예시 결과

|LEVEL|EMPNO|ENAME|MGR|
|---:|---:|---|---:|
|1|7839|KING|NULL|
|2|7566|JONES|7839|
|2|7698|BLAKE|7839|
|2|7782|CLARK|7839|
|3|7788|SCOTT|7566|
|3|7902|FORD|7566|
|3|7499|ALLEN|7698|
|3|7521|WARD|7698|

---

#### **예제 2. 역방향 전개 (자식 → 부모)**

```sql
SELECT LEVEL,
       EMPNO,
       ENAME,
       MGR
FROM EMP
START WITH EMPNO = 7902
CONNECT BY PRIOR MGR = EMPNO;
```

- `START WITH EMPNO = 7902` : 사원번호가 7902인 사원부터 시작한다.
- `CONNECT BY PRIOR MGR = EMPNO` : 현재 사원의 관리자(`MGR`)를 따라 **자식 → 부모** 방향으로 조회한다.
- 특정 사원의 상위 조직 구조를 확인할 때 사용한다.

#### 예시 결과

|LEVEL|EMPNO|ENAME|MGR|
|---:|---:|---|---:|
|1|7902|FORD|7566|
|2|7566|JONES|7839|
|3|7839|KING|NULL|

---

#### **예제 3. 부모 정보 함께 조회**

```sql
SELECT *
FROM (
    SELECT LEVEL AS LVL,
           EMPNO,
           JOB,
           PRIOR ENAME AS MANAGER,
           PRIOR JOB AS MANAGER_JOB
    FROM EMP
    START WITH MGR IS NULL
    CONNECT BY PRIOR EMPNO = MGR
)
ORDER BY LVL;
```

- `LEVEL`을 이용하여 계층(Level)을 표시한다.
- `PRIOR ENAME`은 현재 사원의 **부모(상사)의 이름**을 반환한다.
- `PRIOR JOB`은 현재 사원의 **부모(상사)의 직급**을 반환한다.
- `ORDER BY LVL`을 사용하여 같은 계층(Level)끼리 정렬하여 출력한다.

#### **설명**

1. `START WITH MGR IS NULL`로 최상위 관리자부터 계층 탐색을 시작한다.
2. `CONNECT BY PRIOR EMPNO = MGR`을 통해 부모 → 자식 방향으로 계층을 전개한다.
3. `PRIOR` 키워드를 사용하여 현재 행의 부모 노드 정보를 함께 조회한다.
4. `LEVEL`을 이용하여 조직의 깊이를 확인할 수 있으며, 결과를 계층별로 정렬하여 출력한다.

#### **예시 결과**

|LVL|EMPNO|JOB|MANAGER|MANAGER_JOB|
|---:|---:|---|---|---|
|1|7839|PRESIDENT|NULL|NULL|
|2|7566|MANAGER|KING|PRESIDENT|
|2|7698|MANAGER|KING|PRESIDENT|
|2|7782|MANAGER|KING|PRESIDENT|
|3|7788|ANALYST|JONES|MANAGER|
|3|7902|ANALYST|JONES|MANAGER|
|3|7499|SALESMAN|BLAKE|MANAGER|
|3|7521|SALESMAN|BLAKE|MANAGER|

---

### **2. 셀프 조인(Self Join)**

셀프 조인은 **하나의 테이블을 자기 자신과 조인(Self Join)**하는 기법이다.

하나의 테이블 안에 부모-자식 관계(상사-부하, 조직도 등)가 함께 저장되어 있을 때 주로 사용한다.

동일한 테이블을 두 번 사용하는 것이므로 **반드시 테이블 별칭(Alias)**을 지정하여 서로 다른 테이블처럼 구분해야 한다.

계층형 질의를 지원하지 않는 DBMS에서는 계층 구조를 조회하기 위해 셀프 조인을 많이 사용한다.

```sql
SELECT B.EMPNO,
       B.ENAME,
       B.JOB,
       A.ENAME AS BOSS,
       A.JOB AS BOSS_JOB
FROM EMP A,
     EMP B
WHERE A.EMPNO = B.MGR;
```

- EMP 테이블을 자기 자신과 조인하여 사원과 상사의 정보를 함께 조회한다.

#### **설명**

1. `EMP A`는 **상사(부모)** 역할의 테이블이다.
2. `EMP B`는 **사원(자식)** 역할의 테이블이다.
3. `A.EMPNO = B.MGR` 조건으로 상사의 사원번호와 사원의 관리자번호를 연결한다.
4. 사원의 정보와 함께 해당 사원의 상사 이름과 직급을 조회한다.

#### **예시 결과**

|EMPNO|ENAME|JOB|BOSS|BOSS_JOB|
|---:|---|---|---|---|
|7499|ALLEN|SALESMAN|BLAKE|MANAGER|
|7521|WARD|SALESMAN|BLAKE|MANAGER|
|7566|JONES|MANAGER|KING|PRESIDENT|
|7902|FORD|ANALYST|JONES|MANAGER|
