---
layout: wiki
title: 상속
wiki_name: python
parent: python/상속
order: 1
---

## **상속(Inheritance)이란?**

상속(Inheritance)은 기존 클래스의 속성과 메서드를 물려받아 새로운 클래스를 만드는 기능이다.

상속을 사용하면 기존 코드를 재사용할 수 있으며, 클래스 간의 계층 구조를 만들 수 있다.

---

### **(1) 기본 구조**

```python
class 부모클래스:
    pass

class 자식클래스(부모클래스):
    pass
```

자식 클래스는 부모 클래스의 필드와 메서드를 상속받는다.

---

### **(2) 상속 예제**

```python
class Person:

    def greet(self):
        print("안녕하세요.")

class Student(Person):
    pass

student = Student()

student.greet()
```

결과:

```text
안녕하세요.
```

Student 클래스에 greet()가 없지만 부모 클래스인 Person의 메서드를 사용할 수 있다.

---

### **(3) 부모 클래스와 자식 클래스**

```python
class Person:
    pass

class Student(Person):
    pass
```

- Person → 부모 클래스(Super Class, Base Class)
- Student → 자식 클래스(Sub Class, Derived Class)

---

### **(4) Is-A 관계**

상속은 Is-A 관계를 표현한다.

```python
class Person:
    pass

class Soldier(Person):
    pass
```

```text
Soldier is a Person
군인은 사람이다.
```

상속 관계가 성립한다.

---

### **(5) Has-A 관계**

상속이 아닌 포함 관계를 Has-A 관계라고 한다.

```python
class Engine:
    pass

class Car:

    def __init__(self):
        self.engine = Engine()
```

```text
Car has a Engine
자동차는 엔진을 가진다.
```

상속이 아니라 객체를 필드로 포함한 관계이다.

---

### **(6) 상속의 장점**

#### 코드 재사용

```python
class Person:

    def greet(self):
        print("안녕하세요.")

class Student(Person):
    pass
```

부모 클래스의 코드를 그대로 사용할 수 있다.

### 유지보수 용이

공통 기능을 부모 클래스에 작성하면 여러 자식 클래스가 사용할 수 있다.

### 계층 구조 표현

```text
Person
├── Student
├── Soldier
└── Teacher
```

현실 세계의 관계를 표현하기 쉽다.

---

### **(7) 상속받은 내용**

```python
class Person:

    def __init__(self):
        self.name = "Kim"

    def greet(self):
        print("안녕하세요.")

class Student(Person):
    pass
```

Student는 다음을 모두 사용할 수 있다.

```python
student = Student()

print(student.name)
student.greet()
```

---

### **(8) 모든 클래스의 최상위 부모**

파이썬의 모든 클래스는 object 클래스를 상속받는다.

```python
class Person:
    pass
```

실제로는

```python
class Person(object):
    pass
```

와 같다.

---

### 정리

- 상속은 부모 클래스의 기능을 물려받는 것이다.
- 자식 클래스는 부모 클래스의 필드와 메서드를 사용할 수 있다.
- 상속은 Is-A 관계를 표현한다.
- 코드 재사용과 유지보수에 유리하다.
- 모든 클래스의 최상위 부모는 object 클래스이다.
