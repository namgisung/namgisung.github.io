---
layout: wiki
title: continue문
wiki_name: c
parent: c
order: 9
---

## continue문

`continue`문은 **반복문 안에서만 사용**될 수 있으며,

반복이 진행 중 `continue`를 만나면 **이후의 실행문을 건너뛰고**

반복문의 **끝으로 이동하여 다음 반복을 수행**한다.

---

### **(1) 기본 개념**

* `continue` → 현재 반복 **중단**
  
* 반복문 자체는 종료 ❌
  
* 다음 반복으로 **바로 이동**

---

### **(2) for문에서의 continue**

```c
#include <stdio.h>

int main() {
    for (int i = 0; i <= 10; i++) {
        if (i % 3 == 0) {
            continue;
        }
        printf("%d\n", i);
    }
    return 0;
}
```

위 코드는 `i`가 **3의 배수일 때 continue문을 만나 출력하지 않고**,

3의 배수가 아닌 값만 출력한다.

---

### **(3) 동작 설명**

1. `i`가 3의 배수인지 검사

2. 3의 배수이면 `continue` 실행

3. `printf`를 건너뛰고 증감식(`i++`)으로 이동

4. 다음 반복 실행

---

## **(4) 주의사항**

* `continue`는 **가장 가까운 반복문**에만 적용된다.
  
* `while`문에서는 `continue` 사용 시 **증감식 위치에 주의**해야 한다.

```c
int i = 0;
while (i < 10) {
    i++;
    if (i % 2 == 0) {
        continue;
    }
    printf("%d\n", i);
}
```

증감식이 없으면 **무한 반복**이 발생할 수 있다.
