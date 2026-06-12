---
layout: wiki
title: import
wiki_name: python
parent: python/모듈
order: 2
---

## **import**

import는 이미 만들어진 파이썬 모듈(파일)을 현재 스크립트로 불러오는 키워드이다.

외부의 코드 자원을 가져와 내 코드에서 연결하여 쓸 때 사용한다.

---

### **(1) 기본 구조**

```python
import 모듈이름

```

* 모듈이름 : 불러올 파이썬 파일의 이름 (단, 확장자 `.py`는 제외하고 파일명만 입력)

하나의 스크립트에서 여러 개의 모듈을 불러올 수 있으며, 일반적으로 코드의 가장 최상단에 작성한다.

---

### **(2) 기본 사용법**

불러올 모듈 파일(`calc.py`)이 존재한다고 가정한다.

```python
# calc.py
def add(a, b):
    return a + b

```

이후 `main.py`에서 `calc` 모듈을 불러와 연산을 수행한다.

```python
# main.py
import calc

result = calc.add(10, 20)

print(result)

```

결과:

```python
30

```

`import`를 통해 파일 전체를 가져왔기 때문에, 내부 함수에 접근할 때 항상 `calc.`이라는 접두사를 붙여야 한다.

---

### **(3) 여러 모듈 한 번에 불러오기**

쉼표(`,`)를 사용하여 한 줄에 여러 모듈을 동시에 불러올 수 있다.

```python
import math, os, sys

print(math.pi)

```

결과:

```python
3.141592653589793

```

다만, PEP 8(파이썬 코드 스타일 가이드)에서는 가독성을 위해 한 줄에 하나씩 `import`하는 것을 권장한다.

```python
# 권장 규격
import math
import os
import sys

```

---

### **(4) 네임스페이스(Namespace) 보호**

`import` 방식은 현재 파일의 변수 공간(네임스페이스)과 불러온 모듈의 변수 공간을 엄격하게 분리한다.

```python
import calc

def add(a, b):
    return "현재 파일의 add 함수"

# 1. 현재 파일의 함수 호출
print(add(1, 2))

# 2. calc 모듈의 함수 호출
print(calc.add(1, 2))

```

결과:

```python
현재 파일의 add 함수
3

```

이름이 같은 함수가 존재하더라도 앞에 `calc.`이 붙기 때문에 충돌이 발생하지 않는다.

---

### **(5) import의 동작**

`import`가 일어날 때 파이썬이 모듈을 찾는 내부 순서이다.

```text
1. sys.modules (이미 메모리에 로드된 모듈인지 확인)
   ↓
2. built-in modules (파이썬 내장 표준 모듈인지 확인)
   ↓
3. sys.path (현재 디렉토리 및 파이썬 환경 변수에 등록된 폴더 검색)

```

현재 작성 중인 파일과 같은 폴더에 모듈 파일이 있어야 문제없이 import가 수행된다.

---

### 정리

- import는 외부 파이썬 파일(`.py`)을 가져오는 핵심 키워드이다.
- 모듈을 불러올 때는 확장자를 제외한 파일 이름만 명시한다.
- `모듈이름.함수()` 형태로 호출하므로 현재 파일의 변수/함수와 이름이 겹쳐도 안전하다.
- 관례상 코드의 가장 맨 위(최상단)에 모듈 호출문을 모아둔다.

