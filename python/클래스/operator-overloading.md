---
layout: wiki
title: 연산자 오버로딩
wiki_name: python
parent: python/클래스
order: 13
---

## **연산자 오버로딩(Operator Overloading)**

연산자 오버로딩은 연산자의 동작을 객체에 맞게 재정의하는 것이다.

파이썬에서는 특수 메서드(Special Method)를 이용하여 연산자의 동작을 정의할 수 있다.

---

### **(1) 왜 사용하는가?**

기본적으로 연산자는 숫자와 같은 기본 자료형에 사용된다.

```python
print(10 + 20)
```

결과:

```text
30
```

하지만 사용자 정의 클래스에도 연산자를 사용할 수 있도록 만들 수 있다.

---

### **(2) __add__()**

`+` 연산자를 재정의한다.

```python
class Point:

    def __init__(self, x):
        self.x = x

    def __add__(self, other):
        return Point(self.x + other.x)

p1 = Point(10)
p2 = Point(20)

p3 = p1 + p2

print(p3.x)
```

결과:

```text
30
```

실제로는 다음과 같이 동작한다.

```python
p1.__add__(p2)
```

---

### **(3) __sub__()**

`-` 연산자가 수행될 때 호출되는 특수 메서드이다.

```python
class Number:

    def __init__(self, value):
        self.value = value

    def __sub__(self, other):
        return Number(self.value - other.value)

n1 = Number(20)
n2 = Number(5)

print((n1 - n2).value)
```

결과:

```text
15
```

---

### **(4) __mul__()**

`*` 연산자를 재정의한다.

```python
class Number:

    def __init__(self, value):
        self.value = value

    def __mul__(self, other):
        return Number(self.value * other.value)

n1 = Number(10)
n2 = Number(3)

print((n1 * n2).value)
```

결과:

```text
30
```

---

### **(5) __gt__()**

`>` 연산자를 재정의한다.

```python
class Student:

    def __init__(self, score):
        self.score = score

    def __gt__(self, other):
        return self.score > other.score

s1 = Student(90)
s2 = Student(80)

print(s1 > s2)
```

결과:

```text
True
```

---

### **(6) __eq__()**

`==` 연산자를 재정의한다.

```python
class Student:

    def __init__(self, score):
        self.score = score

    def __eq__(self, other):
        return self.score == other.score

s1 = Student(90)
s2 = Student(90)

print(s1 == s2)
```

결과:

```text
True
```

---

### **(7) 자주 사용하는 연산자**

| 연산자 | 특수 메서드 |
|----------|----------|
| + | __add__() |
| - | __sub__() |
| * | __mul__() |
| / | __truediv__() |
| // | __floordiv__() |
| % | __mod__() |
| ** | __pow__() |
| > | __gt__() |
| < | __lt__() |
| >= | __ge__() |
| <= | __le__() |
| == | __eq__() |

---

### 정리

- 연산자 오버로딩은 연산자의 동작을 재정의하는 것이다.
- 특수 메서드를 사용하여 구현한다.
- 사용자 정의 객체에도 연산자를 사용할 수 있다.
- `+`, `-`, `*`, `==`, `>` 등의 연산자를 재정의할 수 있다.
