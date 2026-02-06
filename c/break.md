---
layout: wiki
title: break문
wiki_name: c
parent: c
order: 8
---


## break문

`break`문은 **현재 위치에서 가장 가까운 반복문이나 switch문을 즉시 빠져나올 때** 사용한다.

---

### **(1) 기본 개념**

`break`가 실행되면

→ 남은 반복은 무시되고

→ 반복문 또는 `switch`문을 **즉시 종료**한다.

---

### **(2) 반복문에서의 break**

```c
int sum = 0;
int i = 1;

while (1) {   // C언어에서는 true 대신 1 사용
    if (sum > 100) {
        break;
    }
    sum += 1;
    i++;
}
```

위 코드는 `sum`이 **100보다 커지는 순간**

`break`문이 실행되어 **즉시 while문을 빠져나간다.**

---

## **(3) switch문에서의 break**

`switch`문에서 `break`는

해당 `case`를 실행한 뒤 **switch문을 종료**하는 역할을 한다.

```c
int n = 2;

switch (n) {
    case 1:
        printf("1\n");
        break;
    case 2:
        printf("2\n");
        break;
    default:
        printf("default\n");
}
```

`break`가 없으면 다음 `case`까지 **계속 실행(fall-through)** 되므로

원하는 동작을 위해 보통 `break`를 넣어준다.

---

## **(4) 주의사항**

* `break`는 **가장 가까운** 반복문 또는 `switch`문만 빠져나온다.
* 중첩된 반복문에서는 **바깥 반복문까지는 빠져나오지 않는다.**

```c
while (1) {
    for (int i = 0; i < 5; i++) {
        break;  // for문만 종료됨
    }
}
```
