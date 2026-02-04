---
layout: wiki
title: 함수 호출
wiki_name: c
parent: c/function(함수)
order: 2
---


# 함수 호출

함수 호출이란, **이미 정의된 함수를 실행시키는 것**을 말한다.

C 언어에서 함수는 **호출되었을 때만 실행**된다.

---

## 함수 호출 기본 구조

```c
함수이름(전달할_값);
```

또는 반환값이 있는 경우

```c
변수 = 함수이름(전달할_값);
```

---

## 함수 호출 예제

```c
#include <stdio.h>

void hello() {      // 함수 정의
    printf("Hello C\n");
}

int main(void) {
    hello();        // 함수 호출
    hello();
    return 0;
}
```

### 실행 결과

```
Hello C
Hello C
```

`hello()`가 호출될 때마다 함수 내부 코드가 실행된다.

---

## 반환값이 있는 함수 호출

```c
#include <stdio.h>

int sum(void) {
    return 10 + 20;
}

int main(void) {
    int result = sum();   // 함수 호출 + 반환값 저장
    printf("%d\n", result);
    return 0;
}
```

* `sum()` 함수 실행
* `return 30;`이 호출한 곳으로 전달됨
* 반환값을 변수에 저장하거나 바로 사용할 수 있음

---

## 함수 호출 흐름 (중요)

1. `main` 함수에서 함수 호출
2. 실행 흐름이 **호출된 함수로 이동**
3. 함수 내부 코드 실행
4. `return`을 만나면 호출한 위치로 복귀
5. 이후 코드 계속 실행

함수 호출은 **실행 흐름의 이동**이다.

---

## 함수 호출 시 주의사항

### (1) 함수는 먼저 정의되거나 선언되어야 한다

```c
int sum(int a, int b); // 함수 선언 (프로토타입)

int main(void) {
    printf("%d\n", sum(3, 5));
    return 0;
}

int sum(int a, int b) {  // 함수 정의
    return a + b;
}
```

* C에서는 **함수 호출 전에 함수가 알려져 있어야 한다**
* 그래서 함수 선언(프로토타입)을 사용한다

---

### (2) 함수 이름 뒤에는 반드시 `()`가 붙어야 한다

```c
sum;   // ❌ 함수 호출 아님
sum(); // ⭕ 함수 호출
```

* `()`가 있어야 함수가 실행된다
