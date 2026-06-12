---
layout: wiki
title: import *
wiki_name: python
parent: python/모듈
order: 4
---

## **import \***

import *은 모듈 내부의 모든 변수, 함수, 클래스를 한 번에 현재 스크립트로 불러오는 키워드이다.

별표(`*`)는 애스터리스크(Asterisk)라고 하며, 와일드카드(Wildcard)로서 '모든 것'을 의미한다.

---

### **(1) 기본 구조**

```python
from 모듈이름 import *

```

모듈 안에 있는 수십, 수백 개의 기능을 개별적으로 적지 않고 전부 다 가져와 사용할 때 쓴다.

---

### **(2) 기본 사용법**

불러올 모듈 파일(`calc.py`)에 여러 기능이 있다고 가정한다.

```python
# calc.py
def add(a, b): return a + b
def sub(a, b): return a - b
def mul(a, b): return a * b
def div(a, b): return a / b

```

이후 `main.py`에서 `*`을 이용해 전체 기능을 한 번에 로드한다.

```python
# main.py
from calc import *

# 접두사 없이 모든 함수 사용 가능
print(add(10, 2))
print(sub(10, 2))
print(mul(10, 2))
print(div(10, 2))

```

결과:

```python
12
8
20
5.0

```

---

### **(3) import \*의 치명적인 단점 (사용을 권장하지 않는 이유)**

편리해 보이지만 실제 프로젝트에서는 사용을 지양(안티 패턴)해야 한다.

#### 1. 출처의 불분명함 (가독성 저하)

코드가 길어지거나 여러 모듈에서 `import *`를 쓰면, 현재 사용 중인 함수가 도대체 어느 모듈에서 정의된 것인지 추적하기가 매우 어려워진다.

#### 2. 네임스페이스 오염 및 충돌

서로 다른 모듈에 동일한 이름의 함수가 있을 경우, 나중에 `import *`한 모듈의 기능이 이전의 기능을 무조건 덮어쓰게 되어 의도치 않은 버그가 발생한다.

```python
from module_A import * # 내부에 close() 함수 있음
from module_B import * # 내부에 또 다른 close() 함수 있음

close()  # 과연 A와 B 중 어떤 close가 실행될지 예측하기 힘듦

```

---

### **(4) __all__을 이용한 무분별한 import 제한**

만약 모듈 제작자가 `import *`로 노출될 기능을 제한하고 싶다면, 모듈 내부에 `__all__`이라는 특수 변수를 정의하면 된다.

```python
# calc.py
__all__ = ['add', 'sub']  # *으로 가져올 수 있는 기능을 제한

def add(a, b): return a + b
def sub(a, b): return a - b
def mul(a, b): return a * b  # *으로 가져오기 불가능

```

```python
# main.py
from calc import *

print(add(1, 2))  # 정상 작동
print(mul(1, 2))  # NameError 발생 (가져오지 못함)

```

---

### **(5) 소스코드 연결 상태**

`import *`가 실행될 때 현재 파일의 변수 공간 상태이다.

```text
[ calc.py ] ─────── import * ───────> [ main.py (내부 공간) ]
  ├── add()                             ├── add()  (내포됨)
  ├── sub()                             ├── sub()  (내포됨)
  ├── mul()                             ├── mul()  (내포됨)
  └── div()                             └── div()  (내포됨)
                                      ※ 기존에 있던 동일 이름 기능은 소멸

```

---

### 정리

- import *은 모듈 내 모든 기능을 한 번에 현재 파일로 가져온다.
- 매번 함수 이름을 나열하지 않아도 되므로 일회성 테스트 코드를 짤 때는 편리하다.
- 지만 함수 출처가 불분명해지고 네임스페이스 충돌 위험이 커지므로 실무에서는 권장하지 않는다.
- 모듈 파일 내에 `__all__`을 지정하면 `import *`로 가져갈 수 있는 범위를 통제할 수 있다.
