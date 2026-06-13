---
layout: wiki
title: 정적 변수와 클래스 필드
wiki_name: python
parent: python/클래스
order: 7
---

## **정적 변수와 클래스 필드**

클래스 내부(메소드 외부)에서 선언된 변수는 모든 객체들이 공유할 수 있으며, 이를 **클래스 변수**, **정적 변수(Static Variable)**, 또는 **클래스 필드(Class Field)**라고 부른다. 

용어는 다양하지만 파이썬 표준 명칭은 **'클래스 변수'**이며, 모두 동일한 개념을 가리킨다.

---

### **(1) 클래스 변수의 선언**

```python
class Student:
    school = "ABC"  # 클래스 변수 (정적 변수, 클래스 필드)

```

---

### **(2) 클래스 변수의 특징**

* **공유성**: 모든 인스턴스(객체)가 단 하나의 메모리 공간을 공유한다.
* **독립성**: 객체 생성(`Instance`) 없이도 클래스 이름만으로 언제든 사용할 수 있다.
* **위치**: 클래스 블록 직하단, 메소드 외부에 선언한다.

---

### **(3) 클래스 이름으로 접근 (권장)**

```python
class Student:
    school = "ABC"

print(Student.school)  # 클래스이름.변수이름 형식으로 접근

```

결과:

```text
ABC

```

---

### **(4) 객체로 접근**

```python
class Student:
    school = "ABC"

s1 = Student()
print(s1.school)  # 객체를 통해서도 접근 가능

```

결과:

```text
ABC

```

---

### **(5) 모든 객체가 공유**

```python
class Student:
    school = "ABC"

s1 = Student()
s2 = Student()

# 클래스 이름을 통해 값을 변경
Student.school = "XYZ"

print(s1.school)
print(s2.school)

```

결과:

```text
XYZ
XYZ

```

클래스 변수를 변경하면 이를 참조하던 모든 객체의 값도 함께 변경된다.

---

### **(6) 인스턴스 변수와의 차이**

```python
class Student:
    school = "ABC"  # 클래스 변수 (모든 객체가 공유)

    def __init__(self, name):
        self.name = name  # 인스턴스 변수 (각 객체마다 독립적)

```

---

## **심화: 클래스 변수와 인스턴스 변수의 실전 함정**

파이썬에서 클래스 변수와 인스턴스 변수의 이름이 같을 때 발생하는 독특한 메모리 오버라이딩(덮어쓰기) 현상을 보여주는 대표적인 예제이다.

### **1. 실전 분석 코드**

```python
class MyFirstClass:
    num = 10  # 클래스 변수 (정적 필드)

    def __init__(self):
        # 객체가 생성될 때마다 공용 클래스 변수를 1씩 증가
        MyFirstClass.num += 1

    def obj_num(self):
        # 명시적으로 MyFirstClass.num을 지정하여 클래스 변수 값을 출력
        print("For obj %s num is %d" % (self, MyFirstClass.num))

# 객체 2개 생성 (생성자가 2번 실행되면서 클래스 변수는 12가 됨)
obj1 = MyFirstClass()
obj2 = MyFirstClass()

# 핵심 함정 구간: 인스턴스 이름으로 값을 수정/대입 시도
obj1.num += 1  # 이 순간 obj1 내부에 독립적인 인스턴스 변수 num이 생성됨 (다른 객체 주소 포인트)

# 결과 출력
print("num for class is %d" % MyFirstClass.num)
print("num for obj1 is %d" % obj1.num)
print("num for obj2 is %d" % obj2.num)

# 메소드 호출
obj1.obj_num()
obj2.obj_num()
print("num for class is %d" % MyFirstClass.num)

```

### **2. 실행 결과**

```text
num for class is 12
num for obj1 is 13
num for obj2 is 12
For obj <__main__.MyFirstClass object at 0x...> num is 12
For obj <__main__.MyFirstClass object at 0x...> num is 12
num for class is 12

```

### **3. 핵심 원리 및 코드 해석**

#### **값을 읽을 때 (Lookup 규칙)**

`obj2.num`처럼 값을 단순히 조회할 때, 파이썬은 먼저 `obj2` 객체 내부에 `num`이라는 인스턴스 변수가 있는지 찾는다. 없다면 상위 개념인 **클래스 변수 공간**으로 올라가서 값을 빌려와 출력한다. (따라서 `obj2.num`은 공용 변수 값인 12가 나온다.)

#### **값을 대입/수정할 때 (Assignment 규칙)**

`obj1.num += 1`은 내부적으로 `obj1.num = obj1.num + 1`로 처리된다.

파이썬에서 변수에 값을 대입(`=`)하는 행위는 해당 영역에 변수를 새로 생성하는 것과 같다. 이 대입 연산이 일어나는 순간, `obj1` 객체 메모리 내부에 클래스 변수와 이름이 똑같은 **독립적인 인스턴스 변수 `num`이 탄생**한다.

* 값은 당시에 빌려온 클래스 변수(12)에 1을 더한 **13**이 저장된다.
* 이 현상 이후로 `obj1.num`은 클래스 변수를 바라보지 않고, **자기 객체 내부에 새로 생성된 인스턴스 변수 13**만 바라보게 된다. (클래스 변수 본체는 여전히 12로 유지)

#### **메소드 내부의 출력 형태**

`obj_num()` 메소드 내부에서는 `self.num`이 아니라 명시적으로 `MyFirstClass.num`을 출력하도록 코딩되어 있다. 따라서 `obj1`이 호출하든 `obj2`가 호출하든 상관없이 무조건 공용 클래스 변수 값인 **12**가 출력된다.

---

### **4. 시각적 메모리 구조**

`obj1.num += 1`이 실행된 직후의 메모리 상태이다.

```text
[ MyFirstClass 클래스 영역 ] ───> 클래스 변수(정적 필드): num = 12
        ▲              ▲
        │ (참조 끊어짐) │ (인스턴스 변수가 없어서 여전히 클래스 변수 참조)
  [ obj1 객체 ]   [ obj2 객체 ]
   └── 인스턴스 변수   └── 인스턴스 변수
       num = 13            (없음)

```

---

### 정리

* **정적 필드, 정적 변수, 클래스 필드**는 모두 파이썬의 **클래스 변수**를 뜻하는 말이다.
* 인스턴스 이름으로 값을 읽을 때 변수가 없으면 클래스 변수를 찾아가서 빌려온다.
* 인스턴스 이름으로 값을 수정하거나 대입(`obj.num = 값`)하면, 클래스 변수가 바뀌는 게 아니라 **그 객체만을 위한 독립적인 인스턴스 변수가 새로 생성되어 클래스 변수를 가린다(오버라이딩).**
