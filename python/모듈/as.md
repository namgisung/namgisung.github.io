---
layout: wiki
title: as
wiki_name: python
parent: python/모듈
order: 5
---

## **as**

as는 모듈이나 함수를 불러올 때 사용자가 원하는 별명(Alias)을 부여하는 키워드이다.

이름이 너무 길어 코딩하기 불편하거나, 현재 스크립트 내의 다른 명칭과의 충돌을 피하고 싶을 때 사용한다.

---

### **(1) 기본 구조**

```python
import 모듈이름 as 별명
from 모듈이름 import 기능 as 별명

```

* 별명 : 원래 이름 대신 현재 파일 안에서 사용할 새로운 이름

`as`를 통해 별명을 지정한 이후에는, 원래의 모듈 이름이나 함수 이름은 현재 파일 내에서 더 이상 사용할 수 없다.

---

### **(2) 모듈 이름 축약하기 (기본 사용법)**

이름이 긴 외부 라이브러리나 모듈을 가져올 때 짧은 별칭을 주어 타자량을 줄인다.

```python
import datetime as dt

# 원래는 datetime.datetime.now()로 써야 함
now_time = dt.datetime.now()

print(now_time)

```

파이썬의 데이터 분석 라이브러리인 `pandas`를 `pd`로, `numpy`를 `np`로 줄여 쓰는 것이 대표적인 관례이다.

---

### **(3) 특정 함수 이름 축약하기**

`from import` 방식과 결합하여 가져오는 특정 기능에만 별명을 부여할 수도 있다.

```python
from math import square_root_function_name as sqrt

# 아주 긴 함수 이름을 단 4글자로 축약
result = sqrt(16)

print(result)

```

---

### **(4) 네임스페이스 충돌 방지**

현재 작업 중인 파일에 이미 존재하는 변수나 함수명이 모듈 내 기능과 동일할 때, `as`를 쓰면 덮어쓰기 현상을 완벽하게 방지할 수 있다.

```python
# 내 파일에 이미 구현된 add 함수
def add(a, b):
    return a + b

# 외부 모듈의 add 함수를 별명을 붙여 가져옴
from calculator_module import add as external_add

print(add(5, 5))          # 내가 만든 add 실행
print(external_add(5, 5)) # 외부에서 가져온 add 실행

```

서로 다른 두 모듈에서 똑같은 이름의 함수를 둘 다 가져와야 할 때도 유용하다.
(`from module_A import close as a_close`, `from module_B import close as b_close`)

---

### **(5) as 사용 시 공간 변화**

`as`를 선언하면 메모리상의 원래 이름과 연결되는 새로운 로컬 변수명(별명)이 맵핑되는 구조이다.

```text
[ 원래 모듈: datetime ]
        │
        ▼ (import datetime as dt 실행)
[ 현재 파일 변수 공간 ]
    dt ───────> datetime 모듈을 가리킴
    
    ※ 주의: 이 상태에서 datetime.now()를 호출하면 NameError가 발생함.
            반드시 지정한 별명인 dt로만 접근 가능.

```

---

### 정리

- as는 모듈이나 기능에 별명(Alias)을 붙여주는 키워드이다.
- 이름이 긴 모듈을 간결하게 축약하여 코드 생산성을 높일 수 있다.
- 이름이 똑같은 기능 간의 네임스페이스 충돌을 방지하는 안전장치 역할을 한다.
- 한 번 별명을 지정하면, 현재 스크립트 내에서는 원래 이름으로 호출할 수 없고 오직 별명으로만 호출해야 한다.
