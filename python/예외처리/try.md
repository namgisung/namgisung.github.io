---
layout: wiki
title: try
wiki_name: python
parent: python/예외처리
order: 2
---

## **try**

try는 예외가 발생할 수 있는 코드를 작성하는 블록이다.

예외가 발생하면 프로그램이 중단되지 않고 해당 예외를 처리할 수 있다.

---

### **(1) 기본 구조**

```python
try:
    실행문
```

try 블록 안에는 예외가 발생할 가능성이 있는 코드를 작성한다.

---

### **(2) 예외 발생 예시**

```python
try:
    print(10 / 0)
```

결과:

```text
ZeroDivisionError: division by zero
```

0으로 나누는 과정에서 예외가 발생한다.

---

### **(3) try와 except**

try는 일반적으로 except와 함께 사용한다.

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

예외가 발생하면 except 블록으로 이동한다.

---

### **(4) 여러 문장 작성**

```python
try:
    print("start")

    number = int(input())

    print(100 / number)

    print("end")
```

try 블록 안에는 여러 개의 문장을 작성할 수 있다.

---

### **(5) try의 역할**

```python
try:
    실행문
```

- 예외가 발생할 수 있는 코드를 작성한다.
- 예외가 발생하면 프로그램이 즉시 종료되지 않는다.
- 발생한 예외는 except에서 처리할 수 있다.

---

### 정리

- try는 예외 발생 가능성이 있는 코드를 작성하는 블록이다.
- try만 단독으로 사용하지 않고 보통 except와 함께 사용한다.
- 예외가 발생하면 해당 예외를 처리할 수 있다.
