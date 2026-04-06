---
layout: wiki
title: 가변객체
wiki_name: python
parent: python/함수
order: 7
---

## **가변 인자와 키워드 가변 인자**

함수에 전달되는 인자의 개수가 정해져 있지 않을 때는 가변 인자를 사용한다.
또한 키워드 형태의 인자를 여러 개 받을 때는 키워드 가변 인자를 사용한다.

---

### **(1) 가변 인자 (*args)**

가변 인자는 여러 개의 위치 인자를 받을 때 사용한다.
전달된 값은 튜플(tuple) 형태로 저장된다.

```python
def func(*args):
    print(args)

func(1, 2, 3)
```

출력:

```text
(1, 2, 3)
```

---

### **(2) 키워드 가변 인자 (**kwargs)**

키워드 가변 인자는 여러 개의 키워드 인자를 받을 때 사용한다.
전달된 값은 딕셔너리(dict) 형태로 저장된다.

```python
def func(**kwargs):
    print(kwargs)

func(name="kim", age=20)
```

출력:

```text
{'name': 'kim', 'age': 20}
```

---

### **(3) 함께 사용**

가변 인자와 키워드 가변 인자는 함께 사용할 수 있다.

```python
def func(*args, **kwargs):
    print(args)
    print(kwargs)

func(1, 2, a=10, b=20)
```

---

### **(4) 리스트와 딕셔너리 전달**

리스트와 딕셔너리는 각각 `*`, `**`를 사용하여 전달할 수 있다.

```python
arr = [1, 2, 3]
dic = {"a": 10, "b": 20}

def func(*args, **kwargs):
    print(args)
    print(kwargs)

func(*arr, **dic)
```

---

### **주의사항**

함수 정의 시 인자의 순서는 다음과 같다.

```python 
def func(a, b=10, *args, **kwargs):
    pass
```

1. 일반 매개변수
2. 기본값 매개변수
3. *args
4. **kwargs
