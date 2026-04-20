---
layout: wiki
title: 리스트 슬라이싱
wiki_name: python
parent: python/리스트
order: 12
---


리스트 메서드와 내장 함수

파이썬에서 리스트는 다양한 메서드와 내장 함수를 통해 요소를 추가, 삭제, 조회, 정렬할 수 있다.

⸻

(1) 리스트 메서드 (List Method)

리스트 객체에 직접 붙여서 사용하는 함수이다.
형식: 리스트.메서드()

⸻

① 추가

arr.append(1)      # 맨 뒤에 추가
arr.extend([2,3])  # 여러 요소 추가
arr.insert(1, 10)  # 특정 위치에 추가

⸻

② 삭제

arr.remove(2)  # 값으로 삭제
arr.pop()      # 마지막 요소 삭제
arr.clear()    # 전체 삭제

⸻

③ 조회

arr.index(3)   # 위치 반환
arr.count(3)   # 개수 반환

⸻

④ 정렬 및 기타

arr.sort()     # 정렬 (원본 변경)
arr.reverse()  # 뒤집기
arr.copy()     # 복사

⸻

(2) 내장 함수 (Built-in Function)

리스트에 붙지 않고 독립적으로 사용하는 함수이다.
형식: 함수(리스트)

⸻

① 기본 연산

len(arr)   # 길이
sum(arr)   # 합
max(arr)   # 최대값
min(arr)   # 최소값

⸻

② 조건 관련

all(arr)   # 모두 참이면 True
any(arr)   # 하나라도 참이면 True

⸻

③ 변환 및 처리

map(str, arr)                 # 함수 적용
filter(lambda x: x>0, arr)    # 조건 필터
enumerate(arr)                # 인덱스와 함께 반환
zip(arr, arr)                 # 여러 리스트를 묶음

⸻

④ zip() 자세히

여러 개의 iterable을 묶어서 튜플 형태로 반환한다.
```python
a = [1, 2, 3]
b = ['a', 'b', 'c']
result = list(zip(a, b))
print(result)
```
결과:

[(1, 'a'), (2, 'b'), (3, 'c')]

같은 인덱스끼리 묶인다
