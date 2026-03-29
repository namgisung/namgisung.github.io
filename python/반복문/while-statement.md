---
layout: wiki
title: while문
wiki_name: python
parent: python/반복문
order: 1
---

## **while문**

while문은 반복문으로 조건식이 참이면 실행문을 반복해서 실행한다.

---

### **(1) 기본 구조**

while문의 구조는 아래와 같다

```python id="g7k2dp"
while 조건식:
    # 조건이 참이면 수행될 문장들
```

---

### **(2) 동작 순서**

while문의 실행 순서는 다음과 같다.

(1) 조건식이 참이면 들여쓰기된 블록으로 들어가고, 거짓이면 while문을 벗어난다.

(2) 실행문을 수행한 후 다시 조건식을 검사한다.

```python id="m2x9qd"
i = 1
while i <= 10:
    # 실행문
    i += 1
```

위의 예시는 실행문을 10번 반복한다.
원하면
👉 `for문`도 같은 스타일로 이어서 만들어줄게 😎
ㅍ
