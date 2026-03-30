---
layout: wiki
title: break문
wiki_name: python
parent: python
order: 8
---


## **break문**

break문은 현재 위치에서 가장 가까운 반복문을 빠져나온다.

---

### **(1) 기본 사용**

```python
sum = 0
i = 1

while True:
    if sum > 100:
        break
    sum += 1
    i += 1
```

위 코드는 sum이 100보다 커지면 break문이 실행되어 즉시 반복문을 빠져나온다.

---

## 특징

* 반복문(while, for)에서만 사용 가능하다.
* 조건을 만족하면 반복을 즉시 종료한다.

---

## for문에서 사용

```python
for i in range(1, 10):
    if i == 5:
        break
    print(i)
```

5가 되는 순간 반복 종료
