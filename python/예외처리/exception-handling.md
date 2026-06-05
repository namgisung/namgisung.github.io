---
layout: wiki
title: exception handling
wiki_name: python
parent: python/예외처리
order: 1
---


## **예외 처리(Exception Handling)란?**

예외 처리(Exception Handling)는 프로그램 실행 중 발생할 수 있는 오류를 처리하는 기능이다.

예외가 발생하면 프로그램이 비정상적으로 종료될 수 있으므로 적절한 처리가 필요하다.

---

### **(1) 예외(Exception)란?**

예외(Exception)는 프로그램 실행 중 발생하는 오류를 의미한다.

예시:

```python
print(10 / 0)
````

결과:

```text
ZeroDivisionError: division by zero
```

0으로 나누었기 때문에 예외가 발생한다.

---

### **(2) 예외가 발생하면**

```python
print("start")

print(10 / 0)

print("end")
```

결과:

```text
start

ZeroDivisionError: division by zero
```

예외가 발생한 이후 코드는 실행되지 않는다.

---

### **(3) 대표적인 예외**

###3 ZeroDivisionError

```python
10 / 0
```

0으로 나눌 때 발생한다.

---

#### ValueError

```python
int("hello")
```

잘못된 형식의 값을 변환할 때 발생한다.

---

#### IndexError

```python
data = [1, 2, 3]

print(data[5])
```

존재하지 않는 인덱스에 접근할 때 발생한다.

---

#### KeyError

```python
student = {"name": "kim"}

print(student["age"])
```

존재하지 않는 키에 접근할 때 발생한다.

---

#### FileNotFoundError

```python
f = open("test.txt", "r")
```

존재하지 않는 파일을 열 때 발생한다.

---

### **(4) 예외 처리의 필요성**

예외를 처리하지 않으면 프로그램이 비정상적으로 종료될 수 있다.

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

프로그램이 종료되지 않고 계속 실행될 수 있다.

---

### 정리

* 예외(Exception)는 실행 중 발생하는 오류이다.
* 예외가 발생하면 프로그램이 중단될 수 있다.
* 예외 처리를 통해 오류를 안전하게 처리할 수 있다.
* 예외 처리는 try, except 등을 사용한다.
