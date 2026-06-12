---
layout: wiki
title: 특수 메서드
wiki_name: python
parent: python/클래스
order: 10
---

## **특수 메서드(special method)**

특수 메서드는 특정 상황에서 자동으로 호출되는 메서드이다.

메서드 이름 앞뒤에 __ 를 사용한다.

이를 magic method 또는 dunder method라고도 한다.

---

### **(1) \_\_init\_\_()**

객체 생성 시 자동 호출되는 생성자 메서드이다.

```python
class Person:

    def __init__(self):
        print("생성자 호출")
````

---

### **(2) \_\_str\_\_()**

객체를 문자열로 출력할 때 자동 호출된다.

```python
class Person:

    def __str__(self):
        return "Person class"

p1 = Person()

print(p1)
```

결과:

```text
Person class
```

---

### **(3) \_\_len\_\_()**

len() 함수 사용 시 자동 호출된다.

```python
class MyData:

    def __len__(self):
        return 5

d = MyData()

print(len(d))
```

결과:

```text
5
```

---

### **(4) 연산자 관련 특수 메서드**

| 특수 메서드         | 연산자        | 의미        |
| -------------- | ---------- | --------- |
| `__add__`      | `+`        | 덧셈        |
| `__sub__`      | `-`        | 뺄셈        |
| `__mul__`      | `*`        | 곱셈        |
| `__truediv__`  | `/`        | 나눗셈       |
| `__floordiv__` | `//`       | 몫         |
| `__mod__`      | `%`        | 나머지       |
| `__divmod__`   | `divmod()` | 몫과 나머지    |
| `__pow__`      | `**`       | 거듭제곱      |
| `__lshift__`   | `<<`       | 비트 왼쪽 이동  |
| `__rshift__`   | `>>`       | 비트 오른쪽 이동 |
| `__le__`       | `<=`       | 작거나 같다    |
| `__lt__`       | `<`        | 작다        |
| `__ge__`       | `>=`       | 크거나 같다    |
| `__gt__`       | `>`        | 크다        |
| `__eq__`       | `==`       | 같다        |
| `__ne__`       | `!=`       | 같지 않다     |

---

#### **사용 예시**

```python
class Number:

    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value

n1 = Number(10)
n2 = Number(20)

print(n1 + n2)
```

결과:

```text
30
```

* 연산 시 **add**() 메서드가 자동 호출된다.
