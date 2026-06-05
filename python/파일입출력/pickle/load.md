---
layout: wiki
title: load()
wiki_name: python
parent: python/파일입출력/pickle
order: 2
---

## **load()**

load()는 pickle 파일에 저장된 객체를 불러오는 함수이다.

pickle 모듈을 사용한다.

---

### **(1) 기본 구조**

```python
pickle.load(파일객체)
```

- 파일객체 : 읽어올 pickle 파일

---

### **(2) 리스트 불러오기**

```python
import pickle

with open("data.pkl", "rb") as f:
    data = pickle.load(f)

print(data)
```

결과:

```text
[1, 2, 3, 4, 5]
```

파일에 저장된 리스트 객체를 복원한다.

---

### **(3) 딕셔너리 불러오기**

```python
import pickle

with open("student.pkl", "rb") as f:
    student = pickle.load(f)

print(student)
```

결과:

```python
{'name': 'kim', 'age': 20}
```

파일에 저장된 딕셔너리 객체를 복원한다.

---

### **(4) dump()와 함께 사용**

객체 저장

```python
import pickle

data = [1, 2, 3]

with open("data.pkl", "wb") as f:
    pickle.dump(data, f)
```

객체 복원

```python
import pickle

with open("data.pkl", "rb") as f:
    data = pickle.load(f)

print(data)
```

결과:

```text
[1, 2, 3]
```

---

### **(5) 바이너리 읽기 모드 사용**

```python
with open("data.pkl", "rb") as f:
    data = pickle.load(f)
```

pickle 파일은 바이너리 형식이므로 `"rb"` 모드를 사용한다.

- r : read
- b : binary

---

### **(6) dump()와 load() 비교**

| 함수 | 설명 |
|--------|--------|
| dump() | 객체를 파일에 저장 |
| load() | 파일에서 객체를 복원 |

---

### 정리

- load()는 pickle 파일의 객체를 불러온다.
- pickle 모듈을 사용한다.
- 객체의 형태를 그대로 복원할 수 있다.
- 파일은 `"rb"` 모드로 열어야 한다.
