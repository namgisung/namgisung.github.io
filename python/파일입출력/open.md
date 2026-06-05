---
layout: wiki
title: open()
wiki_name: python
parent: python/파일입출력
order: 1
---

## **open()**

open() 함수는 파일을 열기 위해 사용하는 함수이다.

파일을 읽거나 쓰기 전에 반드시 파일을 열어야 한다.

---

### **(1) 기본 구조**

```python
파일객체 = open("파일이름", "모드")
````

* 파일이름 : 열 파일의 경로
* 모드 : 파일 사용 방식

---

### **(2) 읽기 모드**

```python
f = open("test.txt", "r")
```

파일을 읽기 위해 연다.

---

### **(3) 쓰기 모드**

```python
f = open("test.txt", "w")
```

파일에 내용을 작성하기 위해 연다.

---

### **(4) 추가 모드**

```python
f = open("test.txt", "a")
```

파일 끝에 내용을 추가하기 위해 연다.

---

### **(5) 읽기/쓰기 모드**

```python
f = open("test.txt", "r+")
```

파일을 읽고 쓸 수 있다.

---

### **(6) 파일 객체 확인**

```python
f = open("test.txt", "r")

print(f)
```

결과:

```text
<_io.TextIOWrapper name='test.txt' mode='r' encoding='UTF-8'>
```

open()은 파일 객체를 반환한다.

---

### **(7) 사용 후 close()**

```python
f = open("test.txt", "r")

f.close()
```

파일 사용이 끝나면 close()로 닫아주는 것이 좋다.

---

### 정리

* open()은 파일을 여는 함수이다.
* 파일 객체를 반환한다.
* 파일을 읽거나 쓰기 전에 반드시 사용한다.
* 사용이 끝나면 close()를 호출한다.
