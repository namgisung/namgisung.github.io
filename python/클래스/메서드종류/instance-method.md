---
layout: wiki
title: 인스턴스 메서드
wiki_name: python
parent: python/클래스/메서드종류
order: 1
---

## **인스턴스 메서드(instance method)**

인스턴스 메서드는 객체를 통해 호출되는 메서드이다.

메서드의 첫 번째 매개변수로 self를 사용한다.

---

### **(1) 기본 구조**

```python
class Person:

    def hello(self):
        print("Hello")
````

hello()는 인스턴스 메서드이다.

---

### **(2) 객체를 통해 호출**

```python
class Person:

    def hello(self):
        print("Hello")

p1 = Person()

p1.hello()
```

결과:

```text
Hello
```

객체이름.메서드() 형식으로 호출한다.

---

### **(3) self 사용**

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

self는 현재 객체를 참조한다.

---

### **(4) 객체마다 다른 동작**

```python 
class Student:

    def __init__(self, name):
        self.name = name

    def hello(self):
        print("Hello", self.name)

s1 = Student("kim")
s2 = Student("lee")

s1.hello()
s2.hello()
```

결과:

```text
Hello kim
Hello lee
```

객체마다 서로 다른 데이터를 사용할 수 있다.

---

### **(5) 인스턴스 메서드의 특징**

* 객체를 통해 호출한다.
* 첫 번째 매개변수로 self를 사용한다.
* 인스턴스 변수에 접근 가능하다.
