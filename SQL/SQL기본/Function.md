---
layout: wiki
title: 3.3 함수
wiki_name: sql
parent: sql/03.SQL-기본
order: 3
---

## **1. 함수(Function)**

함수(Function)는 입력된 값에 대해 연산을 수행한 후 그 결과를 반환하는 일련의 코드 집합이다.

내장 함수(Built-in Function)는 크게 **단일행 함수(Single-Row Function)**와 **다중행 함수(Multi-Row Function)**로 구분된다.

| 구분                          | 설명                                                                                                           |
| --------------------------- | ------------------------------------------------------------------------------------------------------------ |
| 단일행 함수(Single-Row Function) | 하나의 행에 대해 연산을 수행한 후 결과를 반환한다. 1:M 조인에서도 M쪽의 각각의 행에 대해 적용된다.                                                  |
| 다중행 함수(Multi-Row Function)  | 여러 행을 대상으로 연산하여 하나의 결과를 반환한다. 집계 함수(COUNT, SUM, AVG), 그룹 함수(ROLLUP, CUBE), 윈도우 함수(RANK, ROW_NUMBER) 등이 해당한다. |

---

## **2. 문자 함수(Character Function)**

문자 함수는 문자열을 대상으로 다양한 연산을 수행하는 함수이다.

---

### **2.1 LOWER**

입력된 문자열을 모두 소문자로 변환하여 반환한다.

#### **문법**

```sql
LOWER(arg)
```

* **arg** : 문자열 값 또는 문자열형 칼럼

#### **예제**

```sql
SELECT LOWER(NAME) AS NAME
FROM MEMBER;
```

---

### **2.2 UPPER**

입력된 문자열을 모두 대문자로 변환하여 반환한다.

#### **문법**

```sql
UPPER(arg)
```

* **arg** : 문자열 값 또는 문자열형 칼럼

#### **예제**

```sql
SELECT UPPER(NAME) AS NAME
FROM MEMBER;
```

---

### **2.3 CHR**

입력된 ASCII 코드값에 해당하는 문자를 반환한다.

#### **문법**

```sql
CHR(arg)
```

* **arg** : ASCII 코드값

> SQL Server에서는 `CHR` 대신 `CHAR` 함수를 사용한다.

#### **예제**

```sql
SELECT CHR(97)
FROM DUAL;
```

---

### **2.4 TRIM**

문자열의 양쪽 끝에서 공백 또는 지정한 문자를 제거하여 반환한다.

#### **문법**

```sql
TRIM([[LEADING | TRAILING | BOTH] 문자 FROM] 문자열)
```

| 인자       | 설명            |
| -------- | ------------- |
| LEADING  | 문자열의 왼쪽에서 제거  |
| TRAILING | 문자열의 오른쪽에서 제거 |
| BOTH     | 양쪽에서 제거(기본값)  |

문자를 지정하지 않으면 공백을 제거한다.

#### **예제 ① : 공백 제거**

```sql
SELECT TRIM('  GOOD ')
FROM DUAL;
```

#### **해설**

1. 문자열의 앞뒤 공백을 제거한다.

---

#### **예제 ② : 왼쪽 문자 제거**

```sql
SELECT TRIM(LEADING '가' FROM '가나다라')
FROM DUAL;
```

#### **해설**

1. 문자열의 왼쪽에서 `'가'`를 제거한다.

---

#### **예제 ③ : 오른쪽 문자 제거**

```sql
SELECT TRIM(TRAILING '가' FROM '가나다라가')
FROM DUAL;
```

#### **해설**

1. 문자열의 오른쪽에서 `'가'`를 제거한다.

---

#### **예제 ④ : 양쪽 문자 제거**

```sql
SELECT TRIM(BOTH '가' FROM '가나다라가')
FROM DUAL;
```

#### **해설**

1. 문자열의 양쪽에서 `'가'`를 제거한다.

---

### **2.5 LTRIM**

문자열의 왼쪽 끝에서 공백 또는 지정한 문자를 제거하여 반환한다.

#### **문법**

```sql
LTRIM(arg1 [, arg2])
```

* **arg1** : 문자열 값 또는 문자열형 칼럼
* **arg2** : 제거할 문자 또는 문자열(생략 시 공백 제거)

