---
layout: wiki
title: 딕셔너리의 접근
wiki_name: python
parent: python/딕셔너리
order: 3
---

## **딕셔너리의 접근**

딕셔너리는 키(key)를 이용하여 값(value)에 접근한다.

리스트가 인덱스를 사용하는 것과 달리, 딕셔너리는 키를 사용한다.

----

### **(1) 기본 접근**
```python
student = {"name": "kim", "age": 20}

print(student["name"])  # kim
print(student["age"])   # 20
```
키를 대괄호 [] 안에 넣어 값을 가져온다.

-----

### **(2) 존재하지 않는 키 접근**
```python
student = {"name": "kim"}

print(student["age"])  # 오류 발생
```
존재하지 않는 키에 접근하면 오류가 발생한다.

----

### **(3) get() 함수 사용**
```python
student = {"name": "kim"}

print(student.get("age"))  # None
```

키가 없어도 오류가 발생하지 않고 None을 반환한다.

-----

### **(4) 기본값 지정**
```python
student = {"name": "kim"}

print(student.get("age", 0))  # 0
```
키가 없을 경우 기본값을 지정할 수 있다.
