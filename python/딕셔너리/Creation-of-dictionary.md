---
layout: wiki
title: 딕셔너리의 생성
wiki_name: python
parent: python/딕셔너리
order: 2
---

## **딕셔너리의 생성**

딕셔너리는 중괄호 {}를 사용하여 생성한다.

키(key)와 값(value)을 :로 연결하고, 각 요소는 쉼표(,)로 구분한다.

딕셔너리이름 = {키1: 값1, 키2: 값2}

-----

### **(1) 기본 생성**
```python
student = {"name": "kim", "age": 20}
```
키 "name"에 "kim",

키 "age"에 20이 저장된다.

------

### **(2) 빈 딕셔너리 생성**
```python
student = {}
```
또는
```python
student = dict()
```

------

### **(3) dict() 함수로 생성**
```python
student = dict(name="kim", age=20)
```
키를 문자열처럼 작성할 때 사용 가능

-----

### **(4) 리스트를 이용한 생성**
```python
student = dict([("name", "kim"), ("age", 20)])
```
(키, 값) 형태의 튜플을 이용하여 생성

-----

### **주의사항**
```python
student = {"name": "kim", "name": "lee"}
```
결과:
```python
{'name': 'lee'}
```
키가 중복되면 마지막 값만 남는다.
