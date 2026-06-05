---
layout: wiki
title: with 문
wiki_name: python
parent: python/파일입출력
order: 5
---

## **with 문**

with 문은 파일을 열고 사용이 끝나면 자동으로 close()를 호출하는 문법이다.

파일을 안전하게 관리할 수 있기 때문에 많이 사용된다.

---

### **(1) 기본 구조**

```python
with open("파일이름", "모드") as 파일객체:
    실행문
````

* open()으로 파일을 연다.
* as 뒤의 변수에 파일 객체가 저장된다.
* 블록이 끝나면 자동으로 close()가 호출된다.

---

### **(2) 파일 읽기**

```python
with open("test.txt", "r") as f:
    data = f.read()

print(data)
```

test.txt

```text
Hello
Python
```

결과:

```text
Hello
Python
```

---

### **(3) 파일 쓰기**

```python
with open("test.txt", "w") as f:
    f.write("Hello")
```

test.txt

```text
Hello
```

파일 저장 후 자동으로 close()가 호출된다.

---

### **(4) 반복문과 함께 사용**

```python
with open("test.txt", "r") as f:

    for line in f:
        print(line)
```

결과:

```text
Hello
Python
```

파일의 각 줄을 읽어 출력한다.

---

### **(5) close()와 비교**

기존 방식

```python
f = open("test.txt", "r")

data = f.read()

f.close()
```

with 문 사용

```python
with open("test.txt", "r") as f:
    data = f.read()
```

with 문은 close()를 직접 작성할 필요가 없다.

---

### **(6) 컨텍스트 매니저(Context Manager)**

with 문은 컨텍스트 매니저(Context Manager)를 사용한다.

컨텍스트 매니저는 특정 작업의 시작과 종료를 자동으로 관리하는 객체이다.

파일 객체는 컨텍스트 매니저를 지원한다.

```python
with open("test.txt", "r") as f:
    data = f.read()
```

컨텍스트 매니저는 내부적으로 다음 특수 메서드를 구현하고 있다.

```python
__enter__()
__exit__()
```

* `__enter__()` : with 블록 시작 시 호출
* `__exit__()` : with 블록 종료 시 호출

동작 순서

```text
1. __enter__()
2. 블록 실행
3. __exit__()
```

파일 객체의 경우 `__exit__()`에서 자동으로 `close()`가 호출된다.

따라서 파일을 사용한 후 직접 `close()`를 호출하지 않아도 된다.

---

### **(7) with 문을 사용하는 이유**

```python
with open("test.txt", "r") as f:
    data = f.read()
```

* 자동으로 close() 호출
* 코드가 간결함
* 파일을 안전하게 관리 가능
* 예외가 발생해도 파일이 정상적으로 닫힘

---

### 정리

* with 문은 파일을 자동으로 닫아준다.
* as를 사용하여 파일 객체를 저장한다.
* close()를 직접 호출할 필요가 없다.
* 컨텍스트 매니저를 사용한다.
* 컨텍스트 매니저는 `__enter__()`와 `__exit__()`를 구현한다.
* 파일 입출력에서 많이 사용된다.
