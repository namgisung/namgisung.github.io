---
layout: wiki
title: for문
wiki_name: python
parent: python/반복문
order: 2
---

## **for문**

for문은 반복 횟수를 알고 있을 때 적합하다.
구조가 간단하며 직관적이라 이해하기 쉽다.

```python
for i in range(1, 6):
    print("yes")
```

위의 예시는 "yes"를 5번 출력한 것이다.

---

### **(1) 기본 구조**

for문의 구조는 다음과 같다

```python
for 변수 in 범위:
    # 실행문
```

---

### **(2) 동작 순서**

for문은 범위(range)에 따라 반복된다.

범위에서 값을 하나씩 꺼내 변수에 넣고,

실행문을 수행하는 과정을 반복한다.

```python id="d7c9wf"
for i in range(1, 6):
    print(i)
```

---

## range() 함수

Python에서는 반복 횟수를 `range()`로 지정한다.

```python
range(시작, 끝)
```

시작부터 끝-1까지 반복

```python id="p2r8sj"
range(1, 6)  # 1,2,3,4,5
```

---

## 💡 다양한 사용법

### (1) 0부터 시작

```python id="n1q7ye"
for i in range(5):
    print(i)
```

0 ~ 4 출력

---

### (2) 증가 간격 지정

```python id="u8k3mz"
for i in range(1, 10, 2):
    print(i)
```

1, 3, 5, 7, 9
