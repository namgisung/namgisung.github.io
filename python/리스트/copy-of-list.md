---
layout: wiki
title: 리스트의 복사
wiki_name: python
parent: python/리스트
order: 8
---


## **리스트의 복사**

리스트의 복사는 여러 가지 방법이 있다.

------

### **(1) for문 활용**
```python
num = [1, 2, 3, 4, 5]
new_num = [0] * len(num)

for i in range(len(num)):
    new_num[i] = num[i]
```

-----

### **(2) 슬라이싱**
```python
num = [1, 2, 3, 4, 5]
new_num = num[:]
```

------

### **(3) copy() 함수**
```python
num = [1, 2, 3, 4, 5]
new_num = num.copy()
```

------

### **(4) list() 함수**
```python
num = [1, 2, 3, 4, 5]
new_num = list(num)
```
list()를 사용하면 기존 리스트를 새로운 리스트로 복사할 수 있다.

