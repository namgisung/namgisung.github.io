---
layout: wiki
title: 반환 값
wiki_name: python
parent: python/함수
order: 4
---


## **반환값 (return)**

함수는 `return`을 사용하여 결과를 반환할 수 있다.
`return`을 만나면 함수는 즉시 종료되고, 값을 호출한 곳으로 돌려준다.

---

### **(1) 기본 구조**

```python id="k9dp96"
def 함수이름():
    return 값
```

---

### **(2) 기본 예제**

```python id="2dkt5z"
def add(a, b):
    return a + b

result = add(2, 3)
print(result)
```

위의 코드에서 `add` 함수는 두 수의 합을 계산하여 반환한다.

---

### **(3) return의 특징**

`return`이 실행되면 함수는 즉시 종료된다.

```python id="v1c4lr"
def func():
    return 1
    print("Hello")  # 실행되지 않음
```

---

### **(4) 여러 값 반환**

파이썬에서는 여러 값을 동시에 반환할 수 있다.
이 경우 반환값은 튜플(tuple) 형태로 처리된다.

```python id="8h5qfd"
def func():
    return 1, 2, 3

result = func()
print(result)
```

출력:

```text id="z8l5k1"
(1, 2, 3)
```

---

### **(5) 반환값 나누기 (언패킹)**

반환된 여러 값을 각각의 변수로 나눌 수 있다.

```python id="d44h3m"
def func():
    return 1, 2

a, b = func()

print(a)  # 1
print(b)  # 2
```
