---
layout: wiki
title: reduce()
wiki_name: python
parent: python/람다함수
order: 4
---

## **reduce()**

reduce()는 반복 가능한 객체의 각 요소를 누적 적용하여 하나의 결과값을 만드는 함수이다.

모든 요소를 차례대로 연산하여 단 하나의 최종 값을 도출할 때 사용한다.

---

### **(1) 기본 구조**

```python
from functools import reduce

reduce(함수, 반복가능객체, 초기값)

```

* 함수 : 두 개의 인자(누적값, 현재값)를 받아 하나의 값을 반환하는 함수
* 반복가능객체 : 리스트, 튜플 등의 반복 가능한 객체
* 초기값 (선택) : 연산을 시작할 때 사용할 초기값

reduce()는 내장 함수가 아니므로 `functools` 모듈에서 가져와야 하며, 최종 결과값(단일 값)을 반환한다.

---

### **(2) 일반 함수 사용 (누적 합계)**

```python
from functools import reduce

def add(x, y):
    return x + y

numbers = [1, 2, 3, 4]

result = reduce(add, numbers)

print(result)

```

결과:

```python
10

```

요소들이 처음부터 끝까지 순서대로 더해져 최종 합계가 반환된다.

---

### **(3) 람다 함수 사용**

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(
    lambda x, y: x * y,
    numbers
)

print(result)

```

결과:

```python
24

```

람다 함수와 함께 사용하여 리스트 내 모든 요소의 곱(팩토리얼 효과)을 간결하게 구한다.

---

### **(4) 초기값(Initializer) 활용**

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(
    lambda x, y: x + y,
    numbers,
    100
)

print(result)

```

결과:

```python
110

```

초기값 100부터 시작하여 `100 + 1 + 2 + 3 + 4` 연산이 수행된다. 빈 리스트가 올 수 있는 상황에서 에러를 방지하기 위해서도 사용된다.

---

### **(5) 최댓값 구하기**

```python
from functools import reduce

numbers = [3, 1, 7, 4, 5]

result = reduce(
    lambda x, y: x if x > y else y,
    numbers
)

print(result)

```

결과:

```python
7

```

두 수 중 큰 값을 계속해서 누적 비교하여 최종 최댓값을 걸러낼 수도 있다.

---

### **(6) reduce()의 동작**

```python
numbers = [1, 2, 3, 4]

```

```python
reduce(
    lambda x, y: x + y,
    numbers
)

```

동작 결과

```python
단계 1: [1, 2] 연산 -> 1 + 2 = 3 (누적값 x가 됨)
단계 2: [3, 3] 연산 -> 3 + 3 = 6 (새로운 누적값 x가 됨)
단계 3: [6, 4] 연산 -> 6 + 4 = 10 (최종 반환)

```

↓

```python
10

```

---

### 정리

- reduce()는 요소를 누적 연산하여 단 하나의 최종 값을 만든다.
- `from functools import reduce`가 필요하다.
- 인자로 들어가는 함수는 반드시 2개의 매개변수(누적값, 현재값)를 가져야 한다.
- 초기값을 설정하면 연산의 시작점을 지정할 수 있고, 빈 객체 에러를 방지한다.
- 람다 함수와 조합하여 단순 반복 연산을 줄일 수 있다.
