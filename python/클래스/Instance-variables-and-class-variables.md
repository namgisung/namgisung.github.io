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

```

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

### **(4) 클래스 변수 활용 예제 (시리얼 번호 발급)**

클래스 변수는 단순히 데이터를 공유하는 역할뿐만 아니라, 생성된 객체의 총개수를 누적하거나 고유한 시리얼 번호(ID)를 순차적으로 부여할 때 유용하게 활용된다.

```python
class Television:
    serialNumber = 0  # 클래스 변수 (전체 생산 대수 관리)

    def __init__(self, channel, volume, on):
        self.channel = channel
        self.volume = volume
        self.on = on
        
        # 새로운 TV가 생성될 때마다 클래스 변수를 1씩 증가
        Television.serialNumber += 1 
        
        # 증가된 클래스 변수 값을 이 객체의 고유 번호(인스턴스 변수)로 할당
        self.number = Television.serialNumber

    def show(self):
        print("채널: %d, 음량: %d, 전원: %s, 고유번호: %d" % (self.channel, self.volume, self.on, self.number))

# 객체 생성
tv1 = Television(11, 10, True)
tv2 = Television(7, 15, True)
tv3 = Television(24, 5, False)

tv1.show()
tv2.show()
tv3.show()

```

결과:

```text
채널: 11, 음량: 10, 전원: True, 고유번호: 1
채널: 7, 음량: 15, 전원: True, 고유번호: 2
채널: 24, 음량: 5, 전원: False, 고유번호: 3

```

`Television.serialNumber`라는 공용 카운터를 통해 각 인스턴스(`self.number`)에 중복되지 않는 고유 번호를 성공적으로 부여할 수 있다.

---

### **(5) 인스턴스 변수와 클래스 변수 비교**

| 구분 | 인스턴스 변수 | 클래스 변수 |
| --- | --- | --- |
| **생성 위치** | 메소드 내부에서 `self.` 사용 | 클래스 내부, 메소드 외부 공간 |
| **저장 위치** | 개별 객체(인스턴스) 메모리 내부 | 클래스 자체의 고유 메모리 내부 |
| **공유 여부** | 객체마다 다른 값을 가짐 (독립적) | 모든 객체가 단 하나의 값을 공유 |
| **접근 방법** | `객체명.인스턴스변수` | `클래스명.클래스변수` (권장) |
