---
layout: wiki
title: 람다함수 (lambda)
wiki_name: python
parent: python/람다함수
order: 1
---

## **람다 함수(lambda)**

람다 함수(lambda)는 이름 없이 사용하는 익명 함수(Anonymous Function)이다.

간단한 함수를 한 줄로 작성할 수 있다.

---

### **(1) 기본 구조**

```python
lambda 매개변수 : 반환값
```

예시

```python
lambda x : x * 2
```

---

### **(2) 일반 함수와 비교**

일반 함수

```python
def square(x):
    return x * x

print(square(5))
```

결과:

```text
25
```

람다 함수

```python
square = lambda x: x * x

print(square(5))
```

결과:

```text
25
```

동일한 결과를 얻을 수 있다.

---

### **(3) 여러 매개변수**

```python
add = lambda x, y: x + y

print(add(3, 4))
```

결과:

```text
7
```

---

### **(4) 즉시 실행**

```python
print((lambda x: x * x)(5))
```

결과:

```text
25
```

람다 함수를 정의와 동시에 호출할 수 있다.

---

### **(5) sorted()와 함께 사용**

```python
students = [
    ("Kim", 90),
    ("Lee", 70),
    ("Park", 80)
]

result = sorted(
    students,
    key=lambda student: student[1]
)

print(result)
```

결과:

```python
[('Lee', 70), ('Park', 80), ('Kim', 90)]
```

람다 함수를 기준으로 정렬할 수 있다.

---

### **(8) 람다 함수의 특징**

- 이름이 없는 함수이다.
- 한 줄로 작성한다.
- return 키워드를 사용하지 않는다.
- 간단한 함수 작성에 적합하다.
- map(), filter(), sorted()와 자주 함께 사용된다.

---

### 정리

- 람다 함수는 익명 함수이다.
- `lambda 매개변수 : 반환값` 형태로 작성한다.
- 간단한 함수를 한 줄로 표현할 수 있다.
- map(), filter(), sorted()와 함께 자주 사용된다.
