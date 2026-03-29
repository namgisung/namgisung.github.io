---
layout: wiki
title: continue문
wiki_name: python
parent: python
order: 9
---


## **continue문**

continue문은 반복문 내에서만 사용할 수 있으며,

반복이 진행 중에 continue문을 만나면 반복문의 끝으로 이동하여 다음 반복으로 넘어간다.

---

### **(1) 기본 사용**

```python id="m8v2kx"
for i in range(0, 11):
    if i % 3 == 0:
        continue
    print(i)
```

위 코드는 i가 3의 배수를 제외하고 출력하는 코드이다.
