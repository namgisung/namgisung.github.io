---
layout: wiki
title: 변수
wiki_name: python
parent: python
order: 2
---

**(1) 기본 구조**

```python
a = 10
````

이런 식으로 변수 이름에 값을 대입하여 변수를 선언한다.
파이썬은 변수 선언 시 **자료형을 명시하지 않는다**.

값에 따라 자료형이 자동으로 결정된다.

```python
b = "hello"
c = 3.14
```

---

**(2) 변수 초기화**

파이썬에서는 변수를 선언함과 동시에 반드시 값을 넣어야 한다.

```python
x = 5
y = x
```

아직 값이 정해지지 않은 변수는 사용할 수 없다.

---

**(3) 형 변환 (Type Casting)**

변수의 타입을 바꾸고 싶을 경우
`int()`, `float()`, `str()` 등을 사용해 **명시적으로 형 변환**해야 한다.

```python
input_value = "3.14"
num = float(input_value)
print(num)
```

```python
value = 3.14
int_value = int(value)
print(int_value)  # 3
```

※ 실수를 정수로 변환하면 소수점 아래 값은 버려진다.

---

**(4) 변수 자료형 종류**

논리형: bool

* `True`, `False`
* 조건문과 논리 연산에 사용

```python
flag = True
```

문자열: str

* 문자 또는 문자열 저장
* 따옴표 `' '` 또는 `" "` 사용

```python
ch = 'A'
text = "Hello"
```

정수형: int

* 정수 값 저장

```python
num = 10
```

실수형: float

* 소수점을 가지는 실수

```python
pi = 3.14
```

---

※ 파이썬에는 `char` 타입이 존재하지 않으며
한 글자도 문자열(`str`)로 처리된다.

