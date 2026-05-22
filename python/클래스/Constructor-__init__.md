---
layout: wiki
title: 생성자 __init__
wiki_name: python
parent: python/클래스
order: 3
---

## **생성자 __init__**

생성자(constructor)는 객체가 생성될 때 자동으로 호출되는 특수 메서드이다.

파이썬에서는 `__init__()` 메서드를 사용한다.

---

### **(1) 기본 구조**

```python
class Person:

    def __init__(self):
        print("객체 생성")
````

객체를 생성하면 `__init__()`이 자동 호출된다.

---

### **(2) 객체 생성**

```python
class Person:

    def __init__(self):
        print("객체 생성")

p1 = Person()
```

결과:

```text
객체 생성
```

---

### **(3) 매개변수 사용**

생성자는 객체 생성 시 값을 전달받을 수 있다.

```python
class Person:

    def __init__(self, name):
        self.name = name

p1 = Person("kim")

print(p1.name)
```

결과:

```text
kim
```

---

### **(4) 인스턴스 필드 초기화**

생성자는 주로 인스턴스 필드를 초기화하는 역할을 한다.

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

* self.name
* self.age

는 인스턴스 필드이다.

---

### **(5) 생성자의 특징**

* 객체 생성 시 자동 호출된다.
* 객체 초기화를 담당한다.
* 클래스당 하나의 `__init__()` 메서드를 가진다.

```
```
