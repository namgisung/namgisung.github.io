---
layout: wiki
title: 접근 제한자
wiki_name: python
parent: python/클래스
order: 9
---



## **접근 제한자(access modifier)**

접근 제한자는 클래스 내부 변수와 메서드의 접근 범위를 제한하는 기능이다.

파이썬은 다른 언어처럼 완전한 접근 제한자를 제공하지 않지만 naming 규칙을 사용한다.

---

### **(1) public**

public은 어디서든 접근 가능한 변수와 메서드이다.

```python
class Person:

    def __init__(self):
        self.name = "kim"
```

self.name은 public 변수이다.

---

#### **public 사용**

```python
class Person:

    def __init__(self):
        self.name = "kim"

p1 = Person()

print(p1.name)
```

결과:

```text
kim
```

---

### **(2) protected**

protected는 클래스 내부와 상속 관계에서 사용하는 것을 권장하는 변수이다.

변수 이름 앞에 _를 사용한다.

```python
class Person:

    def __init__(self):
        self._age = 20
```

_age는 protected 변수이다.

---

#### **protected 사용**

```python 
class Person:

    def __init__(self):
        self._age = 20

p1 = Person()

print(p1._age)
```

결과:

```text
20
```

파이썬에서는 접근 가능하지만 내부 사용을 권장한다.

---

### **(3) private**

private는 클래스 내부에서만 사용하도록 만든 변수이다.

변수 이름 앞에 __를 사용한다.

```python
class Person:

    def __init__(self):
        self.__score = 100
```

__score는 private 변수이다.

---

#### **private 사용**

```python
class Person:

    def __init__(self):
        self.__score = 100

p1 = Person()

# print(p1.__score)
```

직접 접근 시 오류가 발생한다.

---

### **(4) private 변수 접근**

private 변수는 내부적으로 이름이 변경(name mangling)된다.

```python 
class Person:

    def __init__(self):
        self.__score = 100

p1 = Person()

print(p1._Person__score)
```

결과:

```text
100
```

---

### **(5) 접근 제한자 정리**

| 형태     | 의미           |
| ------ | ------------ |
| public | 자유롭게 접근 가능   |
| _변수    | protected 의미 |
| __변수   | private 의미   |

```
```
