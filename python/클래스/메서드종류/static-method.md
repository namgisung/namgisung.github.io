---
layout: wiki
title: 정적 메서드
wiki_name: python
parent: python/클래스/메서드종류
order: 3
---

## **정적 메서드(static method)**

정적 메서드는 클래스와 객체에 독립적으로 동작하는 메서드이다.

@staticmethod 데코레이터를 사용한다.

self와 cls를 사용하지 않는다.

---

### **(1) 기본 구조**

```python
class Person:

    @staticmethod
    def hello():
        print("Hello")
```

hello()는 정적 메서드이다.

---

### **(2) 클래스 이름으로 호출**

```python
class Person:

    @staticmethod
    def hello():
        print("Hello")

Person.hello()
```

결과:

```text
Hello
```

클래스이름.메서드() 형식으로 호출한다.

---

### **(3) 객체로도 호출 가능**

```python
class Person:

    @staticmethod
    def hello():
        print("Hello")

p1 = Person()

p1.hello()
```

결과:

```text 
Hello
```

객체를 통해서도 호출 가능하다.

---

### **(4) self와 cls 사용 불가**

```python
class Person:

    @staticmethod
    def test():
        print("static method")
```

정적 메서드는 객체 정보(self)와 클래스 정보(cls)를 사용하지 않는다.

---

### **(5) 정적 메서드의 특징**

* @staticmethod를 사용한다.
* self와 cls를 사용하지 않는다.
* 클래스와 관련된 일반 기능을 작성할 때 사용한다.
* 객체 상태와 독립적으로 동작한다.
