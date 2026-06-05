---
layout: wiki
title: raise
wiki_name: python
parent: python/예외처리
order: 6
---

## **raise**

raise는 예외를 직접 발생시키는 키워드이다.

프로그램에서 특정 조건이 잘못되었을 때 의도적으로 예외를 발생시킬 수 있다.

---

### **(1) 기본 구조**

```python
raise 예외객체
```

또는

```python
raise 예외클래스("오류 메시지")
```

---

### **(2) ValueError 발생**

```python
raise ValueError("잘못된 값입니다.")
```

결과:

```text
ValueError: 잘못된 값입니다.
```

raise를 사용하여 직접 예외를 발생시킨다.

---

### **(3) 조건 검사**

```python
age = -1

if age < 0:
    raise ValueError("나이는 음수일 수 없습니다.")
```

결과:

```text
ValueError: 나이는 음수일 수 없습니다.
```

잘못된 입력값을 검사할 때 자주 사용한다.

---

### **(4) 함수에서 사용**

```python
def divide(a, b):

    if b == 0:
        raise ZeroDivisionError(
            "0으로 나눌 수 없습니다."
        )

    return a / b
```

예외가 발생할 조건을 직접 정의할 수 있다.

---

### **(5) try-except와 함께 사용**

```python
try:

    age = -1

    if age < 0:
        raise ValueError(
            "나이는 음수일 수 없습니다."
        )

except ValueError as e:
    print(e)
```

결과:

```text
나이는 음수일 수 없습니다.
```

raise로 발생시킨 예외도 except로 처리할 수 있다.

---

### **(6) raise를 사용하는 이유**

```python
if score < 0:
    raise ValueError("점수는 음수가 될 수 없습니다.")
```

- 잘못된 데이터 방지
- 함수의 입력값 검증
- 오류 원인 명확화
- 프로그램 안정성 향상

---

### 정리

- raise는 예외를 직접 발생시키는 키워드이다.
- 조건에 따라 예외를 발생시킬 수 있다.
- ValueError, TypeError 등 다양한 예외를 발생시킬 수 있다.
- try-except와 함께 사용할 수 있다.
