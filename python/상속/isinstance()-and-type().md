---
layout: wiki
title: isinstance()와 type()
wiki_name: python
parent: python/상속
order: 6
---

## **isinstance()와 type()**

파이썬에서 객체(인스턴스)가 어떤 클래스를 바탕으로 만들어졌는지 확인하기 위해 `isinstance()` 함수와 `type()` 함수를 사용한다. 

두 함수는 비슷해 보이지만, **상속 관계에 있는 객체를 검사할 때 결정적인 차이점**이 발생하므로 명확히 구분하여 사용해야 한다.

---

### **(1) isinstance() 함수**

`isinstance(object, class)`는 객체가 해당 클래스의 인스턴스이거나, **해당 클래스를 상속받은 자식 클래스의 인스턴스인지** 확인한다.

```python
class Person:
    pass

class Student(Person):
    pass

student = Student()

print(isinstance(student, Student))  # 본인 클래스 확인
print(isinstance(student, Person))   # 부모 클래스 확인

```

결과:

```text
True
True

```

`Student`는 `Person`을 상속받았기 때문에(Is-A 관계), `student` 객체는 `Person` 클래스의 인스턴스로도 인정된다.

---

### **(2) type() 함수**

`type(object)`은 객체가 생성된 **실제 정밀한 클래스 타입**만을 반환한다. 상속 관계를 고려하지 않고 오직 현재 객체 고유의 뼈대만 확인한다.

```python
class Person:
    pass

class Student(Person):
    pass

student = Student()

print(type(student) == Student)  # 본인 클래스 일치 확인
print(type(student) == Person)   # 부모 클래스 일치 확인

```

결과:

```text
True
False

```

`student` 객체의 실제 고유 타입은 `Student`일 뿐이므로, 부모 클래스인 `Person`과 비교하면 `False`를 반환한다.

---

### **(3) 실전 차이점 비교 예제**

두 함수의 동작 메커니즘 차이를 명확하게 보여주는 일괄 검증 예제이다.

```python
class Animal:
    pass

class Dog(Animal):
    pass

poodle = Dog()

# 1. isinstance() 테스트 (상속 관계 인정)
print("[isinstance] poodle is Dog? -> %s" % isinstance(poodle, Dog))
print("[isinstance] poodle is Animal? -> %s" % isinstance(poodle, Animal))

print("-" * 40)

# 2. type() 테스트 (상속 관계 무시, 순수 타입만 비교)
print("[type] poodle is Dog? -> %s" % (type(poodle) == Dog))
print("[type] poodle is Animal? -> %s" % (type(poodle) == Animal))

```

결과:

```text
[isinstance] poodle is Dog? -> True
[isinstance] poodle is Animal? -> True
----------------------------------------
[type] poodle is Dog? -> True
[type] poodle is Animal? -> False

```

---

### **(4) isinstance()와 type()의 뒤집힌 표 비교**

두 함수의 특징과 상속 관계 필터링 기준을 가독성 있게 정리한 표이다.

| 판단 및 동작 기준 | `isinstance(객체, 클래스)` | `type(객체) == 클래스` |
| --- | --- | --- |
| **본인 클래스 검사** | **가능** (`True`) | **가능** (`True`) |
| **부모 클래스(상속) 검사** | **가능** (`True`) <br>(자식 객체도 부모 타입으로 인정) | **불가능** (`False`) <br>(상속 관계를 철저히 외면함) |
| **주요 용도** | 객체지향의 **다형성**을 유지하며 <br>안전하게 타입을 체크할 때 사용 (권장) | 상속 관계 다 치우고, 오직 정확한 <br>원래의 클래스가 무엇인지 매칭할 때 사용 |

---

### 정리

- `isinstance()`는 상속 구조를 이해하는 함수이다. 자식 객체를 부모 클래스냐고 물어봐도 `True`를 준다.
- `type()`은 상속 구조를 무시하는 아주 엄격한 함수이다. 오직 객체가 찍혀 나온 진짜 고유의 클래스 한 놈만 골라낸다.
- 객체지향 프로그래밍(OOP) 및 상속 계층을 다룰 때는 유연한 구조를 위해 `type()`보다 `isinstance()`를 사용하는 것이 설계 표준(Best Practice)에 가깝다.