> SQL Server에서는 `arg2`를 사용할 수 없으며 공백만 제거할 수 있다.

#### **예제**

```sql
SELECT LTRIM('가나다라', '가')
FROM DUAL;
```

#### **해설**

1. `'가나다라'`의 왼쪽에서 `'가'`를 제거한다.

---

### **2.6 RTRIM**

문자열의 오른쪽 끝에서 공백 또는 지정한 문자를 제거하여 반환한다.

#### **문법**

```sql
RTRIM(arg1 [, arg2])
```

* **arg1** : 문자열 값 또는 문자열형 칼럼
* **arg2** : 제거할 문자 또는 문자열(생략 시 공백 제거)

> SQL Server에서는 `arg2`를 사용할 수 없으며 공백만 제거할 수 있다.

#### **예제**

```sql
SELECT RTRIM('가나다라', '라')
FROM DUAL;
```

#### **해설**

1. `'가나다라'`의 오른쪽에서 `'라'`를 제거한다.

---

### **2.7 SUBSTR**

문자열에서 원하는 부분 문자열을 추출하여 반환한다.

#### **문법**

```sql
SUBSTR(arg1, arg2 [, arg3])
```

| 인자   | 설명                      |
| ---- | ----------------------- |
| arg1 | 문자열 또는 문자열형 칼럼          |
| arg2 | 추출을 시작할 위치(1부터 시작)      |
| arg3 | 추출할 길이(생략 시 문자열 끝까지 추출) |

#### **예제**

```sql
SELECT SUBSTR('GOOD MORNING', 1, 4)
FROM DUAL;
```

#### **해설**

1. `'GOOD MORNING'`의 첫 번째 문자부터 4개의 문자를 추출한다.

---

### **2.8 LENGTH**

문자열의 길이를 반환한다.

#### **문법**

```sql
LENGTH(arg)
```

* **arg** : 문자열 값 또는 문자열형 칼럼

> SQL Server에서는 `LENGTH` 대신 `LEN` 함수를 사용한다.

#### **예제**

```sql
SELECT LENGTH('GOOD MORNING')
FROM DUAL;
```

#### **실행 결과**

```
12
```

> 문자열 사이의 공백도 하나의 문자로 계산된다.

---

### **2.9 REPLACE**

문자열에서 특정 문자열을 다른 문자열로 변경하여 반환한다.

#### **문법**

```sql
REPLACE(arg1, arg2 [, arg3])
```

| 인자   | 설명               |
| ---- | ---------------- |
| arg1 | 문자열 또는 문자열형 칼럼   |
| arg2 | 변경할 대상 문자열       |
| arg3 | 변경될 문자열(생략 시 삭제) |

#### **예제 ① : 문자열 변경**

```sql
SELECT REPLACE('Good Morning', 'Morning', 'Afternoon')
FROM DUAL;
```

#### **해설**

1. `'Morning'`을 `'Afternoon'`으로 변경한다.

---

#### **예제 ② : 문자열 삭제**

```sql
SELECT REPLACE('Good Morning', 'Good ')
FROM DUAL;
```

#### **해설**

1. `'Good '`을 삭제하여 `'Morning'`을 반환한다.

---

## **3. 숫자 함수(Numeric Function)**

숫자 함수는 숫자형 데이터를 대상으로 다양한 연산을 수행하는 함수이다.

---

### **3.1 ABS**

절댓값을 반환한다.

#### **문법**

```sql
ABS(arg)
```

* **arg** : 숫자형 값 또는 숫자형 칼럼

#### **예제**

```sql
SELECT ABS(-2.3)
FROM DUAL;
```

#### **해설**

1. `-2.3`의 절댓값인 `2.3`을 반환한다.

---

### **3.2 MOD**

첫 번째 인자를 두 번째 인자로 나눈 나머지를 반환한다.

#### **문법**

```sql
MOD(arg1, arg2)
```

* **arg1** : 숫자형 값 또는 숫자형 칼럼
* **arg2** : 숫자형 값 또는 숫자형 칼럼

> SQL Server에서는 `MOD()` 함수 대신 `%` 연산자를 사용한다.

#### **예제**

```sql
SELECT MOD(9, 2)
FROM DUAL;
```

#### **해설**

1. `9 ÷ 2`의 나머지인 `1`을 반환한다.

