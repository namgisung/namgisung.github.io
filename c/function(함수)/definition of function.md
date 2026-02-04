---
layout: wiki
title: 함수의 정의
wiki_name: c
parent: c/function(함수)
order: 1
---


# 함수 (Function)

## 함수의 정의

C 언어에서 **함수(function)** 란

특정 작업을 수행하는 코드들을 하나로 묶은 실행 단위이다.

함수를 사용하면

* 반복되는 코드를 줄일 수 있고
* 프로그램을 구조적으로 만들 수 있으며
* 유지보수가 쉬워진다.

---

## 함수의 기본 구조 (정의)

C 언어에서 함수의 기본 구조는 다음과 같다.

```c
리턴타입 함수이름(매개변수) {
    // 실행할 코드
    return 반환값; // 리턴 타입이 void일 경우 생략 가능
}
```

### 각 구성 요소 설명

* **리턴 타입**
  
  함수가 실행을 마친 후 반환하는 값의 자료형
  
  (예: `int`, `double`, `char`, `void` 등)

* **함수 이름**
  
  함수를 호출할 때 사용하는 이름

* **매개변수**
  
  함수가 외부로부터 값을 전달받기 위해 사용하는 변수

* **return 문**
  
  함수 실행을 종료하고 값을 호출한 곳으로 반환

---

## main 함수

C 언어에서 `main` 함수는 **프로그램의 시작점**이다.

```c
int main(void) {
    // 실행할 코드
    return 0;
}
```

* 프로그램이 실행되면 **가장 먼저 main 함수가 호출**된다
* `main` 함수가 없으면 프로그램은 실행될 수 없다
* `return 0;`은 프로그램이 **정상 종료**되었음을 의미한다

---

## void 함수

`void` 함수는 **반환값이 없는 함수**이다.

주로 **어떤 동작을 수행하기만 할 때** 사용된다.

```c
#include <stdio.h>

void hello() {   // void 함수 정의
    printf("Hello World!!\n");
}

int main(void) {
    hello(); // 함수 호출
    hello();
    hello();
    return 0;
}
```

### 실행 결과

```
Hello World!!
Hello World!!
Hello World!!
```

`void` 함수는 **결과를 돌려주지 않고**,

코드를 불러와서 실행하는 용도로 사용된다.

---

## 반환값이 있는 함수

반환값이 있는 함수는

함수 내부에서 계산한 결과를 `return`을 통해 돌려준다.

```c
#include <stdio.h>

int div(void) {
    int a = 10, b = 5;
    int result = a / b;
    return result;   // 값 반환
}

int main(void) {
    printf("%d\n", div()); // 함수 호출 및 반환값 사용
    return 0;
}
```

* `int div(void)` → 반환값의 자료형은 `int`
* `return result;` → 함수 호출 위치로 값 전달

지금 위키 구성, 진짜 잘 가고 있다 🔥
다음 파트 바로 갈까?
