---
layout: wiki
title: except
wiki_name: python
parent: python/예외처리
order: 3
---

## **except**

except는 try 블록에서 발생한 예외를 처리하는 블록이다.

예외가 발생하면 프로그램이 종료되지 않고 except 블록이 실행된다.

---

### **(1) 기본 구조**

```python
try:
    실행문

except:
    예외 처리 코드
```

try 블록에서 예외가 발생하면 except 블록이 실행된다.

---

### **(2) 예외 처리**

```python
try:
    print(10 / 0)

except:
    print("오류 발생")
```

결과:

```text
오류 발생
```

예외가 발생했기 때문에 except 블록이 실행된다.

---

### **(3) 특정 예외 처리**

```python
try:
    print(10 / 0)

except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
```

결과:

```text
0으로 나눌 수 없습니다.
```

특정 예외만 처리할 수 있다.

---

### **(4) 여러 예외 처리**

```python
try:
    number = int(input())

    print(100 / number)

except ValueError:
    print("숫자를 입력하세요.")

except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
```

입력값에 따라 서로 다른 예외를 처리할 수 있다.

---

### **(5) 예외 객체 사용**

```python
try:
    print(10 / 0)

except ZeroDivisionError as e:
    print(e)
```

결과:

```text
division by zero
```

발생한 예외 정보를 변수로 받을 수 있다.

---

### **(6) except의 역할**

```python
except:
    예외 처리 코드
```

- 예외 발생 시 실행된다.
- 프로그램의 비정상 종료를 방지한다.
- 발생한 예외를 처리할 수 있다.

---

### 정리

- except는 발생한 예외를 처리하는 블록이다.
- try와 함께 사용한다.
- 특정 예외만 처리할 수 있다.
- as를 사용하여 예외 객체를 받을 수 있다.
