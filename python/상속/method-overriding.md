---
layout: wiki
title: 매서드 오버라이딩
wiki_name: python
parent: python/상속
order: 3
---

## **메서드 오버라이딩(Method Overriding)**

메서드 오버라이딩은 부모 클래스의 메서드를 자식 클래스에서 다시 정의하는 것이다.

상속 관계에서 사용되며, 자식 클래스는 부모 클래스의 메서드를 자신의 목적에 맞게 변경할 수 있다.

---

### **(1) 기본 구조**

```python
class Parent:

    def method(self):
        pass

class Child(Parent):

    def method(self):
        pass
```

부모 클래스와 동일한 이름의 메서드를 자식 클래스에서 다시 작성한다.

---

### **(2) 오버라이딩 예제**

```python
class Person:

    def greet(self):
        print("안녕하세요.")

class Student(Person):

    def greet(self):
        print("저는 학생입니다.")
```

```python
student = Student()

student.greet()
```

결과:

```text
저는 학생입니다.
```

부모 클래스의 greet() 대신 자식 클래스의 greet()가 실행된다.

---

### **(3) 오버라이딩 전과 후**

부모 클래스

```python
class Shape:

    def draw(self):
        print("도형을 그립니다.")
```

자식 클래스

```python
class Circle(Shape):

    def draw(self):
        print("원을 그립니다.")
```

```python
circle = Circle()

circle.draw()
```

결과:

```text
원을 그립니다.
```

---

### **(4) 부모 메서드 호출**

오버라이딩 후에도 super()를 사용하여 부모 메서드를 호출할 수 있다.

```python
class Shape:

    def draw(self):
        print("도형을 그립니다.")

class Circle(Shape):

    def draw(self):

        super().draw()

        print("원을 그립니다.")
```

```python
circle = Circle()

circle.draw()
```

결과:

```text
도형을 그립니다.
원을 그립니다.
```

---

### **(5) 오버라이딩의 목적**

- 부모 메서드의 기능 변경
- 자식 클래스에 맞는 기능 구현
- 다형성 구현

예시

```python
class Animal:

    def sound(self):
        print("동물 소리")

class Dog(Animal):

    def sound(self):
        print("멍멍")

class Cat(Animal):

    def sound(self):
        print("야옹")
```

각 객체는 같은 sound() 메서드를 사용하지만 다른 결과를 출력한다.

---

### **(6) 오버라이딩과 오버로딩**

#### 오버라이딩

```python
class Parent:

    def show(self):
        print("Parent")

class Child(Parent):

    def show(self):
        print("Child")
```

상속 관계에서 부모 메서드를 재정의한다.

---

#### 오버로딩

```python
add(1, 2)
add(1, 2, 3)
```

같은 이름의 함수를 여러 형태로 정의하는 것이다.

파이썬은 일반적인 의미의 메서드 오버로딩을 지원하지 않는다.

---

### **(7) 실행 원리**

```python
student = Student()

student.greet()
```

파이썬은 먼저 Student 클래스에서 greet()를 찾는다.

찾으면 부모 클래스의 greet()는 무시하고 자식 클래스의 greet()를 실행한다.

---

### 정리

- 메서드 오버라이딩은 부모 메서드를 자식 클래스에서 다시 정의하는 것이다.
- 상속 관계에서 사용된다.
- 자식 클래스의 메서드가 우선 실행된다.
- super()를 이용하여 부모 메서드를 호출할 수 있다.
- 다형성을 구현하는 핵심 기능이다.
