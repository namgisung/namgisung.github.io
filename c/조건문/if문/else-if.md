---
layout: wiki
title: else if
wiki_name: c
parent: c/조건문/if문
order: 3
---

## else if 조건문

그리고 **2개 이상의 조건식이 있다면** `else if`를 써서
**“만약 ~라면 ~를 실행하고, 그게 아니라 ~라면 ~를 실행한다”** 를 표현할 수 있다.

---

### **(1) 기본 구조**

```c
if (조건식) {
    // 실행문
}
else if (조건식) {
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
    else if (c == 1) {
        printf("2\n");
    }
    else {
        printf("3\n");
    }

    return 0;
}
```

---

### **(3) 코드 설명**

* `if (c == 0)`
  → c가 0이면 `c` 값을 출력한다.

* `else if (c == 1)`
  → 위 조건이 거짓이고, c가 1이면 `"2"`를 출력한다.

* `else`
  → 위의 모든 조건이 거짓일 경우 `"3"`을 출력한다.

즉 이 코드는

> **c가 0이면 c 출력,
> c가 1이면 2 출력,
> 그 외의 값이면 3 출력**

을 표현한 것이다.
