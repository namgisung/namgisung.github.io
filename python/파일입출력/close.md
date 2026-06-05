---
layout: wiki
title: close()
wiki_name: python
parent: python/파일입출력
order: 4
---

## **close()**

close()는 열린 파일을 닫는 메서드이다.

파일 사용이 끝나면 close()를 호출하여 파일을 닫아주는 것이 좋다.

---

### **(1) 기본 사용**

```python
f = open("test.txt", "r")

f.close()
````

파일을 닫는다.

---

### **(2) 읽기 후 close()**

```python
f = open("test.txt", "r")

data = f.read()

print(data)

f.close()
```

파일을 읽은 후 닫는다.

---

### **(3) 쓰기 후 close()**

```python
f = open("test.txt", "w")

f.write("Hello")

f.close()
```

파일에 저장한 후 닫는다.

---

### **(4) close()를 사용하는 이유**

```python
f = open("test.txt", "r")
```

파일을 열기만 하고 닫지 않으면 시스템 자원이 계속 사용될 수 있다.

따라서 파일 사용이 끝나면 close()를 호출하는 것이 좋다.

---

### **(5) close() 확인**

```python
f = open("test.txt", "r")

print(f.closed)

f.close()

print(f.closed)
```

결과:

```text
False
True
```

* False : 파일이 열려 있음
* True : 파일이 닫혀 있음

---

### 정리

* close()는 열린 파일을 닫는다.
* 파일 사용이 끝나면 호출하는 것이 좋다.
* 파일을 닫으면 시스템 자원을 반환한다.
* 파일의 상태는 closed 속성으로 확인할 수 있다.
