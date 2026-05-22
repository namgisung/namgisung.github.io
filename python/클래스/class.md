---
layout: wiki
title: 클레스
wiki_name: python
parent: python/클래스
order: 1
---


## **클래스(class)란?**

클래스는 데이터와 함수를 하나로 묶는 사용자 정의 자료형이다.

객체를 생성하기 위한 설계도(틀) 역할을 한다.

---

### **(1) 클래스 정의**

```python
class Person:
    pass
````

class 키워드를 사용하여 클래스를 정의한다.

pass는 내용이 없음을 의미한다.

---

### **(2) 객체 생성**

```python
class Person:
    pass

p1 = Person()
```

Person 클래스의 객체(인스턴스)를 생성한다.

---

### **(3) 클래스와 객체**

* 클래스(class) : 객체를 만들기 위한 설계도
* 객체(object) : 클래스로 생성된 실제 데이터

예시:

* 클래스 → 붕어빵 틀
* 객체 → 실제 붕어빵

---

### **(4) 클래스의 구성 요소**

클래스는 변수와 함수를 가질 수 있다.

```python
class Person:

    def __init__(self, name):
        self.name = name

    def hello(self):
        print("Hello")
```

* 변수 -> 필드(field)
* 함수 -> 메서드(method)

---

### **(5) 객체 사용**

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

객체이름.메서드() 형식으로 사용한다.
