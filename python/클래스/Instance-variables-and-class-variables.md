---
layout: wiki
title: 인스턴스 변수와 클래스 변수
wiki_name: python
parent: python/클래스
order: 6
---

## **인스턴스 변수와 클래스 변수**

클래스 내부의 변수는 인스턴스 변수와 클래스 변수로 구분된다.

---

### **(1) 인스턴스 변수**

인스턴스 변수는 객체마다 독립적으로 생성되는 변수이다.

```python
class Student:

    def __init__(self, name):
        self.name = name
````

self.name은 인스턴스 변수이다.

---

#### **객체마다 다른 값 저장**

```python
class Student:

    def __init__(self, name):
        self.name = name

s1 = Student("kim")
s2 = Student("lee")

print(s1.name)
print(s2.name)
```

결과:

```text
kim
lee
```

각 객체는 서로 다른 값을 가진다.

---

### **(2) 클래스 변수**

클래스 변수는 모든 객체가 공유하는 변수이다.

```python
class Student:

    school = "ABC"

    def __init__(self, name):
        self.name = name
```

school은 클래스 변수이다.

---

#### **클래스 변수 사용**

```python
class Student:

    school = "ABC"

    def __init__(self, name):
        self.name = name

s1 = Student("kim")
s2 = Student("lee")

print(s1.school)
print(s2.school)
```

결과:

```text
ABC
ABC
```

모든 객체가 같은 값을 공유한다.

---

### **(3) 클래스 변수 변경**

```python
class Student:

    school = "ABC"

s1 = Student()
s2 = Student()

Student.school = "XYZ"

print(s1.school)
print(s2.school)
```

결과:

```text
XYZ
XYZ
```

클래스 변수를 변경하면 모든 객체에 영향을 준다.

---

### **(4) 인스턴스 변수와 클래스 변수 비교**

| 구분    | 인스턴스 변수 | 클래스 변수   |
| ----- | ------- | -------- |
| 생성 위치 | self 사용 | 클래스 내부   |
| 저장 위치 | 객체 내부   | 클래스 내부   |
| 공유 여부 | 객체마다 다름 | 모든 객체 공유 |
