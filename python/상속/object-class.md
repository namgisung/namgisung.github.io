---
layout: wiki
title: object 클래스
wiki_name: python
parent: python/상속
order: 7
---

## **object 클래스**

파이썬에서 정의되는 **모든 클래스는 예외 없이 최상위 클래스인 `object` 클래스를 자동으로 상속**받는다. 

클래스를 선언할 때 괄호를 비워두거나 상속을 명시하지 않아도, 파이썬 내부적으로는 무조건 `object` 클래스의 자식 클래스로 등록된다.

---

### **(1) 숨겨진 상속 구조**

개발자가 작성한 일반적인 클래스 코드가 파이썬 내부에서 해석되는 형태의 비교이다.

```python
# 1. 개발자가 작성한 코드
class Person:
    pass

# 2. 파이썬이 실제로 처리하는 코드
class Person(object):
    pass

```

따라서 우리가 만드는 모든 클래스는 태어날 때부터 `object` 클래스가 가진 강력한 기본 기능(메서드)들을 고스란히 물려받아 사용하게 된다.

---

### **(2) object 클래스를 증명하는 방법**

`isinstance()` 함수나 클래스의 상속 계층을 보여주는 `__mro__` 속성을 활용하면, 우리가 만든 클래스가 진짜로 `object`를 상속받았는지 눈으로 확인할 수 있다.

```python
class Student:
    pass

s = Student()

# 1. isinstance로 object 계층 확인
print("s는 object의 인스턴스인가? -> %s" % isinstance(s, object))

# 2. MRO(메서드 탐색 순서) 확인
print("Student 클래스의 상속 계층: %s" % str(Student.__mro__))

```

결과:

```text
s는 object의 인스턴스인가? -> True
Student 클래스의 상속 계층: (<class '__main__.Student'>, <class 'object'>)

```

출력 결과에서 보듯 `Student` 클래스의 최종 종착지(최상위 부모)는 무조건 `<class 'object'>`가 된다.

---

### **(3) object 클래스가 물려주는 마법 메서드 (Special Method)**

우리가 클래스를 만들 때 직접 정의하지 않아도 쓸 수 있었던 `__init__`, `__str__`, `__dir__` 같은 수많은 언더바 2개(`__`) 짜리 메서드들은 전부 **`object` 클래스가 자식들에게 기본으로 물려준 유산**이다.

자식 클래스들은 이 유산들을 메서드 오버라이딩(Method Overriding)하여 입맛에 맞게 개조해서 사용한다.

#### **대표적인 오버라이딩 예시: `__str__` 메서드**

`object` 클래스가 물려준 원본 `__str__`은 객체를 프린트할 때 주소값(`<__main__.Student object at 0x...>`)을 찍어내도록 설계되어 있다. 이를 자식 클래스에서 오버라이딩하면 내가 원하는 문자열이 찍히도록 바꿀 수 있다.

```python
class Student(object):  # object 명시 (생략 가능)
    def __init__(self, name):
        self.name = name

    # 부모(object)가 물려준 __str__ 메서드를 내 입맛에 맞게 오버라이딩!
    def __str__(self):
        return "학번 및 이름: %s" % self.name

s1 = Student("남기성")
print(s1)  # 내부적으로 s1.__str__()이 호출됨

```

결과:

```text
학번 및 이름: 남기성

```

만약 `__str__`을 오버라이딩하지 않았다면 `object` 본연의 기능이 작동하여 재미없는 메모리 주소값만 출력되었을 것이다.

---

### **(4) 상속 계층도 시각화**

파이썬 세계관의 모든 객체지향 구조는 단 하나의 거대한 뿌리에서 뻗어나온다.

```text
       [ object 클래스 ]  <--- 파이썬의 모든 클래스의 시조새
        ▲             ▲
        │ (자동 상속)  │ (자동 상속)
   [ Person ]     [ Animal ]
        ▲             ▲
        │             │
   [ Student ]     [ Dog ]

```

---

### 정리

- 파이썬의 모든 클래스는 명시하지 않아도 무조건 `object` 클래스를 최상위 부모로 둔다.
- 파이썬의 핵심 내장 기능들(`__init__`, `__str__` 등)은 모두 `object` 클래스로부터 상속받은 것이다.
- `object`가 물려준 기본 메서드들을 자식 클래스에서 오버라이딩함으로써 파이썬다운(Pythonic) 강력한 객체를 설계할 수 있다.
