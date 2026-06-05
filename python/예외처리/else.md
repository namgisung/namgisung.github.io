---
layout: wiki
title: else
wiki_name: python
parent: python/예외처리
order: 4
---

## **else**

else는 try 블록에서 예외가 발생하지 않았을 때 실행되는 블록이다.

except 블록 다음에 작성한다.

---

### **(1) 기본 구조**

```python
try:
    실행문

except 예외:
    예외 처리

else:
    실행문
```

- 예외 발생 $\to$ except 실행
- 예외 없음 $\to$ else 실행

---

### **(2) 예외가 없는 경우**

```python
try:
    print(10 / 2)

except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")

else:
    print("정상 실행")
```

결과:

```text
5.0
정상 실행
```

try 블록에서 예외가 발생하지 않았으므로 else가 실행된다.

---

### **(3) 예외가 발생한 경우**

```python
try:
    print(10 / 0)

except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")

else:
    print("정상 실행")
```

결과:

```text
0으로 나눌 수 없습니다.
```

예외가 발생했으므로 else는 실행되지 않는다.

---

### **(4) 실행 순서**

```python
try:
    실행문

except:
    예외 처리

else:
    실행문
```

동작 순서

```text
예외 발생
try → except

예외 없음
try → else
```

---

### **(5) else를 사용하는 이유**

```python
try:
    number = int(input())

except ValueError:
    print("숫자를 입력하세요.")

else:
    print("입력한 숫자:", number)
```

정상 실행 시 수행할 코드를 구분하여 작성할 수 있다.

---

### 정리

- else는 예외가 발생하지 않았을 때 실행된다.
- except 뒤에 작성한다.
- 예외가 발생하면 실행되지 않는다.
- 정상 실행 코드를 분리할 때 사용한다.
