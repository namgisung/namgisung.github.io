---
layout: wiki
title: self와 객체참조
wiki_name: python
parent: python/클래스
order: 4
---

## **self와 객체참조**

self는 현재 객체 자신을 참조하는 변수이다.

클래스 내부에서 인스턴스 필드와 메서드에 접근할 때 사용한다.

---

### **(1) self의 기본 구조**

```python
class Person:

    def hello(self):
        print("Hello")
````

메서드의 첫 번째 매개변수로 self를 사용한다.

---

### **(2) self는 현재 객체를 의미**

```python
class Person:

    def show(self):
        print(self)

p1 = Person()

p1.show()
```

결과:

```text
<__main__.Person object at 0x000001>
```

self는 현재 객체의 주소(참조값)를 가진다.

---

### **(3) 인스턴스 필드 접근**

```python
class Person:

    def __init__(self, name):
        self.name = name

    def show(self):
        print(self.name)

p1 = Person("kim")

p1.show()
```

결과:

```text
kim
```

self.name 형태로 인스턴스 필드에 접근한다.

---

### **(4) 객체참조**

변수는 객체 자체를 저장하는 것이 아니라 객체의 참조값(주소)을 저장한다.

```python
class Person:
    pass

p1 = Person()
p2 = p1

print(p1 is p2)
```

결과:

```text
True
```

p1과 p2는 같은 객체를 참조한다.

---

### **(5) self를 사용하는 이유**

객체마다 서로 다른 데이터를 저장하기 위해 사용한다.

```python
class Student:

    def __init__(self, name):
        self.name = name

s1 = Student("kim")
s2 = Student("lee")

print(s1.name)
print(s2.name)
```

결과:

```text
kim
lee
```

각 객체는 독립적인 데이터를 가진다.
