---
layout: wiki
title: 집합(set)
wiki_name: python
parent: python
order: 15
---

## **집합 (set)**

집합(set)은 중복을 허용하지 않고, 순서가 없는 자료형이다.

---

### **(1) 특징**

- 중복 요소를 자동으로 제거한다  
- 순서가 없기 때문에 인덱스를 사용할 수 없다  
- 변경 가능한(mutable) 자료형이다  

```python
s = {1, 2, 2, 3}
print(s)   # {1, 2, 3}
```

---

### **(2) 생성 방법**

```python
s1 = {1, 2, 3}
s2 = set([1, 2, 3])
```
빈 집합 생성
```python
s = set()   # {}는 딕셔너리
```

---

### **(3) 요소 추가 / 삭제**

```python
s = {1, 2, 3}
s.add(4)        # 요소 1개 추가
s.update([5,6]) # 여러 요소 추가
s.remove(2)     # 삭제 (없으면 오류 발생)
s.discard(10)   # 삭제 (없어도 오류 없음)
s.pop()         # 임의의 요소 삭제
s.clear()       # 전체 삭제
```

---

### **(4) 집합 연산**

```python
a = {1, 2, 3}
b = {3, 4, 5}
print(a & b)  # 교집합
print(a | b)  # 합집합
print(a - b)  # 차집합
```
또는
```python
a.intersection(b) #교집합
a.union(b) #합집합
a.difference(b) #차집합
```

---

### **(5) 포함 여부**
```python
s = {1, 2, 3}
print(1 in s)   # True
```
해시 기반이라 매우 빠르다

---

### **(6) 형 변환**
```python
arr = [1, 2, 2, 3]
s = set(arr)        # 중복 제거
arr2 = list(s)
```

----

### **내장함수**

집합은 전용 내장함수가 없고 대신 리스트 내장함수를 같이 쓴다.
