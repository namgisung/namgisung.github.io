---
layout: wiki
title: 4.7 PIVOT절과 UNPIVIT절
wiki_name: sql
parent: sql/04.SQL-활용
order: 7
---

## **4.7 PIVOT절과 UNPIVOT절**

PIVOT과 UNPIVOT은 **테이블의 행(Row)과 열(Column)을 서로 변환**하는 기능이다.

* **PIVOT** : 행(Row)을 열(Column)로 변환한다.
* **UNPIVOT** : 열(Column)을 행(Row)으로 변환한다.

주로 데이터를 집계하거나 보고서(교차표)를 생성할 때 사용한다.

---

### **1. PIVOT절**

PIVOT은 **행(Row)을 열(Column)로 변환**하는 기능이다.

지정한 칼럼의 각 행 값이 새로운 열(Column)이 되며, 해당 값에 대해 집계 함수(`COUNT`, `SUM`, `AVG` 등)를 수행한다.

먼저 `EMP` 테이블과 `DEPT` 테이블을 조인하여 PIVOT의 대상 데이터를 만든다.

```sql
SELECT E.JOB, D.DNAME
FROM EMP E, DEPT D
WHERE E.DEPTNO = D.DEPTNO;
```

#### **조회 결과**

| JOB       | DNAME      |
| --------- | ---------- |
| PRESIDENT | ACCOUNTING |
| MANAGER   | ACCOUNTING |
| CLERK     | ACCOUNTING |
| ANALYST   | RESEARCH   |
| ANALYST   | RESEARCH   |
| CLERK     | RESEARCH   |
| MANAGER   | RESEARCH   |
| CLERK     | SALES      |
| SALESMAN  | SALES      |
| SALESMAN  | SALES      |
| SALESMAN  | SALES      |
| SALESMAN  | SALES      |
| MANAGER   | SALES      |

이를 PIVOT으로 변환하면 다음과 같다.

```sql
SELECT *
FROM (
    SELECT E.JOB, D.DNAME
    FROM EMP E, DEPT D
    WHERE E.DEPTNO = D.DEPTNO
)
PIVOT (
    COUNT(*)
    FOR DNAME IN (
        'ACCOUNTING' AS ACCOUNTING,
        'RESEARCH' AS RESEARCH,
        'SALES' AS SALES
    )
);
```

* `EMP` 테이블과 `DEPT` 테이블을 조인한 결과를 기준으로 PIVOT을 수행한다.
* `JOB`을 행(Row)으로 사용하고 `DNAME`을 열(Column)로 변환한다.
* 각 부서별 직업의 개수를 `COUNT(*)`로 집계한다.

#### **해설**

1. 서브쿼리에서 `EMP`와 `DEPT`를 조인하여 `JOB`, `DNAME` 데이터를 생성한다.
2. `PIVOT` 절에서 `DNAME`의 값을 각각 하나의 열(`ACCOUNTING`, `RESEARCH`, `SALES`)로 변환한다.
3. 각 부서별(`DNAME`) 직업(`JOB`)의 개수를 `COUNT(*)`로 집계한다.
4. 결과적으로 **행은 직업(JOB), 열은 부서(DNAME)** 인 교차표(Cross Tab)가 생성된다.

#### **실행 결과**

| JOB       | ACCOUNTING | RESEARCH | SALES |
| --------- | ---------: | -------: | ----: |
| PRESIDENT |          1 |        0 |     0 |
| MANAGER   |          1 |        1 |     1 |
| CLERK     |          1 |        1 |     1 |
| ANALYST   |          0 |        2 |     0 |
| SALESMAN  |          0 |        0 |     4 |

---

### **2. UNPIVOT절**

UNPIVOT은 **열(Column)을 행(Row)으로 변환**하는 기능이다.

여러 개의 열에 저장된 데이터를 하나의 열로 변환하여 집계나 분석이 쉽도록 재구성한다.

예를 들어 다음과 같은 평균 기온 테이블이 있다고 가정한다.

| 계절 | Y2018 | Y2019 | Y2020 | Y2021 | Y2022 |
| -- | ----: | ----: | ----: | ----: | ----: |
| 봄  |  12.9 |  12.5 |  12.0 |  12.8 |  13.2 |
| 여름 |  25.3 |  23.9 |  24.0 |  24.2 |  24.5 |
| 가을 |  13.5 |  15.2 |  14.0 |  14.9 |  14.8 |
| 겨울 |   1.0 |   2.8 |   1.0 |   0.3 |   0.2 |

이와 같은 형태에서는 연도별 `GROUP BY` 연산을 수행하기 어렵다.

이를 `UNPIVOT`으로 변환하면 다음과 같다.

```sql
SELECT 계절, 연도, 기온
FROM (
    SELECT *
    FROM 평균기온
)
UNPIVOT (
    기온
    FOR 연도 IN (
        Y2018 AS '2018년',
        Y2019 AS '2019년',
        Y2020 AS '2020년',
        Y2021 AS '2021년',
        Y2022 AS '2022년'
    )
);
```

#### **해설**

1. `평균기온` 테이블을 조회한다.
2. `UNPIVOT`을 이용하여 여러 연도 칼럼(`Y2018` ~ `Y2022`)을 하나의 `연도` 칼럼으로 변환한다.
3. 각 연도의 값을 하나의 `기온` 칼럼으로 변환한다.
4. 결과적으로 **계절 / 연도 / 기온** 형태의 세로 구조 테이블이 생성된다.
5. 이렇게 변환하면 `GROUP BY 연도`, `GROUP BY 계절`과 같은 집계 연산을 쉽게 수행할 수 있다.

#### **실행 결과**

| 계절 | 연도    |   기온 |
| -- | ----- | ---: |
| 봄  | 2018년 | 12.9 |
| 봄  | 2019년 | 12.5 |
| 봄  | 2020년 | 12.0 |
| 봄  | 2021년 | 12.8 |
| 봄  | 2022년 | 13.2 |
| 여름 | 2018년 | 25.3 |
| 여름 | 2019년 | 23.9 |
| 여름 | 2020년 | 24.0 |
| 여름 | 2021년 | 24.2 |
| 여름 | 2022년 | 24.5 |
| 가을 | 2018년 | 13.5 |
| 가을 | 2019년 | 15.2 |
| 가을 | 2020년 | 14.0 |
| 가을 | 2021년 | 14.9 |
| 가을 | 2022년 | 14.8 |
| 겨울 | 2018년 |  1.0 |
| 겨울 | 2019년 |  2.8 |
| 겨울 | 2020년 |  1.0 |
| 겨울 | 2021년 |  0.3 |
| 겨울 | 2022년 |  0.2 |

### **PIVOT과 UNPIVOT 비교**

| 구분    | PIVOT              | UNPIVOT             |
| ----- | ------------------ | ------------------- |
| 변환 방향 | 행(Row) → 열(Column) | 열(Column) → 행(Row)  |
| 주요 목적 | 교차표(Cross Tab) 생성  | 정규화된 형태로 변환         |
| 주요 사용 | 보고서, 통계 출력         | 집계 및 분석을 위한 데이터 재구성 |
