---
layout: wiki
title: read()
wiki_name: python
parent: python/파일입출력
order: 2
---

## **read()**

read()는 파일의 내용을 읽어오는 메서드이다.

파일은 읽기 모드("r")로 열어야 한다.

---

### **(1) read()**

파일 전체 내용을 문자열로 읽어온다.

```python
f = open("test.txt", "r")

data = f.read()

print(data)

f.close()
````

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

## **(2) readline()**

한 줄만 읽어온다.

```python
f = open("test.txt", "r")

line = f.readline()

print(line)

f.close()
```

test.txt

```text
Hello
Python
```

결과:

```text
Hello
```

readline()을 여러 번 호출하면 다음 줄을 읽는다.

```python
f = open("test.txt", "r")

print(f.readline())
print(f.readline())

f.close()
```

결과:

```text
Hello

Python
```

---

### **(3) readlines()**

모든 줄을 리스트로 읽어온다.

```python
f = open("test.txt", "r")

data = f.readlines()

print(data)

f.close()
```

test.txt

```text
Hello
Python
```

결과:

```python
['Hello\n', 'Python']
```

각 줄이 리스트의 요소로 저장된다.

---

### **(4) 반복문과 함께 사용**

```python
f = open("test.txt", "r")

for line in f:
    print(line)

f.close()
```

결과:

```text
Hello
Python
```

파일의 각 줄을 순서대로 읽는다.

---

### **(5) read(), readline(), readlines() 비교**

| 메서드         | 반환형       | 설명            |
| ----------- | --------- | ------------- |
| read()      | 문자열(str)  | 파일 전체 읽기      |
| readline()  | 문자열(str)  | 한 줄 읽기        |
| readlines() | 리스트(list) | 모든 줄을 리스트로 읽기 |

---

## 정리

* read()는 파일 전체를 읽는다.
* readline()은 한 줄씩 읽는다.
* readlines()는 모든 줄을 리스트로 반환한다.
* 파일은 읽기 모드("r")로 열어야 한다.
