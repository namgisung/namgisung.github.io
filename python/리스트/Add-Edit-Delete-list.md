---
layout: wiki
title: 리스트의 추가,수정,삭제
wiki_name: python
parent: python/리스트
order: 5
---

## **리스트의 추가, 수정, 삭제**

리스트는 가변 객체이므로 요소를 추가, 수정, 삭제할 수 있다.

---

### **(1) 요소 추가**

리스트에 값을 추가하는 방법은 여러 가지가 있다.

```python
arr = [1, 2, 3]

arr.append(4)      # 맨 뒤에 추가
print(arr)         # [1, 2, 3, 4]
```

```python
arr.insert(1, 10)  # 인덱스 1 위치에 10 추가
print(arr)         # [1, 10, 2, 3, 4]
```

```python
arr.extend([5, 6]) # 여러 요소 추가
print(arr)         # [1, 10, 2, 3, 4, 5, 6]
```

---

### **(2) 요소 수정**

인덱스를 사용하여 값을 변경할 수 있다.

```python
arr = [1, 2, 3]

arr[0] = 10
print(arr)   # [10, 2, 3]
```

---

### **(3) 요소 삭제**

리스트에서 요소를 삭제하는 방법도 여러 가지가 있다.

```python
arr = [1, 2, 3, 4]

arr.pop()        # 마지막 요소 삭제
print(arr)       # [1, 2, 3]
```

```python
arr.pop(1)       # 인덱스 1 삭제
print(arr)       # [1, 3]
```

```python
arr.remove(3)    # 값 3 삭제
print(arr)       # [1]
```

```python
del arr[0]       # 인덱스 0 삭제
print(arr)       # []
```

### **(4) 리스트 삭제**
```python
aa = [10, 20, 30]
aa = []
print(aa)  # []
````
> 기존 리스트를 버리고, 새로운 빈 리스트를 다시 할당

```python
aa = [10, 20, 30]
aa = None
print(aa)  # None
```
> 리스트가 아니라 **아무것도 참조하지 않는 상태(None)**

```python
aa = [10, 20, 30]
del aa
print(aa)  # 오류 발생
```
> 변수 자체가 메모리에서 제거됨 (이름이 사라짐)
