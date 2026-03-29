---
layout: wiki
title: 리스트 순회
wiki_name: python
parent: python/리스트
order: 8
---

## **리스트 순회**

리스트에 저장된 값을 하나씩 꺼내어 처리하는 것을 리스트 순회라고 한다.

---

### **(1) 기본 구조**

```python
for 변수 in 리스트:
    # 실행문
```

---

### **(2) 리스트 요소 출력**

```python
arr = [10, 20, 30, 40, 50]

for i in arr:
    print(i)
```

리스트의 요소를 하나씩 꺼내어 출력한다.

---

### **(3) 인덱스를 이용한 순회**

```python
arr = [10, 20, 30, 40, 50]

for i in range(len(arr)):
    print(arr[i])
```

인덱스를 이용하여 리스트의 요소에 접근할 수 있다.

---

### **(4) enumerate() 사용**

```python
arr = [10, 20, 30, 40, 50]

for index, value in enumerate(arr):
    print(index, value)
```

인덱스와 값을 동시에 사용할 수 있다.
원하면
👉 “딕셔너리 순회도 같은 스타일로” 이어서 만들어줄게 😎
