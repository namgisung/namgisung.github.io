---
layout: wiki
title: match문
wiki_name: python
parent: python/조건문
order: 2
---

## **match문**

if문은 조건식이 많아질수록 복잡해지고 처리해야 할 조건이 많아진다.

이와 달리 match문은 하나의 값에 대해 여러 경우를 비교하여 간결하게 처리할 수 있다.

---

### **(1) match문 기본구조**

```python
match 변수:
    case 값1:
        # 변수의 값이 값1일 때 실행
    case 값2:
        # 변수의 값이 값2일 때 실행
    case _:
        # 어떤 값과도 일치하지 않을 때 실행
```

```python
x = 2

match x:
    case 1:
        print("1입니다")
    case 2:
        print("2입니다")
    case _:
        print("기타 값")
```

---

### **(2) match문 동작 순서**

match문은 먼저 변수를 검사한 후,

위에서부터 순서대로 case를 비교한다.

일치하는 case가 나오면 해당 코드가 실행되고,

자동으로 match문을 빠져나간다. (break 필요 없음)

---

### **(3) match문 특징**

#### (1) default → case _

```python
case _:
```

모든 경우를 처리하는 기본값 역할

---

#### (2) 다양한 값 비교 가능

```python
x = "apple"

match x:
    case "apple":
        print("사과")
    case "banana":
        print("바나나")
```
