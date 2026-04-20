---
layout: wiki
title: 기본값 매개변수
wiki_name: python
parent: python/함수
order: 5
---

## **기본값 매개변수**

매개변수에 기본값을 설정하면, 함수 호출 시 인자를 전달하지 않아도 기본값이 자동으로 사용된다.

---

### **(1) 기본 구조**

```python
def 함수이름(매개변수=기본값):
    # 실행문
```

---

### **(2) 기본 예제**

```python
def func(a, b=10):
    print(a, b)

func(5)       # b는 기본값 10 사용
func(5, 20)   # b에 20 전달
```

위의 코드에서 `b`는 기본값이 설정되어 있기 때문에, 인자를 전달하지 않으면 기본값이 사용된다.

---

### **(3) 여러 개의 기본값**

여러 개의 매개변수에 기본값을 설정할 수 있다.

```python
def func(a=1, b=2):
    print(a, b)

func()
func(10)
func(10, 20)
```

---

### **주의사항**

기본값 매개변수는 일반 매개변수 뒤에 작성해야 한다.

```python
def func(a, b=10):   # 가능
    pass
```

```python
def func(a=10, b):   # 오류
    pass
```
