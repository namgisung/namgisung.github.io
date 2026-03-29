---
layout: wiki
title: 딕셔너리의 삭제
wiki_name: python
parent: python/딕셔너리
order: 5
---


## **딕셔너리의 삭제**

딕셔너리는 특정 키를 이용하여 값을 삭제할 수 있다.

-----

### **(1) del 키워드 사용**
```python
student = {"name": "kim", "age": 20}

del student["age"]
```
"age" 키와 해당 값이 삭제된다.

다만, 존재하지 읺는 키 삭제시 오류난다.

----

### **(2) pop() 함수 사용**
```python
student = {"name": "kim", "age": 20}

student.pop("age")
```
"age" 키를 삭제하고 해당 값을 반환한다.

----

### **(3) pop() 기본값 설정**
```python
student = {"name": "kim"}

student.pop("age", None)
```
키가 없어도 오류가 발생하지 않는다.
