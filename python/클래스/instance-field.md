---
layout: wiki
title: 인스턴스 field
wiki_name: python
parent: python/클래스
order: 5
---

## **인스턴스 필드(instance field)**

인스턴스 필드는 객체마다 개별적으로 가지는 변수이다.

주로 `self.변수이름` 형태로 생성한다.

---

### **(1) 기본 구조**

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.age = age
````

* self.name
* self.age

는 인스턴스 필드이다.

---

### **(2) 객체마다 다른 값 저장**

```python
class Person:

    def __init__(self, name):
        self.name = name

p1 = Person("kim")
p2 = Person("lee")

print(p1.name)
print(p2.name)
```

결과:

```text
kim
lee
```

각 객체는 서로 다른 데이터를 가진다.

---

### **(3) 인스턴스 필드 접근**

객체이름.필드이름 형식으로 접근한다.

```python
class Student:

    def __init__(self, score):
        self.score = score

s1 = Student(100)

print(s1.score)
```

결과:

```text
100
```

---

### **(4) 인스턴스 필드 추가**

생성자 외부에서도 인스턴스 필드를 추가할 수 있다.

```python
class Person:
    pass

p1 = Person()

p1.name = "kim"

print(p1.name)
```

결과:

```text
kim
```

---

### **(5) 인스턴스 필드의 특징**

* 객체마다 독립적으로 존재한다.
* self를 사용하여 생성한다.
* 객체별로 다른 값을 저장할 수 있다.

