---
layout: wiki
title: is 와 is not
wiki_name: python
parent: python/클래스
order: 11
---

## **is 와 is not**

is 연산자는 두 변수가 같은 객체를 참조하는지 확인한다.

is not 연산자는 서로 다른 객체를 참조하는지 확인한다.

---

## **(1) is 연산자**

```python
a = [1, 2, 3]
b = a

print(a is b)
```

결과:

```text
True
```

a와 b는 같은 객체를 참조한다.

---

### **(2) is not 연산자**

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a is not b)
```

결과:

```text
True
```

a와 b는 서로 다른 객체이다.

---

### **(3) == 와 is 의 차이**

== 는 값(value)을 비교한다.

is 는 객체의 주소(참조값)를 비교한다.

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
print(a is b)
```

결과:

```text
True
False
```

* == → 값 비교
* is → 객체 비교

---

### **(4) 객체 참조 예시**

```python
a = [1, 2, 3]
b = a

b[0] = 100

print(a)
```

결과:

```text
[100, 2, 3]
```

a와 b는 같은 객체를 참조하므로 함께 변경된다.

---

### **(5) is 와 is not의 특징**

* 객체의 주소를 비교한다.
* 객체 참조 여부를 확인할 때 사용한다.
* == 와는 의미가 다르다.
