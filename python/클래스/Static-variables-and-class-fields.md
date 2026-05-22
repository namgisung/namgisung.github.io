---
layout: wiki
title: 정적 변수와 클래스 필드
wiki_name: python
parent: python/클래스
order: 7
---

## **정적 변수와 클래스 필드**

클래스 내부에서 생성된 변수는 객체들이 공유할 수 있으며 이를 클래스 변수 또는 정적 변수(static variable)라고 한다.

클래스 변수는 클래스 필드(class field)라고도 한다.

---

### **(1) 클래스 변수의 선언**

```python
class Student:

    school = "ABC"
````

school은 클래스 변수(정적 변수, 클래스 필드)이다.

---

### **(2) 클래스 변수의 특징**

* 객체들이 공유한다.
* 객체 생성 없이 사용할 수 있다.
* 클래스 내부에 선언한다.

---

### **(3) 클래스 이름으로 접근**

```python 
class Student:

    school = "ABC"

print(Student.school)
```

결과:

```text
ABC
```

클래스이름.변수이름 형식으로 접근한다.

---

### **(4) 객체로 접근**

```python
class Student:

    school = "ABC"

s1 = Student()

print(s1.school)
```

결과:

```text
ABC
```

객체를 통해서도 접근할 수 있다.

---

### **(5) 모든 객체가 공유**

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

```
XYZ
XYZ
```

모든 객체가 같은 데이터를 공유한다.

---

### **(6) 인스턴스 변수와의 차이**

```python
class Student:

    school = "ABC"

    def __init__(self, name):
        self.name = name
```

* school → 클래스 변수
* self.name → 인스턴스 변수
