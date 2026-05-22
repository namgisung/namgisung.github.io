---
layout: wiki
title: 클래스 메서드
wiki_name: python
parent: python/클래스/메서드종류
order: 2
---


## **클래스 메서드(class method)**

클래스 메서드는 클래스를 대상으로 동작하는 메서드이다.

@classmethod 데코레이터를 사용한다.

첫 번째 매개변수로 cls를 사용한다.

---

### **(1) 기본 구조**

```python
class Person:

    @classmethod
    def hello(cls):
        print("Hello")
````

hello()는 클래스 메서드이다.

---

### **(2) 클래스 이름으로 호출**

```python
class Person:

    @classmethod
    def hello(cls):
        print("Hello")

Person.hello()
```

결과:

```text
Hello
```

클래스이름.메서드() 형식으로 호출한다.

---

### **(3) cls 사용**

cls는 현재 클래스를 참조한다.

```python
class Student:

    school = "ABC"

    @classmethod
    def show(cls):
        print(cls.school)

Student.show()
```

결과:

```text
ABC
```

---

### **(4) 객체로도 호출 가능**

```python 
class Person:

    @classmethod
    def hello(cls):
        print("Hello")

p1 = Person()

p1.hello()
```

결과:

```text
Hello
```

보통은 클래스 이름으로 호출한다.

---

### **(5) 클래스 메서드의 특징**

* @classmethod를 사용한다.
* 첫 번째 매개변수로 cls를 사용한다.
* 클래스 변수에 접근 가능하다.
* 클래스 전체와 관련된 동작을 수행한다.
