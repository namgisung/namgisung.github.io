---
layout: wiki
title: write()
wiki_name: python
parent: python/파일입출력
order: 3
---

## **write()**

write()는 파일에 내용을 작성하는 메서드이다.

파일은 쓰기 모드("w"), 추가 모드("a"), 또는 읽기/쓰기 모드("r+")로 열어야 한다.

---

### **(1) write()**

문자열을 파일에 저장한다.

```python
f = open("test.txt", "w")

f.write("Hello")

f.close()
````

test.txt

```text
Hello
```

---

### **(2) 여러 번 write()**

```python
f = open("test.txt", "w")

f.write("Hello\n")
f.write("Python\n")
f.write("World")

f.close()
```

test.txt

```text
Hello
Python
World
```

---

### **(3) write()의 반환값**

write()는 저장한 문자 수를 반환한다.

```python
f = open("test.txt", "w")

count = f.write("Hello")

print(count)

f.close()
```

결과:

```text
5
```

---

### **(4) append 모드와 함께 사용**

```python
f = open("test.txt", "a")

f.write("\nPython")

f.close()
```

기존 파일

```text
Hello
```

결과

```text
Hello
Python
```

파일 끝에 내용이 추가된다.

---

### **(5) 숫자는 문자열로 변환 필요**

```python
f = open("test.txt", "w")

f.write(str(100))

f.close()
```

write()는 문자열만 저장할 수 있다.

---

### **(6) writelines()**

문자열 리스트를 한 번에 저장한다.

```python
f = open("test.txt", "w")

data = ["Hello\n", "Python\n", "World"]

f.writelines(data)

f.close()
```

test.txt

```text
Hello
Python
World
```

---

### **(7) write()와 writelines() 비교**

| 메서드          | 설명         |
| ------------ | ---------- |
| write()      | 문자열 하나 저장  |
| writelines() | 문자열 리스트 저장 |

---

## 정리

* write()는 문자열을 파일에 저장한다.
* write()는 저장한 문자 수를 반환한다.
* 숫자는 str()로 변환 후 저장해야 한다.
* writelines()는 문자열 리스트를 저장한다.
* 파일은 "w", "a", "r+" 모드에서 사용할 수 있다.