---

### **3.3 ROUND**

수를 반올림하여 반환한다.

#### **문법**

```sql
ROUND(arg1 [, arg2])
```

| 인자   | 설명                 |
| ---- | ------------------ |
| arg1 | 대상 숫자              |
| arg2 | 소수점 이하 자릿수(생략 시 0) |

#### **예제 ①**

```sql
SELECT ROUND(2.67, 1)
FROM DUAL;
```

#### **해설**

1. 소수 둘째 자리에서 반올림하여 `2.7`을 반환한다.

---

#### **예제 ②**

```sql
SELECT ROUND(2.67)
FROM DUAL;
```

#### **해설**

1. 정수로 반올림하여 `3`을 반환한다.

---

### **3.4 TRUNC**

수를 반올림하지 않고 지정한 자릿수까지 남기고 나머지를 버림하여 반환한다.

#### **문법**

```sql
TRUNC(arg1 [, arg2])
```

| 인자   | 설명                     |
| ---- | ---------------------- |
| arg1 | 대상이 되는 숫자형 값 또는 숫자형 칼럼 |
| arg2 | 소수점 이하 자릿수(생략 시 0)     |

#### **예제 ①**

```sql
SELECT TRUNC(2.37, 1)
FROM DUAL;
```

#### **해설**

1. `2.37`을 소수점 첫째 자리까지만 남기고 버림하여 `2.3`을 반환한다.

---

#### **예제 ②**

```sql
SELECT TRUNC(2.37)
FROM DUAL;
```

#### **해설**

1. `2.37`을 정수까지만 남기고 버림하여 `2`를 반환한다.

---

### **3.5 SIGN**

입력된 값이 양수이면 `1`, 음수이면 `-1`, 0이면 `0`을 반환한다.

#### **문법**

```sql
SIGN(arg)
```

* **arg** : 숫자형 값 또는 숫자형 칼럼

#### **예제**

```sql
SELECT SIGN(2.3)
FROM DUAL;
```

#### **해설**

1. `2.3`은 양수이므로 `1`을 반환한다.

---

### **3.6 CEIL**

입력된 값보다 크거나 같은 최소의 정수를 반환한다.

#### **문법**

```sql
CEIL(arg)
```

* **arg** : 숫자형 값 또는 숫자형 칼럼

#### **예제**

```sql
SELECT CEIL(2.3)
FROM DUAL;
```

#### **해설**

1. `2.3` 이상인 최소 정수 `3`을 반환한다.

---

### **3.7 FLOOR**

입력된 값보다 작거나 같은 최대의 정수를 반환한다.

#### **문법**

```sql
FLOOR(arg)
```

* **arg** : 숫자형 값 또는 숫자형 칼럼

#### **예제**

```sql
SELECT FLOOR(2.3)
FROM DUAL;
```

#### **해설**

1. `2.3` 이하인 최대 정수 `2`를 반환한다.

---

### **3.8 기타 숫자 함수**

다음과 같은 숫자 함수도 자주 사용된다.

| 함수    | 설명           |
| ----- | ------------ |
| EXP   | 지수 계산        |
| LOG   | 로그 계산        |
| LN    | 자연로그 계산      |
| POWER | 거듭제곱 계산      |
| SIN   | 사인(Sine)     |
| COS   | 코사인(Cosine)  |
| TAN   | 탄젠트(Tangent) |

---

## **4. 날짜 함수(Date Function)**

날짜 함수는 날짜(Date) 데이터를 처리하는 함수이다.

---

### **4.1 SYSDATE**

현재 날짜와 시간을 반환한다.

#### **문법**

```sql
SYSDATE
```

> SQL Server에서는 `SYSDATE` 대신 `GETDATE()`를 사용하며, 반드시 괄호를 포함해야 한다.

#### **예제**

```sql
SELECT SYSDATE AS TODAY
FROM DUAL;
```

---

### **4.2 EXTRACT**

날짜 데이터에서 연도, 월, 일 등의 값을 추출한다.

#### **문법**

```sql
EXTRACT(항목 FROM 날짜)
```

| 항목     | 설명 |
| ------ | -- |
| YEAR   | 연도 |
| MONTH  | 월  |
| DAY    | 일  |
| HOUR   | 시  |
| MINUTE | 분  |
| SECOND | 초  |

