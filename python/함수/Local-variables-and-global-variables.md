---
layout: wiki
title: 지역변수와 전역변수
wiki_name: python
parent: python/함수
order: 9
---

## **지역변수와 전역변수**

파이썬에서 변수는 선언된 위치에 따라 지역변수와 전역변수로 나뉜다.

---

### **(1) 지역변수 (Local Variable)**

지역변수는 함수 내부에서 선언된 변수로, 해당 함수 안에서만 사용할 수 있다.

```python
def func():
    x = 10   # 지역변수
    print(x)

func()
```

함수 외부에서는 접근할 수 없다.

```python
print(x)   # 오류 발생
```

---

### **(2) 전역변수 (Global Variable)**

전역변수는 함수 외부에서 선언된 변수로, 프로그램 전체에서 사용할 수 있다.

```python
x = 10   # 전역변수

def func():
    print(x)

func()
```

---

### **(3) 지역과 전역의 관계**

함수 내부에서 변수를 선언하면 해당 변수는 지역변수가 된다.
이 경우 전역변수와 이름이 같더라도 서로 다른 변수로 취급된다.

```python
x = 10

def func():
    x = 20   # 지역변수
    print(x)

func()
print(x)
```

출력:

```text
20
10
```

---

### **(4) global 키워드**

함수 내부에서 전역변수를 수정하려면 `global` 키워드를 사용해야 한다.

```python
x = 10

def func():
    global x
    x = 20

func()
print(x)   # 20
```
