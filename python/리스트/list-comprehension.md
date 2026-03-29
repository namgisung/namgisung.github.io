---
layout: wiki
title: 리스트 컴프리맨션
wiki_name: python
parent: python/리스트
order: 5
---



## **리스트 컴프리헨션**

리스트 컴프리헨션은 반복문을 사용하여 리스트를 간단하게 생성하는 방법이다.

---

### **(1) 기본 구조**

```python
[표현식 for 변수 in 반복가능한객체]
```

---

### **(2) 기본 예제**

```python
arr = []

for i in range(5):
    arr.append(i)
```

위 코드를 리스트 컴프리헨션으로 쓰면:

```python
arr = [i for i in range(5)]
```

---

### 조건 포함

```python
arr = [i for i in range(10) if i % 2 == 0]
```

짝수만 저장


```python
arr = [i * 2 for i in range(5)]
```

결과:

```text
[0, 2, 4, 6, 8]
```

---


기존 방식:

```python
arr = []
for i in range(5):
    arr.append(i)
```

컴프리헨션:

```python
arr = [i for i in range(5)]
```
