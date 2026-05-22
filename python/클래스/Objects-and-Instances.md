---
layout: wiki
title: 객체와 인스턴스
wiki_name: python
parent: python/클래스
order: 2
---

## **객체(object)와 인스턴스(instance)**

클래스로 생성된 실제 데이터를 객체(object) 또는 인스턴스(instance)라고 한다.

---

### **(1) 객체 생성**

```python
class Person:
    pass

p1 = Person()
````

Person 클래스로 객체를 생성하였다.

---

### **(2) 객체(object)**

객체는 클래스에 의해 생성된 실제 데이터를 의미한다.

```python
p1 = Person()
```

여기서 p1은 객체이다.

---

### **(3) 인스턴스(instance)**

인스턴스는 특정 클래스에 의해 생성된 객체를 의미한다.

```python
p1 = Person()
```

p1은 Person 클래스의 인스턴스이다.

---

### **(4) 객체와 인스턴스의 차이**

* 객체(object) : 생성된 모든 실제 데이터
* 인스턴스(instance) : 어떤 클래스에 의해 생성되었는지 강조한 표현

즉,

```python
p1 = Person()
```

* p1은 객체이다.
* p1은 Person 클래스의 인스턴스이다.

---

### **(5) 객체 참조**

변수는 객체의 주소(참조값)를 저장한다.

```python
p1 = Person()
p2 = p1
```

p1과 p2는 같은 객체를 참조한다.

---

### **(6) is 연산자**

is 연산자는 두 변수가 같은 객체를 참조하는지 확인한다.

```python
p1 = Person()
p2 = p1

print(p1 is p2)
```

결과:

```text
True
```
