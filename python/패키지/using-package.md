---
layout: wiki
title: 패키지 사용하기
wiki_name: python
parent: python/패키지
order: 2
---

## **패키지 사용하기**

패키지 사용하기는 폴더 구조로 계층화된 모듈의 자원을 다양한 키워드(`import`, `from`, `as`)를 조합하여 호출하는 방법이다.

프로젝트의 성격과 코드의 간결성을 고려하여 최적의 구문으로 패키지 내부 모듈에 접근할 때 활용한다.

---

### **(1) 대상 패키지 구조 가정**

본문 예제 코드는 다음과 같은 파일 시스템 구조를 기준으로 동작한다.

```text
graphics/              # 최상위 패키지 폴더
├── __init__.py
├── screen.py          # 모듈 (render() 함수 포함)
└── geometry/          # 하위(Sub) 패키지 폴더
    ├── __init__.py
    └── primitive.py   # 모듈 (draw_line() 함수 포함)

```

---

### **(2) import 키워드 사용 (기본 호출)**

가장 정석적인 방법으로, 가장 하위의 모듈까지 점(`.`)으로 연결하여 호출한다.

```python
import graphics.screen

# 호출 시 패키지 경로를 전부 다 적어주어야 함
graphics.screen.render()

```

* **주의점**: `import` 키워드 바로 뒤에는 무조건 **모듈**이나 **패키지** 이름만 올 수 있다. 모듈 내부의 특정 '함수'를 바로 `import` 뒤에 적으면 구문 에러(SyntaxError)가 발생한다.
```python
import graphics.screen.render  # 에러 발생!

```



---

### **(3) from ... import 키워드 사용 (간결한 호출)**

`from` 뒤에 패키지나 모듈 경로를 명시하면, `import` 뒤에 모듈은 물론 특정 함수나 변수까지 지정하여 가져올 수 있다. 앞에 긴 접두사를 붙이지 않아도 되어 가장 많이 애용된다.

#### 방법 A. 특정 모듈만 가져오기

```python
from graphics import screen

# 앞에 패키지명을 생략하고 모듈명부터 접근 가능
screen.render()

```

#### 방법 B. 모듈 안의 특정 함수 직접 가져오기

```python
from graphics.screen import render

# 모듈명도 생략하고 함수를 바로 호출 가능
render()

```

---

### **(4) 하위(Sub) 패키지 호출하기**

패키지 안에 또 다른 폴더(패키지)가 중첩되어 있는 계층 구조도 동일하게 점(`.`)을 이어 붙여 접근한다.

```python
# geometry 폴더 속 primitive.py 모듈 안의 draw_line 함수 호출
from graphics.geometry.primitive import draw_line

draw_line()

```

---

### **(5) as 키워드와 조합 (별명 부여)**

패키지 경로가 너무 깊거나 길어질 경우 `as`를 이용해 가명을 주어 호출 코드를 축약한다.

```python
import graphics.geometry.primitive as prim

# 긴 경로 대신 별칭으로 간결하게 사용
prim.draw_line()

```

---

### **(6) 패키지 호출 흐름 시각화**

경로를 지정해 들어갈 때 프로그램 내부적으로 타깃을 찾아내는 탐색 방향성이다.

```text
[from graphics.geometry.primitive import draw_line]

 graphics (최상위 폴더)
   ↓
 geometry (하위 폴더)
   ↓
 primitive.py (모듈 파일)
   ↓
 draw_line() (최종 함수 추출 ──> 메인 공간에 등록)

```

---

### 정리

- 패키지 내 모듈을 불러올 때는 하위 경로로 들어갈 때마다 점(`.`)을 찍어 구분한다.
- `import 패키지.모듈` 형식을 쓰면 호출할 때 경로를 풀네임으로 다 적어야 하므로 공간이 엄격히 분리된다.
- `from 패키지.모듈 import 함수` 형식을 쓰면 패키지명과 모듈명을 생략하고 함수를 다이렉트로 쓸 수 있어 코드가 깔끔해진다.
- 경로가 지나치게 깊어질 경우 `as` 키워드로 별명을 주어 가독성을 지킬 수 있다.
