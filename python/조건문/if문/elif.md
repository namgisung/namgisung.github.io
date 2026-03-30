---
layout: wiki
title: elif
wiki_name: python
parent: python/조건문/if문
order: 3
---

## **elif**

그리고 2개 이상의 조건식이 있다면 elif를 써서
"만약 ~면 ~를 실행하고 그 조건이 아니라 ~라면 ~를 실행한다" 를 표현할 수 있다.

---

### **(1) 기본 구조**

```python
if 조건식:
    # 실행문
elif 조건식:
    # 실행문
else:
    # 실행문
```

```python id="p1k9sx"
c = 0
if c == 0:
    print(c)
elif c == 1:
    print("2")
else:
    print("3")
```

코드에서 elif문으로 c가 0이 아니라 1이면 2를 출력한다는 것을 표현한 것이다.
