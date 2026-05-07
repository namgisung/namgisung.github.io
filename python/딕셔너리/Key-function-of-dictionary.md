---
layout: wiki
title: 딕셔너리의 주요함수
wiki_name: python
parent: python/딕셔너리
order: 6
---

## **딕셔너리의 주요 함수**

딕셔너리는 데이터를 다루기 위한 여러 가지 함수를 제공한다.

---

### **(1) keys()**
```python
student = {"name": "kim", "age": 20}

print(student.keys())
```
결과: 
```python
dict_key(['name','age'])
```
모든 키를 반환한다.
```python
for key in student.key()
  print(key)
```
결과:
```python
name
age
```


----

### **(2) values()**
```python
student = {"name": "kim", "age": 20}

print(student.values())
```
결과: 
```python
dict_values(['kim',20])
```
모든 키를 반환한다.
```python
for value in student.values()
  print(value)
```
결과:
```python
kim
20
```

---

### **(3) items()**
```python
student = {"name": "kim", "age": 20}

print(student.items())
```
결과: 
```python
dict_items([('name','kim'), ('age', 20)])
```
(키, 값) 쌍을 반환한다.
```python
for key, value in student.items()
  print(key, value)
```
결과:
```python
name kim
age 20
```

---

### **(4) clear()**
```python
student = {"name": "kim", "age": 20}

student.clear()
```
모든 요소를 삭제한다.

---

### **(5) in 연산자**
```python
student = {"name": "kim", "age": 20}

print("name" in student)  # True
```
특정 키가 존재하는지 확인한다.
