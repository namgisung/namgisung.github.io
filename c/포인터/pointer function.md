---
layout: wiki
title: 함수 포인터
wiki_name: c
parent: c/포인터
order: 11
---

## 함수 포인터

**함수명은 함수 정의가 있는 메모리의 시작 위치**이다.
함수명이 주소이므로 **포인터에 저장**하면 함수를 다양한 방식으로 호출할 수 있다.

---

### (1) 함수 포인터 선언

```c
int (*fp)(int, int);   // 함수 포인터 선언
```

* 함수 포인터는 변수명 앞에 `*`를 붙여 포인터임을 표시한다
* 가리키는 함수의 형태를 **반환형과 매개변수**로 나누어 적는다
* **함수의 형태**는 매개변수의 개수와 자료형, 그리고 반환값의 자료형으로 정의된다. 함수 형태는 함수 선언에서 알 수 있고, 이것이 함수 포인터가 가리키는 형태이다
* **무조건 괄호로 묶어야 한다.** 괄호가 없으면 주소를 반환하는 함수의 선언이 된다

```c
int (*fp)(int, int);   // 함수 포인터
int *fp(int, int);     // int 포인터를 반환하는 함수 선언 (전혀 다른 의미)
```

---

### (2) 함수 포인터 사용

```c
#include <stdio.h>

int sum(int, int);         // 함수 선언

int main(void)
{
    int (*fp)(int, int);   // 함수 포인터 선언
    int res;               // 반환값을 저장할 변수

    fp = sum;              // 함수명을 함수 포인터에 저장
    res = fp(10, 20);      // 함수 포인터로 함수 호출
    printf("result : %d\n", res);   // 반환값 출력

    return 0;
}

int sum(int a, int b)      // 함수 정의
{
    return (a + b);
}
```

실행 결과

```
result : 30
```

* 함수 `sum`의 주소를 저장할 함수 포인터를 선언하고, `fp = sum;`으로 저장한다
* `fp`에는 **같은 형태의 함수를 여러 가지 넣었다 뺐다** 할 수 있다

---

### (3) 함수 포인터를 매개변수로 받는 함수 (선택적 호출)

함수 포인터를 매개변수로 받으면, **호출할 때 어떤 기능을 쓸지 골라서** 넘길 수 있다.

```c
#include <stdio.h>

void func(int (*fp)(int, int));      // 함수 포인터를 매개변수로 갖는 함수
int sum(int a, int b);               // 두 정수를 더하는 함수
int mul(int a, int b);               // 두 정수를 곱하는 함수
int max(int a, int b);               // 두 정수 중에 큰 값을 구하는 함수

int main(void)
{
    int sel;                         // 선택된 메뉴 번호를 저장할 변수

    printf("01 두 정수의 합\n");     // 메뉴 출력
    printf("02 두 정수의 곱\n");
    printf("03 두 정수 중에서 큰 값 계산\n");
    printf("원하는 연산을 선택하세요 : ");
    scanf("%d", &sel);               // 메뉴 번호 입력

    switch (sel)
    {
    case 1: func(sum); break;        // 1이면 func에 덧셈 기능 추가
    case 2: func(mul); break;        // 2이면 func에 곱셈 기능 추가
    case 3: func(max); break;        // 3이면 func에 큰 값 구하는 기능 추가
    }

    return 0;
}

void func(int (*fp)(int, int))
{
    int a, b;                        // 두 정수를 저장할 변수
    int res;                         // 함수의 반환값을 저장할 변수

    printf("두 정수의 값을 입력하세요 : ");
    scanf("%d%d", &a, &b);           // 두 정수 입력
    res = fp(a, b);                  // 함수 포인터로 가리키는 함수를 호출
    printf("결괏값은 : %d\n", res);  // 반환값 출력
}

int sum(int a, int b)        // 덧셈 함수
{
    return (a + b);
}

int mul(int a, int b)        // 곱셈 함수
{
    return (a * b);
}

int max(int a, int b)        // 큰 값을 구하는 함수
{
    if (a > b) return a;
    else return b;
}
```

실행 예 (1번 선택, 3과 4 입력)

```
01 두 정수의 합
02 두 정수의 곱
03 두 정수 중에서 큰 값 계산
원하는 연산을 선택하세요 : 1
두 정수의 값을 입력하세요 : 3 4
결괏값은 : 7
```

* `func`는 하나인데, 넘겨준 함수(`sum`, `mul`, `max`)에 따라 **동작이 달라진다**
* 세 함수는 매개변수 `(int, int)`와 반환형 `int`로 **형태가 같아서** 같은 함수 포인터로 받을 수 있다
