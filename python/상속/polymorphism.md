---
layout: wiki
title: 다형성
wiki_name: python
parent: python/상속
order: 4
---

## **다형성(Polymorphism)**

다형성은 같은 메서드 호출에 대해 객체마다 다르게 동작하는 성질이다.

상속과 메서드 오버라이딩을 통해 구현된다.

---

### **(1) 다형성이란?**

```python
animal.sound()
```

코드는 같지만 객체에 따라 결과가 달라질 수 있다.

```python
Dog().sound()
```

결과:

```text
멍멍
```

```python
Cat().sound()
```

결과:

```text
야옹
```

같은 sound() 메서드이지만 객체에 따라 다르게 동작한다.

---

### **(2) 다형성 예제**

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

```python
Dog().sound()
Cat().sound()
```

결과:

```text
멍멍
야옹
```

---

### **(3) 반복문과 다형성**

다형성은 여러 객체를 동일한 방식으로 처리할 수 있게 해준다.

```python
animals = [
    Dog(),
    Cat()
]

for animal in animals:
    animal.sound()
```

결과:

```text
멍멍
야옹
```

```python
class Shape:

    def __init__(self, name):
        self.name = name

    def getArea(self):
        raise NotImplementedError(
            "이것은 추상메소드입니다."
        )

class Circle(Shape):

    def __init__(self, name, radius):
        super().__init__(name)
        self.radius = radius

    def getArea(self):
        return 3.141592 * self.radius ** 2

class Rectangle(Shape):

    def __init__(self, name, width, height):
        super().__init__(name)

        self.width = width
        self.height = height

    def getArea(self):
        return self.width * self.height
```
```python
shapeList = [ Circle("c1", 10), Rectangle("r1", 10, 10) ]
for s in shapeList:
  print(s.getArea())
```

---

### **(4) 다형성이 필요한 이유**

다형성이 없다면

```python
dog.sound()
cat.sound()
```

객체마다 따로 처리해야 한다.

다형성을 사용하면

```python
for animal in animals:
    animal.sound()
```

처럼 동일한 코드로 여러 객체를 처리할 수 있다.

---

### **(5) 다형성과 오버라이딩**

다형성은 메서드 오버라이딩을 통해 구현된다.

```python
class Shape:

    def draw(self):
        print("도형")

class Circle(Shape):

    def draw(self):
        print("원")

class Rectangle(Shape):

    def draw(self):
        print("사각형")
```

```python
shapes = [
    Circle(),
    Rectangle()
]

for shape in shapes:
    shape.draw()
```

결과:

```text
원
사각형
```

---

### **(6) 다형성의 장점**

- 코드 재사용
- 유지보수 용이
- 확장성 향상
- 반복문을 이용한 객체 처리 가능

---

#3# **(7) 상속에서 가장 중요한 개념**

상속의 핵심 목적 중 하나는 다형성이다.

부모 타입으로 여러 자식 객체를 다룰 수 있다.

```python
animals = [
    Dog(),
    Cat()
]
```

```python
for animal in animals:
    animal.sound()
```

이와 같은 구조가 객체지향 프로그래밍의 대표적인 예이다.

---

### 정리

- 다형성은 같은 메서드 호출에 대해 객체마다 다르게 동작하는 성질이다.
- 메서드 오버라이딩을 통해 구현된다.
- 여러 객체를 동일한 방식으로 처리할 수 있다.
- 반복문과 함께 자주 사용된다.
- 상속에서 가장 중요한 개념 중 하나이다.
