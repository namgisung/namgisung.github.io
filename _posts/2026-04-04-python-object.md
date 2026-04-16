---
layout: base
title:  "[python 잡다한것] 파이썬 객체 정리"
date:   2026-04-04
categories: [python 잡다한것]
---

## **파이썬 객체 정리**

파이썬의 자료형은 값의 변경 가능 여부에 따라 불변 객체와 가변 객체로 나눌 수 있다.
또한 여러 값을 하나로 묶어 저장하는 자료형이 존재한다.

---

### **(1) 불변 객체 (Immutable)**

불변 객체는 생성 후 값을 변경할 수 없는 객체이다.
값을 변경하려면 새로운 객체를 생성해야 한다.

* 숫자 (int, float)
* 문자열 (str)
* 튜플 (tuple)

```python
a = "hello"
a = "world"  # 새로운 객체 생성
```
함수 인자로 들어갈때 불변 객체는 복사본을 전달한다.
```python
def modify1(s):
  s += "To You"

msg = "Happy Birthday"
print("msg=", msg)
modify1(msg)
print("msg=", msg)
```
```python
msg= Happy Birthday
msg= Happy Birthday
```
---

### **(2) 가변 객체 (Mutable)**

가변 객체는 생성 후에도 값을 직접 수정할 수 있는 객체이다.

데이터가 큰 객체들이다.

* 리스트 (list)
* 딕셔너리 (dict)
* 집합 (set)
* 배열 (array)
* 사용자가 정의한 객체 (user-defined classes (unless specifically made immutable))

```python
arr = [1, 2, 3]
arr[0] = 10  # 값 변경 가능
```
함수 인자로 들어갈때 가변 객체는 원본을 전달한다.
```python
def modify2 (li):
  li += [100, 200]

list = [1, 2, 3, 4, 5]
print (list)
modify2 (list)
print (list)
```
```python
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 100, 200]
```

---

### **(3) 여러 값을 묶는 자료형**

여러 개의 값을 하나로 묶어 저장하는 자료형이다.

* 리스트 (list) → 변경 가능
* 튜플 (tuple) → 변경 불가능
* 문자열 (str) → 문자들의 집합 (불변)

```python
arr = [1, 2, 3]
t = (1, 2, 3)
s = "hello"
```
