---
layout: wiki
title: dump()
wiki_name: python
parent: python/파일입출력/pickle
order: 2
---

## **dump()**

dump()는 파이썬 객체를 파일에 저장하는 함수이다.

pickle 모듈을 사용한다.

---

### **(1) 기본 구조**

```python
pickle.dump(객체, 파일객체)
```

- 객체 : 저장할 데이터
- 파일객체 : 저장할 파일

---

### **(2) 리스트 저장**

```python
import pickle

data = [1, 2, 3, 4, 5]

with open("data.pkl", "wb") as f:
    pickle.dump(data, f)
```

리스트 객체를 파일에 저장한다.

---

### **(3) 딕셔너리 저장**

```python
import pickle

student = {
    "name": "kim",
    "age": 20
}

with open("student.pkl", "wb") as f:
    pickle.dump(student, f)
```

딕셔너리 객체를 파일에 저장한다.

---

### **(4) 왜 사용하는가?**

일반 파일 저장

```python
f.write(str(data))
```

`문자열로 저장된다.`

pickle 저장

```python
pickle.dump(data, f)
```

`객체 자체가 저장된다.`

---

### **(5) 바이너리 모드 사용**

```python
with open("data.pkl", "wb") as f:
    pickle.dump(data, f)
```

pickle은 바이너리 형식으로 저장하므로 `"wb"` 모드를 사용한다.

- w : write
- b : binary

---

### 정리

- dump()는 객체를 파일에 저장한다.
- pickle 모듈을 사용한다.
- 객체의 형태를 유지한 채 저장할 수 있다.
- 파일은 "wb" 모드로 열어야 한다.
