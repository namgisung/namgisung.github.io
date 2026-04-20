---
layout: wiki
title: 리스트 컴프리헨션
wiki_name: python
parent: python/리스트
order: 6
---

## **리스트 컴프리헨션**

리스트 컴프리헨션은 반복문을 사용하여 리스트를 간단하게 생성하는 방법이다.

---

### **(1)*삼항 연산자**

```python id="a1k9zp"
x = 5
result = 10 if x > 0 else 0
print(result)
```

결과:

```text id="r1m4qk"
10
```

단독으로 사용되는 조건 표현식 (컴프리헨션 아님)

---

### **(2)*수식 + for**

```python
arr = [i for i in range(5)]
print(arr)
```

결과:

```text
[0, 1, 2, 3, 4]
```

---

### **(3)*수식 + for + for (중첩 반복)**

```python
arr = [j for i in range(2) for j in range(3)]
print(arr)
```

결과:

```text
[0, 1, 2, 0, 1, 2]
```

---

### **(4)*수식 + for + if (조건 필터링)**

```python
arr = [i for i in range(10) if i % 2 == 0]
print(arr)
```

결과:

```text
[0, 2, 4, 6, 8]
```

---

### **(5)*수식 + if ~ else + for (삼항 포함)**

```python 
arr = [i if i % 2 == 0 else 0 for i in range(5)]
print(arr)
```

결과:

```text 
[0, 0, 2, 0, 4]
```
