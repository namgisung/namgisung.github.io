---
layout: wiki
title: else
wiki_name: java
parent: java/조건문/if문
order: 2
---


## else 조건문

만일 조건이 **거짓(false)** 이라면 중괄호 `{}` 안에 있는 실행문은 동작하지 않고 `if`문을 빠져나간다.

조건이 **거짓일 때 다른 동작을 수행하고 싶다면** `else`를 사용하면 된다.

---

### **(1) 기본 구조**

```c
if (조건식) {
    // 실행문
}
else {
    // 실행문
}
```

---

### **(2) 예제 코드**

```c
#include <stdio.h>

int main() {
    int c = 0;

    if (c == 0) {
        printf("%d\n", c);
    }
    else {
        printf("false\n");
    }

    return 0;
}
```

---

### **(3) 코드 설명**

* `if (c == 0)`

  → c가 0이면 `c` 값을 출력한다.

* `else`

  → 위 조건이 거짓일 경우 `"false"`를 출력한다.

즉 이 코드는

> **c가 0이면 c 출력,

> 그렇지 않으면 false 출력**

을 의미한다.
