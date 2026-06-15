---
layout: wiki
title: super()
wiki_name: python
parent: python/상속
order: 2
---

## **super()**

super()는 부모 클래스의 메서드나 생성자를 호출하기 위해 사용하는 함수이다.

주로 자식 클래스의 생성자에서 부모 클래스의 생성자를 호출할 때 사용한다.

---

### **(1) 기본 구조**

```python
super().메서드명()
```

또는

```python
super().__init__()
```

---

### **(2) 부모 생성자 호출**

```python
class Person:

    def __init__(self, name):
        self.name = name

class Student(Person):

    def __init__(self, name):
        super().__init__(name)

student = Student("Kim")

print(student.name)
```

결과:

```text
Kim
```

부모 클래스의 생성자를 호출하여 name 필드를 초기화한다.

---

### **(3) 부모 생성자 + 자식 생성자**

```python
class Person:

    def __init__(self, name):
        self.name = name

class Student(Person):

    def __init__(self, name, major):

        super().__init__(name)

        self.major = major

student = Student(
    "Kim",
    "Computer Science"
)

print(student.name)
print(student.major)
```

결과:

```text
Kim
Computer Science
```

자식 클래스는 부모의 필드와 자신의 필드를 모두 가질 수 있다.

---

### **(4) 부모 메서드 호출**

```python
class Person:

    def greet(self):
        print("안녕하세요.")

class Student(Person):

    def greet(self):

        super().greet()

        print("저는 학생입니다.")
```

```python
student = Student()

student.greet()
```

결과:

```text
안녕하세요.
저는 학생입니다.
```

부모 메서드를 실행한 후 자식 클래스의 기능을 추가할 수 있다.

---

### **(5) super()를 사용하는 이유**

```python
class Student(Person):

    def __init__(self, name, major):

        super().__init__(name)

        self.major = major
```

- 부모 클래스의 코드를 재사용할 수 있다.
- 중복 코드를 줄일 수 있다.
- 유지보수가 쉬워진다.

---

### **(6) 생성자 호출 순서**

```python
class Person:

    def __init__(self):
        print("Person 생성")

class Student(Person):

    def __init__(self):

        super().__init__()

        print("Student 생성")
```

```python
student = Student()
```

결과:

```text
Person 생성
Student 생성
```

부모 클래스의 생성자가 먼저 실행된다.

---

### **(7) 주의사항**

```python
class Student(Person):

    def __init__(self, name):

        super().__init__(name)
```

부모 클래스의 생성자가 필요한 매개변수를 가지고 있다면 반드시 전달해야 한다.

교수님 수업 기준으로는 부모 생성자 호출을 생성자 맨 앞에 작성하는 것이 좋다.

---

### 정리

- super()는 부모 클래스의 메서드나 생성자를 호출한다.
- 주로 부모 생성자를 호출할 때 사용한다.
- 코드 재사용에 유리하다.
- 부모 생성자가 먼저 실행된다.
- 부모 메서드를 호출하여 기능을 확장할 수 있다.
