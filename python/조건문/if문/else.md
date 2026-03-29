---
layout: wiki
title: else
wiki_name: python
parent: python/조건문/if문
order: 2
---

## **else**

만일 조건이 거짓이라면 if문의 실행문은 동작하지 않고 if문을 빠져나간다.

거짓일 때 다른 동작을 실행시키려면 else를 사용하면 된다.

---

### **(1) 기본 구조**

```python id="k2f8wz"
if 조건식:
    # 실행문
else:
    # 실행문
```

```python id="z8c1xq"
c = 0
if c == 0:
    print(c)
else:
    print("false")
```

이처럼 if문 뒤에 조건식을 쓰고 콜론(`:`)을 붙이며,

else에는 조건이 거짓일 때 실행할 코드를 작성한다.
