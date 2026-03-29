---
layout: wiki
title: 딕셔너리의 추가/수정
wiki_name: python
parent: python/딕셔너리
order: 4
---

## **딕셔너리의 추가 / 수정**

딕셔너리는 키를 이용하여 값을 추가하거나 수정할 수 있다.

----

### **(1) 값 추가**
```python
student = {"name": "kim", "age": 20}

student["grade"] = 3
```
"grade" 키가 새로 추가되고 값 3이 저장된다.

----

### **(2) 값 수정**
```python
student = {"name": "kim", "age": 20}

student["age"] = 21
```
기존 "age"의 값이 20 → 21로 변경된다.

-----

### **여러 값 추가**
```python
student = {"name": "kim"}

student["age"] = 20
student["grade"] = 3
```
