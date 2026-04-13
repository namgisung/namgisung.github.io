---
layout: wiki
title: 리스트의 초기화
wiki_name: python
parent: python/리스트
order: 4
---

## **리스트의 초기화**

리스트는 생성과 동시에 값을 넣을 수 있다.
```python
score = [50, 60, 70, 80, 90]
```
또는 요소에 직접 값을 저장할 수도 있다.
```python
score = [0, 0, 0, 0, 0]
```
```python
score[0] = 50
score[1] = 60
score[2] = 70
score[3] = 80
score[4] = 90
```

-----

### **(1) for문 활용**
```python
score = [0] * 5

for i in range(len(score)):
    score[i] = i * 10 + 50
```

-----

### **(2) 리스트 생성과 초기화를 동시에 하기**
```python
score = [50, 60, 70, 80, 90]
```
또는 리스트 컴프리헨션을 사용할 수도 있다.
```python
score = [i * 10 + 50 for i in range(5)]
```
