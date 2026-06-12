---
layout: wiki
title: map()
wiki_name: python
parent: python/람다함수
order: 2
---

## **map()**

map()은 반복 가능한 객체의 각 요소에 함수를 적용하는 함수이다.

모든 요소에 동일한 작업을 수행할 때 사용한다.

---

### **(1) 기본 구조**

```python
map(함수, 반복가능객체)
```

- 함수 : 각 요소에 적용할 함수
- 반복가능객체 : 리스트, 튜플 등의 반복 가능한 객체

map()은 map 객체를 반환한다.

---

### **(2) 일반 함수 사용**

```python
def square(x):
    return x * x

numbers = [1, 2, 3, 4]

result = map(square, numbers)

print(list(result))
```

결과:

```python
[1, 4, 9, 16]
```

각 요소에 square() 함수가 적용된다.

---

### **(3) 람다 함수 사용**

```python
numbers = [1, 2, 3, 4]

result = map(
    lambda x: x * 2,
    numbers
)

print(list(result))
```

결과:

```python
[2, 4, 6, 8]
```

람다 함수와 함께 자주 사용된다.

---

### **(4) 문자열 변환**

```python
numbers = ["1", "2", "3", "4"]

result = map(int, numbers)

print(list(result))
```

결과:

```python
[1, 2, 3, 4]
```

문자열을 정수로 변환할 수 있다.

---

### **(5) 여러 반복가능객체 사용**

```python
a = [1, 2, 3]
b = [10, 20, 30]

result = map(
    lambda x, y: x + y,
    a,
    b
)

print(list(result))
```

결과:

```python
[11, 22, 33]
```

여러 객체의 요소를 동시에 사용할 수 있다.

---

### **(6) map 객체**

```python
numbers = [1, 2, 3]

result = map(
    lambda x: x * 2,
    numbers
)

print(result)
```

결과:

```python
<map object at 0x...>
```

map()은 map 객체를 반환하므로 list() 등을 사용하여 확인한다.

---

### **(7) map()의 동작**

```python
numbers = [1, 2, 3]
```

```python
map(
    lambda x: x * 2,
    numbers
)
```

동작 결과

```python
[
    1 * 2,
    2 * 2,
    3 * 2
]
```

↓

```python
[2, 4, 6]
```

---

## 정리

- map()은 각 요소에 함수를 적용한다.
- map 객체를 반환한다.
- list()로 결과를 확인할 수 있다.
- 람다 함수와 자주 사용된다.
- 여러 반복가능객체를 사용할 수 있다.
