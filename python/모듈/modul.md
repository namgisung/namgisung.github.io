---
layout: wiki
title: 모듈
wiki_name: python
parent: python/모듈
order: 1
---

## **모듈(Module)**

모듈은 파이썬 코드를 담고 있는 파일(`*.py`)이다.

변수, 함수, 클래스 등을 모아두고 필요할 때마다 불러와 재사용하기 위해 사용한다.

---

### **(1) 기본 구조**

- **모듈 만들기**: 단순히 파이썬 파일(`파일명.py`)을 생성하고 내부에 함수나 변수를 정의하면 된다.
- **모듈 불러오기**: `import 파일명` 형식으로 불러와 내부에 정의된 기능을 사용한다.

코드의 가독성을 높이고, 유지보수를 쉽게 만들기 위해 필수적인 개념이다.

---

### **(2) 모듈 만들기 (math_tool.py)**

우선 다른 파일에서 불러와서 사용할 기준 모듈 파일(`math_tool.py`)을 생성한다.

```python
# math_tool.py

PI = 3.141592

def add(a, b):
    return a + b

def square(x):
    return x * x

```

자주 사용하는 상수와 함수를 파일 하나에 모아두었다.

---

### **(3) 모듈 사용하기 (main.py)**

위에서 만든 `math_tool.py`와 동일한 디렉토리(폴더)에 `main.py`를 만들고 모듈을 호출한다.

```python
# main.py
import math_tool

# 모듈 내 변수 사용
print(math_tool.PI)

# 모듈 내 함수 사용
result1 = math_tool.add(5, 3)
result2 = math_tool.square(4)

print(result1)
print(result2)

```

결과:

```python
3.141592
8
16

```

`모듈이름.기능` 형태로 접근하여 사용할 수 있다.

---

### **(4) 파이썬 표준 모듈 사용**

개발자가 직접 만들지 않아도 파이썬이 기본으로 제공하는 표준 모듈(내장 모듈)도 동일하게 사용할 수 있다.

```python
import math

print(math.factorial(5))

```

결과:

```python
120

```

---

### **(5) 모듈의 동작 원리**

`import` 명령어가 실행될 때 파이썬 내부에서 파일이 연결되는 구조이다.

```text
[ main.py ] 
    │
    ├── import math_tool  ──>  [ math_tool.py ]
    │                              ├── PI = 3.14
    │                              └── add(a, b)
    │
    └── math_tool.add(5, 3) ──> math_tool 내의 add() 호출

```

---

### 정리

- 모듈은 파이썬 함수와 변수 등을 모아놓은 하나의 파일(`*.py`)이다.
- `import 모듈이름`을 통해 불러와서 재사용할 수 있다.
- 불러온 모듈의 기능을 쓸 때는 `모듈이름.함수명()` 형태를 사용한다.
- 직접 만드는 모듈 외에도 파이썬 기본 제공 내장 모듈이 존재한다.
