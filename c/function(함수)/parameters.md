---
layout: wiki
title: 매개변수
wiki_name: c
parent: c/function(함수)
order: 3
---


# 매개변수

매개변수란 **함수를 호출할 때 외부로부터 값을 전달받기 위해**

함수 정의 시 괄호 `()` 안에 선언하는 변수이다.

C 언어에서 매개변수는 **함수 내부에서만 사용 가능한 지역변수**이다.

---

## 매개변수 기본 구조

### 함수 정의

```c
리턴타입 함수이름(자료형 변수명) {
    // 실행할 코드
}
```

### 함수 호출

```c
함수이름(값);
```

---

## 매개변수 사용 예제

```c
#include <stdio.h>

void printNum(int a) {   // 매개변수 a
    printf("%d\n", a);
}

int main(void) {
    printNum(10);        // 값 전달
    printNum(20);
    return 0;
}
```

* `printNum(10)` → `a = 10`
* `printNum(20)` → `a = 20`

---

## 여러 개의 매개변수

매개변수가 여러 개일 경우 `,`로 구분한다.

```c
#include <stdio.h>

void sum(int a, int b) {
    printf("%d\n", a + b);
}

int main(void) {
    sum(5, 10);
    return 0;
}
```

* 함수 호출 시 **순서와 자료형이 반드시 일치**해야 한다

---

## 매개변수 전달 방식 (중요❗)

### 값에 의한 전달 (Call by Value)

C 언어에서는 **기본적으로 값에 의한 전달**을 사용한다.

```c
#include <stdio.h>

void change(int x) {
    x = 100;
}

int main(void) {
    int a = 10;
    change(a);
    printf("%d\n", a);  // 10
    return 0;
}
```

함수 안에서 값을 변경해도 **원본 변수는 변하지 않는다**

이유:

* 매개변수는 **복사본**이기 때문

---

## 배열을 매개변수로 전달할 때

배열을 매개변수로 전달하면 **배열의 시작 주소가 전달된다.**

```c
#include <stdio.h>

void printArr(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
}

int main(void) {
    int a[3] = {1, 2, 3};
    printArr(a, 3);
    return 0;
}
```

* 배열 이름 = 배열의 시작 주소
* 그래서 배열을 수정하면 **원본 배열이 변경된다**

---

## 자바와의 차이

| Java     | C          |
| -------- | ---------- |
| 객체 참조 전달 | 값 전달이 기본   |
| 배열도 객체   | 배열은 메모리 주소 |
| 안전함      | 직접 관리 필요   |

