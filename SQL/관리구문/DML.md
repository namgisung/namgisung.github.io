---
layout: wiki
title: 5.1 DML
wiki_name: sql
parent: sql/05.관리구문
order: 1
---

## **5.1 DML (Data Manipulation Language)**

DML(Data Manipulation Language)은 **데이터를 조회하거나 조작하는 SQL 명령어**이다.

대표적인 DML에는 `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE`가 있으며, 데이터를 조회하거나 추가·수정·삭제하는 작업을 수행한다.

> **특징**
- `SELECT` : 데이터 조회
- `INSERT` : 데이터 추가
- `UPDATE` : 데이터 수정
- `DELETE` : 데이터 삭제
- `MERGE` : 조건에 따라 수정 또는 삽입

DML은 **DDL과 달리 자동 COMMIT되지 않는다.**

따라서 `COMMIT`을 실행하기 전에는 `ROLLBACK`을 통해 작업을 취소할 수 있으며, 다른 사용자는 변경된 데이터를 조회할 수 없다.

---

### **1. INSERT**

테이블에 새로운 행(레코드)을 추가하는 명령어이다.

```sql
INSERT INTO 테이블명 [(컬럼1 [, 컬럼2 ...])]
VALUES (값1 [, 값2 ...]);
```

- 지정한 컬럼에 데이터를 삽입한다.
- 컬럼 목록을 생략하면 테이블의 **모든 컬럼 순서와 개수, 데이터 타입**에 맞게 값을 입력해야 한다.
- 컬럼 목록에 없는 컬럼은 `NULL`이 입력된다.
- 단, `PRIMARY KEY` 또는 `NOT NULL` 제약조건이 있는 컬럼에는 `NULL`을 입력할 수 없다.

```sql
INSERT INTO MEMBER (MEMBER_ID, NAME, EMAIL)
VALUES (1006, 'Ethan', 'ETHAN@GMAIL.COM');
```

- MEMBER 테이블에 새로운 행을 추가한다.
- `PHONE` 컬럼은 값을 입력하지 않았으므로 `NULL`이 저장된다.

```sql
INSERT INTO MEMBER
VALUES (1006, 'Ethan', 'ETHAN@GMAIL.COM', '010-5532-6565');
```

- MEMBER 테이블의 모든 컬럼에 값을 입력한다.
- 컬럼 순서와 데이터 개수가 테이블 구조와 일치해야 한다.

---

### **2. UPDATE**

기존 데이터를 수정하는 명령어이다.

`WHERE`절을 이용하여 수정할 행을 지정한다.

```sql
UPDATE 테이블명
SET 컬럼1 = 값1 [, 컬럼2 = 값2 ...]
[WHERE 조건식];
```

- 조건에 맞는 행의 값을 수정한다.
- `WHERE`절을 생략하면 **모든 행이 수정**되므로 주의해야 한다.

```sql
UPDATE MEMBER
SET PHONE = '010-7788-6809'
WHERE MEMBER_ID = 1006;
```

- MEMBER_ID가 1006인 회원의 전화번호를 변경한다.

#### **해설**

1. `MEMBER` 테이블에서 `MEMBER_ID`가 1006인 행을 찾는다.
2. 해당 행의 `PHONE` 컬럼 값을 `'010-7788-6809'`로 수정한다.

---

### **3. DELETE**

기존 데이터를 삭제하는 명령어이다.

```sql
DELETE FROM 테이블명
[WHERE 조건식];
```

- 조건에 맞는 행을 삭제한다.
- `WHERE`절을 생략하면 **모든 행이 삭제**된다.

```sql
DELETE FROM MEMBER
WHERE MEMBER_ID = 1006;
```

- MEMBER_ID가 1006인 회원 정보를 삭제한다.

#### **해설**

1. `MEMBER` 테이블에서 `MEMBER_ID`가 1006인 행을 찾는다.
2. 해당 행을 삭제한다.

> **DELETE와 TRUNCATE의 차이**

|구분|DELETE|TRUNCATE|
|---|---|---|
|종류|DML|DDL|
|삭제 대상|조건에 맞는 행 또는 전체 행|테이블 전체|
|WHERE 사용|가능|불가능|
|ROLLBACK|가능|불가능(자동 COMMIT)|
|속도|상대적으로 느림|빠름|

---

### **4. MERGE**

`MERGE`는 **조건에 따라 UPDATE 또는 INSERT를 수행하는 명령어**이다.

대상 테이블과 비교 테이블을 비교하여,
- 조건이 일치하면 `UPDATE`
- 조건이 일치하지 않으면 `INSERT`
를 수행한다.

```sql
MERGE INTO 대상테이블
USING 비교테이블
ON (조건식)
WHEN MATCHED THEN
    UPDATE SET ...
WHEN NOT MATCHED THEN
    INSERT (...)
    VALUES (...);
```

- `USING` : 비교 대상 테이블을 지정한다.
- `ON` : 두 테이블을 비교할 조건을 지정한다.
- `WHEN MATCHED` : 조건이 일치하면 UPDATE를 수행한다.
- `WHEN NOT MATCHED` : 조건이 일치하지 않으면 INSERT를 수행한다.
- `WHEN MATCHED`와 `WHEN NOT MATCHED`는 하나만 사용할 수도 있다.

```sql
MERGE INTO MEMBER_BACKUP MB
USING MEMBER M
ON (MB.MEMBER_ID = M.MEMBER_ID)
WHEN MATCHED THEN
    UPDATE SET
        MB.NAME = M.NAME,
        MB.EMAIL = M.EMAIL,
        MB.PHONE = M.PHONE
WHEN NOT MATCHED THEN
    INSERT (MEMBER_ID, NAME, EMAIL, PHONE)
    VALUES (M.MEMBER_ID, M.NAME, M.EMAIL, M.PHONE);
```

- MEMBER 테이블의 데이터를 MEMBER_BACKUP 테이블과 비교한다.
- 동일한 MEMBER_ID가 있으면 정보를 수정한다.
- 없으면 새로운 회원 정보를 추가한다.

#### **해설**

1. `MEMBER_BACKUP`과 `MEMBER`를 `MEMBER_ID`를 기준으로 비교한다.
2. 동일한 회원이 존재하면 `NAME`, `EMAIL`, `PHONE`을 최신 정보로 수정한다.
3. 동일한 회원이 존재하지 않으면 새로운 회원 정보를 삽입한다.
4. 백업 테이블을 원본 테이블과 동일한 상태로 유지할 때 자주 사용된다.
