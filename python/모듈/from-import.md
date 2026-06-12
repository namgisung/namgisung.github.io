---
layout: wiki
title: from import
wiki_name: python
parent: python/모듈
order: 3
---

## **from import**

from import는 모듈에서 전체가 아닌 특정 변수, 함수, 클래스만 골라서 현재 스크립트로 불러오는 키워드이다.

모듈 이름을 매번 앞에 붙이지 않고, 가져온 기능을 직접 호출하여 사용하고 싶을 때 쓴다.

---

### **(1) 기본 구조**

```python
from 모듈이름 import 가져올기능

```

* 모듈이름 : 기능을 가져올 대상 파이썬 파일명
* 가져올기능 : 모듈 내부에 정의된 변수, 함수, 클래스 이름

여러 개의 기능을 동시에 가져오고 싶다면 쉼표(`,`)를 사용하여 나열할 수 있다.

---

### **(2) 기본 사용법**

불러올 모듈 파일(`calc.py`)의 구조가 다음과 같다고 가정한다.

```python
# calc.py
def add(a, b):
    return a + b

def sub(a, b):
    return a - b

```

이후 `main.py`에서 `add` 함수만 콕 집어서 가져온다.

```python
# main.py
from calc import add

# calc.add()가 아니라 바로 add()로 사용 가능
result = add(5, 3)

print(result)

```

결과:

```python
8

```

가져오지 않은 `sub(5, 3)`을 호출하면 현재 스크립트에서는 인식하지 못하므로 에러가 발생한다.

---

### **(3) 여러 기능 한 번에 가져오기**

쉼표(`,`)로 구분하여 하나의 모듈에서 필요한 여러 요소를 한 번에 로드할 수 있다.

```python
# main.py
from calc import add, sub

print(add(10, 5))
print(sub(10, 5))

```

결과:

```python
15
5

```

---

### **(4) 네임스페이스 충돌 위험**

`from import` 방식은 가져온 기능을 현재 파일의 변수 공간(네임스페이스)에 그대로 등록한다. 따라서 현재 파일에 이름이 같은 기능이 있다면 덮어쓰기가 발생하므로 주의해야 한다.

```python
# main.py
from calc import add

# 현재 파일에서 동일한 이름의 함수 정의
def add(a, b):
    return "내가 만든 add 함수"

# 나중에 정의된 함수가 이전의 import 내용을 덮어씀
print(add(1, 2))

```

결과:

```python
내가 만든 add 함수

```

---

### **(5) import와 from import의 차이**

두 방식의 호출 형태와 코드 내부적인 연결 차이점이다.

```text
[ import calc ]
현재 파일 ──> calc.add() 호출 (공간이 분리되어 안전함)

[ from calc import add ]
현재 파일 ──> add() 바로 호출 (내부 변수처럼 쓰이지만 충돌 위험 있음)

```

---

### 정리

- from import는 모듈 내의 특정 기능만 지정하여 현재 공간으로 가져온다.
- 호출할 때 앞에 `모듈이름.`을 생략하고 함수 이름만으로 바로 사용할 수 있어 코드가 간결해진다.
- 현재 파일에 존재하는 변수나 함수와 이름이 겹치면 기존 코드가 덮어씌워질 위험이 있다.
- 가독성과 충돌 방지를 위해 명확하게 필요한 기능만 나열해서 쓰는 것을 권장한다.