> SQL Server에서는 `EXTRACT` 대신 `DATEPART()` 함수를 사용한다.

#### **예제**

```sql
SELECT
    SYSDATE AS TODAY,
    EXTRACT(MONTH FROM SYSDATE) AS MON,
    EXTRACT(DAY FROM SYSDATE) AS DAY
FROM DUAL;
```

#### **해설**

1. 현재 날짜를 조회한다.
2. 현재 날짜에서 월(MONTH)을 추출한다.
3. 현재 날짜에서 일(DAY)을 추출한다.

---

## **5. 변환 함수(Conversion Function)**

변환 함수는 데이터 타입을 다른 타입으로 변환하는 함수이다.

형변환은 **암시적 형변환**과 **명시적 형변환**으로 구분된다.

| 구분      | 설명                     |
| ------- | ---------------------- |
| 암시적 형변환 | DBMS가 내부적으로 자동 변환한다.   |
| 명시적 형변환 | 사용자가 함수를 이용하여 직접 변환한다. |

> 암시적 형변환은 성능 저하나 오류가 발생할 수 있으므로 명시적 형변환을 사용하는 것이 좋다.

---

### **5.1 TO_NUMBER**

문자열을 숫자형으로 변환한다.

#### **문법**

```sql
TO_NUMBER(arg)
```

* **arg** : 문자열 값 또는 문자열형 칼럼

#### **예제**

```sql
SELECT TO_NUMBER('1001') AS MEMBER_ID
FROM DUAL;
```

---

### **5.2 TO_CHAR**

숫자형 또는 날짜형 데이터를 문자열로 변환한다.

#### **문법**

```sql
TO_CHAR(arg1 [, arg2])
```

| 인자   | 설명             |
| ---- | -------------- |
| arg1 | 숫자형 또는 날짜형 데이터 |
| arg2 | 날짜 포맷(날짜형인 경우) |

#### **예제 ①**

```sql
SELECT TO_CHAR(1001) AS MEMBER_ID
FROM DUAL;
```

#### **예제 ②**

```sql
SELECT TO_CHAR(SYSDATE, 'YYYYMMDD') AS TODAY
FROM DUAL;
```

#### **해설**

1. 현재 날짜를 `YYYYMMDD` 형식의 문자열로 변환한다.

---

### **5.3 TO_DATE**

문자열을 날짜형으로 변환한다.

#### **문법**

```sql
TO_DATE(arg1, arg2)
```

| 인자   | 설명    |
| ---- | ----- |
| arg1 | 문자열   |
| arg2 | 날짜 형식 |

#### **예제**

```sql
SELECT TO_DATE('20240130', 'YYYYMMDD') AS TODAY
FROM DUAL;
```

#### **해설**

1. `'20240130'` 문자열을 `YYYYMMDD` 형식으로 해석하여 날짜형으로 변환한다.

---

## **6. NULL 관련 함수**

NULL 관련 함수는 NULL 값을 다른 값으로 변경하거나 NULL 여부를 판단할 때 사용한다.

---

### **6.1 NVL**

첫 번째 인자가 NULL이 아니면 첫 번째 인자를 반환하고, NULL이면 두 번째 인자를 반환한다.

> 첫 번째 인자와 두 번째 인자의 데이터 타입은 동일해야 한다.

#### **문법**

```sql
NVL(arg1, arg2)
```

* **arg1** : 칼럼 또는 표현식
* **arg2** : NULL일 경우 반환할 값

> SQL Server에서는 `NVL` 대신 `ISNULL` 함수를 사용한다.

#### **예제**

```sql
SELECT EMPNO, ENAME, NVL(COMM, 0) AS COMM
FROM EMP;
```

#### **해설**

1. COMM 칼럼이 NULL이면 `0`으로 변경하여 조회한다.

---

### **6.2 NULLIF**

두 인자의 값이 같으면 NULL을 반환하고, 다르면 첫 번째 인자를 반환한다.

#### **문법**

```sql
NULLIF(arg1, arg2)
```

* **arg1** : 칼럼 또는 표현식
* **arg2** : 비교할 값(동일한 데이터 타입)

#### **예제**

