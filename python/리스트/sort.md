---
layout: wiki
title: 리스트의 정렬
wiki_name: python
parent: python/리스트
order: 10
---

## **리스트의 정렬**

리스트의 요소를 정렬할 때는 `sort()` 메서드를 사용한다.

---

### **(1) 기본 구조**

```python
리스트이름.sort()
```

---

### **(2) 기본 예제**

```python
arr = [3, 1, 4, 2]
arr.sort()

print(arr)   # [1, 2, 3, 4]
```

리스트의 요소가 오름차순으로 정렬된다.

---

### **(3) 내림차순 정렬**

```python
arr = [3, 1, 4, 2]
arr.sort(reverse=True)

print(arr)   # [4, 3, 2, 1]
```

---

### **(4) 문자열 정렬**

```python
arr = ["banana", "apple", "cherry"]
arr.sort()

print(arr)   # ['apple', 'banana', 'cherry']
```

문자열은 알파벳 순서로 정렬된다.

---

### **(5) sorted() 함수**

`sorted()`는 새로운 리스트를 반환한다.

```python
arr = [3, 1, 4, 2]

new_arr = sorted(arr)

print(new_arr)  # [1, 2, 3, 4]
print(arr)      # [3, 1, 4, 2]
```

---

## sort() vs sorted()

* `sort()` : 원본 리스트를 변경
* `sorted()` : 새로운 리스트 반환
