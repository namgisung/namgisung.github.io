---
layout: wiki
title: 5.2 TCL
wiki_name: sql
parent: sql/05.관리구문
order: 2
---

# **5.2 TCL**

TCL(Transaction Control Language)은 **트랜잭션을 제어하는 SQL 명령어**이다.

트랜잭션(Transaction)이란 데이터베이스에서 데이터를 읽고 쓰는 작업을 **하나의 논리적인 작업 단위**로 묶은 것이다.

트랜잭션은 데이터의 **무결성(Integrity)**을 보장하기 위해 반드시 함께 수행되어야 하는 작업들을 하나로 관리한다.

TCL은 INSERT, UPDATE, DELETE와 같은 DML 명령어들을 하나의 트랜잭션으로 묶어 처리하거나, 수행한 작업을 취소할 수 있는 기능을 제공한다.

---

## **1. 트랜잭션의 특징(ACID)**

| 특징               | 설명                                                            |
| ---------------- | ------------------------------------------------------------- |
| 원자성(Atomicity)   | 하나의 트랜잭션으로 묶인 작업은 **모두 수행되거나(All), 전혀 수행되지 않아야 한다(Nothing).** |
| 일관성(Consistency) | 트랜잭션 수행 전 데이터베이스가 일관된 상태였다면, 수행 후에도 일관된 상태를 유지해야 한다.          |
| 고립성(Isolation)   | 트랜잭션은 서로 독립적으로 수행되며, 다른 트랜잭션의 작업에 영향을 받지 않는다.                 |
| 영속성(Durability)  | 성공적으로 완료(COMMIT)된 트랜잭션의 결과는 데이터베이스에 영구적으로 저장된다.               |

---

## **2. COMMIT**

COMMIT 명령어는 INSERT, UPDATE, DELETE와 같은 DML 명령을 통해 수행한 변경사항을 **데이터베이스에 영구적으로 반영**하고 **락(Lock)을 해제**하여 트랜잭션을 종료한다.

> **COMMIT 이후에는 ROLLBACK으로 변경사항을 취소할 수 없다.**

---

## **3. ROLLBACK**

ROLLBACK은 **마지막 COMMIT 이후 수행된 모든 변경사항**, 또는 **SAVEPOINT 이후의 변경사항만 취소**하여 이전 상태로 되돌린다.

COMMIT과 마찬가지로 ROLLBACK을 수행하면 **락(Lock)이 해제**된다.

> **ROLLBACK은 마지막 COMMIT 이후의 변경사항만 취소할 수 있으며, 이미 COMMIT된 내용은 취소할 수 없다.**

또한 Oracle에서는 **CREATE, ALTER, DROP, TRUNCATE**와 같은 DDL 명령어는 **자동 COMMIT**되므로 ROLLBACK이 불가능하다.

반면 **INSERT, UPDATE, DELETE**와 같은 DML 명령어는 자동 COMMIT되지 않으므로 ROLLBACK이 가능하다.

> **※ Oracle 기준**

---

### 예제

#### [주문]

| 고객번호 | 주문금액 |
| ---- | ---: |
| 1001 | 1000 |
| 1002 | 2000 |
| 1003 | 3000 |

```sql
BEGIN TRANSACTION;

INSERT INTO 주문(고객번호, 주문금액)
VALUES(1004, 2000);

COMMIT;

BEGIN TRANSACTION;

DELETE 주문
WHERE 고객번호 = 1001;

BEGIN TRANSACTION;

UPDATE 주문
SET 주문금액 = 2000
WHERE 고객번호 = 1003;

ROLLBACK;

SELECT COUNT(*)
FROM 주문
WHERE 주문금액 <= 2000;
```

**실행 결과**

```text
3
```

**설명**

* 고객번호 1004 추가 → **COMMIT**되어 영구 반영
* 고객번호 1001 삭제 → ROLLBACK으로 취소
* 고객번호 1003 금액 변경 → ROLLBACK으로 취소
* 따라서 최종 데이터는 다음과 같다.

| 고객번호 | 주문금액 |
| ---- | ---: |
| 1001 | 1000 |
| 1002 | 2000 |
| 1003 | 3000 |
| 1004 | 2000 |

주문금액이 **2000 이하**인 고객은 **1001, 1002, 1004** 총 **3건**이다.

---

## **4. SAVEPOINT**

SAVEPOINT는 **ROLLBACK을 수행하기 위한 저장점**을 지정하는 명령어이다.

ROLLBACK TO SAVEPOINT를 수행하면 **저장점 이후의 변경사항만 취소**되며, 저장점 이전의 변경사항은 유지된다.

---

### Oracle

```sql
SAVEPOINT <이름>;

ROLLBACK TO <이름>;
```

Oracle에서는 별도로 트랜잭션의 시작을 지정하지 않는다.

**첫 번째 DML(INSERT, UPDATE, DELETE)이 실행되는 순간 자동으로 트랜잭션이 시작된다.**

---

### SQL Server

```sql
BEGIN TRANSACTION;

SAVE TRANSACTION <이름>;

ROLLBACK TRANSACTION <이름>;
```

SQL Server에서는 **BEGIN TRANSACTION**으로 트랜잭션의 시작을 명시적으로 지정할 수 있다.

---

### 예제

#### [주문]

| 고객번호 | 주문금액 |
| ---- | ---: |
| 1001 | 1000 |
| 1002 | 2000 |
| 1003 | 3000 |

```sql
BEGIN TRANSACTION;

SAVE TRANSACTION SP1;

UPDATE 주문
SET 주문금액 = 2000
WHERE 고객번호 = 1003;

SAVE TRANSACTION SP2;

UPDATE 주문
SET 주문금액 = 1000
WHERE 고객번호 = 1001;

ROLLBACK TRANSACTION SP2;

COMMIT;
```

**실행 결과**

| 고객번호 | 주문금액 |
| ---- | ---: |
| 1001 | 1000 |
| 1002 | 2000 |
| 1003 | 2000 |

**설명**

1. **SP1 저장**
2. 고객번호 **1003**의 주문금액을 **3000 → 2000**으로 변경
3. **SP2 저장**
4. 고객번호 **1001**의 주문금액을 **1000 → 1000**으로 변경
5. **ROLLBACK TO SP2** 수행

   * **SP2 이후 작업만 취소**
   * 1001에 대한 변경만 취소된다.
   * SP2 이전에 수행한 **1003의 변경은 유지된다.**
6. COMMIT을 수행하여 최종 결과를 저장한다.

---

### SQLD 시험 포인트

* **COMMIT 이후에는 ROLLBACK이 불가능하다.**
* **ROLLBACK은 마지막 COMMIT 이후의 변경사항만 취소한다.**
* **SAVEPOINT는 저장점 이후의 변경사항만 취소한다.**
* **Oracle에서는 DDL(CREATE, ALTER, DROP, TRUNCATE)이 자동 COMMIT된다.**
* **Oracle은 첫 DML 실행 시 트랜잭션이 자동 시작되며, SQL Server는 BEGIN TRANSACTION으로 시작할 수 있다.**
