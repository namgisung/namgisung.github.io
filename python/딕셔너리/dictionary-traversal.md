---
layout: wiki
title: 딕셔너리 순회
wiki_name: python
parent: python/딕셔너리
order: 7
---

## **딕셔너리 순회**

딕셔너리에 저장된 데이터를 하나씩 꺼내어 처리하는 것을 딕셔너리 순회라고 한다.

-----

### **(1) key 순회**
```python
student = {"name": "kim", "age": 20}

for key in student:
    print(key)
```
딕셔너리의 모든 키를 순회한다.

---

### **(2) value 순회**
```python
student = {"name": "kim", "age": 20}

for value in student.values():
    print(value)
```
딕셔너리의 모든 값을 순회한다.

----

### **(3) key, value 함께 순회**
```python
student = {"name": "kim", "age": 20}

for key, value in student.items():
    print(key, value)
```
키와 값을 동시에 사용할 수 있다.
