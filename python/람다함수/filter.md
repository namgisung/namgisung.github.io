---
layout: wiki
title: filter()
wiki_name: python
parent: python/람다함수
order: 3
---


## **filter()**

filter()는 반복 가능한 객체의 각 요소 중 조건에 맞는(True인) 요소만 걸러내는 함수이다.

특정 조건에 부합하는 데이터만 추출할 때 사용한다.

---

### **(1) 기본 구조**

```python
filter(함수, 반복가능객체)

```

* 함수 : 각 요소를 검사하여 True 또는 False를 반환하는 함수
* 반복가능객체 : 리스트, 튜플 등의 반복 가능한 객체

filter()는 filter 객체를 반환한다.

---

### **(2) 일반 함수 사용**

```python
def is_even(x):
    return x % 2 == 0

numbers = [1, 2, 3, 4, 5, 6]

result = filter(is_even, numbers)

print(list(result))

```

결과:

```python
[2, 4, 6]

```

is_even() 함수가 True를 반환하는 짝수만 걸러진다.

---

### **(3) 람다 함수 사용**

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(
    lambda x: x > 3,
    numbers
)

print(list(result))

```

결과:

```python
[4, 5, 6]

```

람다 함수와 함께 사용하여 조건을 간결하게 표현할 수 있다.

---

### **(4) None 사용 (참인 요소만 남기기)**

```python
data = [0, 1, False, True, "", "Hello"]

result = filter(None, data)

print(list(result))

```

결과:

```python
[1, True, 'Hello']

```

함수 자리에 None을 넣으면 조건문에서 False로 취급되는 값(0, False, 빈 문자열 등)을 모두 제거한다.

---

### **(5) filter 객체**

```python
numbers = [1, 2, 3]

result = filter(
    lambda x: x > 1,
    numbers
)

print(result)

```

결과:

```python
<filter object at 0x...>

```

filter()는 filter 객체를 반환하므로 list() 등을 사용하여 확인한다.

---

### **(6) filter()의 동작**

```python
numbers = [1, 2, 3, 4]

```

```python
filter(
    lambda x: x % 2 == 0,
    numbers
)

```

동작 결과

```python
[
    1 -> False (탈락),
    2 -> True (생존),
    3 -> False (탈락),
    4 -> True (생존)
]

```

↓

```python
[2, 4]

```

---

### 정리

- filter()는 조건이 True인 요소만 골라낸다.
- filter 객체를 반환한다.
- list()로 결과를 확인할 수 있다.
- 람다 함수와 자주 사용된다.
- 함수 자리에 None을 쓰면 참(True)인 값만 남긴다.