```sql
SELECT EMPNO, ENAME, MGR,
       NULLIF(MGR, 7698) AS NM
FROM EMP;
```

#### **해설**

1. MGR 값이 `7698`이면 NULL을 반환한다.
2. 그렇지 않으면 원래 MGR 값을 반환한다.

---

### **6.3 COALESCE**

입력된 인자를 순서대로 검사하여 **NULL이 아닌 첫 번째 값을 반환**한다.

#### **문법**

```sql
COALESCE(arg1 [, arg2 ...])
```

* **arg1, arg2 ...** : 칼럼 또는 표현식
* 모든 인자는 같은 데이터 타입이어야 한다.

#### **예제**

```sql
SELECT EMPNO,
       COALESCE(HOURLY_WAGE, SALARY, COMMISSION) AS TOTAL_SALARY
FROM WAGES;
```

#### **해설**

1. `HOURLY_WAGE`부터 차례대로 검사한다.
2. NULL이 아니면 해당 값을 반환한다.
3. NULL이면 다음 인자를 계속 검사한다.

---

## **7. CASE**

CASE문은 조건에 따라 서로 다른 값을 반환하는 표현식이다.

---

### **형식 ① : 조건식 사용**

```sql
CASE
    WHEN 칼럼1 = 값1 THEN 값A
    WHEN 칼럼1 = 값2 THEN 값B
    ...
    ELSE 값N
END
```

---

### **형식 ② : 비교 대상 지정**

```sql
CASE 칼럼1
    WHEN 값1 THEN 값A
    WHEN 값2 THEN 값B
    ...
    ELSE 값N
END
```

---

### **예제**

```sql
SELECT ENAME,
       CASE
           WHEN SAL >= 3000 THEN 'HIGH'
           WHEN SAL >= 2000 THEN 'MIDDLE'
           ELSE 'LOW'
       END AS GRADE
FROM EMP;
```

#### **해설**

1. 급여가 3000 이상이면 `HIGH`를 반환한다.
2. 급여가 2000 이상이면 `MIDDLE`을 반환한다.
3. 그 외에는 `LOW`를 반환한다.

---

### **DECODE (Oracle)**

Oracle에서는 `CASE`와 동일한 기능을 하는 `DECODE` 함수를 제공한다.

#### **문법**

```sql
DECODE(칼럼1, 값1, 결과1 [, 값2, 결과2 ...] [, 기본값])
```

---

## **8. 추가 정리**

### **문자 함수**

| 함수      | 설명               |
| ------- | ---------------- |
| LOWER   | 소문자로 변환          |
| UPPER   | 대문자로 변환          |
| CHR     | ASCII 코드를 문자로 변환 |
| TRIM    | 양쪽 공백 또는 문자 제거   |
| LTRIM   | 왼쪽 공백 또는 문자 제거   |
| RTRIM   | 오른쪽 공백 또는 문자 제거  |
| SUBSTR  | 부분 문자열 추출        |
| LENGTH  | 문자열 길이 반환        |
| REPLACE | 문자열 치환           |

---

### **숫자 함수**

| 함수    | 설명    |
| ----- | ----- |
| ABS   | 절댓값   |
| MOD   | 나머지   |
| ROUND | 반올림   |
| TRUNC | 버림    |
| SIGN  | 부호 반환 |
| CEIL  | 올림    |
| FLOOR | 내림    |

---

### **날짜 함수**

| 함수      | 설명         |
| ------- | ---------- |
| SYSDATE | 현재 날짜 및 시간 |
| EXTRACT | 날짜 정보 추출   |

---

### **변환 함수**

| 함수        | 설명        |
| --------- | --------- |
| TO_NUMBER | 숫자형으로 변환  |
| TO_CHAR   | 문자열형으로 변환 |
| TO_DATE   | 날짜형으로 변환  |

---

### **NULL 관련 함수**

| 함수       | 설명                 |
| -------- | ------------------ |
| NVL      | NULL이면 다른 값 반환     |
| NULLIF   | 두 값이 같으면 NULL 반환   |
| COALESCE | NULL이 아닌 첫 번째 값 반환 |

> SQLD에서는 **문자 함수**, **숫자 함수**, **날짜 함수**, **변환 함수**, **NULL 관련 함수**, **CASE와 DECODE의 차이**가 자주 출제된다.
