---
layout: wiki
title: 리스트 매소드와 내장 함수
wiki_name: python
parent: python/리스트
order: 12
---


## **리스트 메소드와 내장 함수**

파이썬에서 리스트는 다양한 메서드와 내장 함수를 통해 요소를 추가, 삭제, 조회, 정렬할 수 있다.

---

### **(1) 리스트 메서드 (List Method)**

리스트 객체에 직접 붙여서 사용하는 함수이다.
형식: 리스트.메서드()

---

* 추가

```python
arr.append(데이터)      # 맨 뒤에 추가
arr.extend([2,3])  # 여러 요소 추가
arr.insert(인덱스, 데이터)  # 특정 위치에 추가
```

---

* 삭제

```python
arr.remove(데이터)  # 값으로 삭제
arr.pop()      # 마지막 요소 삭제
arr.pop(인덱스)     # 인덱스로 삭제
arr.clear()    # 전체 삭제
```
---

* 조회

```python
arr.index(데이터)   # 위치 반환
arr.count(데이터)   # 개수 반환
```

---

* 정렬 및 기타

```python
arr.sort()     # 정렬 (원본 변경)
arr.sort(reverse=True) # 정렬 반대로
arr.reverse()  # 뒤집기
arr.copy()     # 복사
```
---

### **(2) 내장 함수 (Built-in Function)**

리스트에 붙지 않고 독립적으로 사용하는 함수이다.

형식: 함수(리스트)

---

* 기본 연산
```python
len(arr)   # 길이
sum(arr)   # 합
max(arr)   # 최대값
min(arr)   # 최소값
```

----

* 조건 관련

```python
all(arr)   # 모두 참이면 True
any(arr)   # 하나라도 참이면 True
```

---

* 변환 및 처리

```python
map(str, arr)                 # 함수 적용
filter(lambda x: x>0, arr)    # 조건 필터
enumerate(arr)                # 인덱스와 함께 반환
zip(arr, arr)                 # 여러 리스트를 묶음
```

---


* zip() 자세히

여러 개의 iterable을 묶어서 튜플 형태로 반환한다.
```python
a = [1, 2, 3]
b = ['a', 'b', 'c']
result = list(zip(a, b))
print(result)
```
결과:
```text
[(1, 'a'), (2, 'b'), (3, 'c')]
```
같은 인덱스끼리 묶인다
