---
layout: wiki
title: 함수와 포인터
wiki_name: c
parent: c/포인터
order: 7
---

## 함수와 포인터

C언어에서 함수와 포인터를 함께 사용하는 이유는 **함수 호출 이후에도 원본 데이터를 직접 다루기 위해서**이다.

C언어의 함수는 기본적으로 **값에 의한 전달(Call by Value)** 방식을 사용한다.

즉, 일반 변수를 매개변수로 전달하면 함수 내부에서는 **복사본**을 사용하게 된다.

하지만 **포인터를 매개변수로 사용하면 변수의 주소를 전달**하게 되고,

함수 내부에서 원본 변수에 직접 접근하여 값을 변경할 수 있다.

---

### 포인터를 매개변수로 사용하는 함수

#### 정의

함수의 매개변수로 포인터를 사용하면,

→ 함수 내부에서 호출한 쪽 변수의 값을 직접 수정할 수 있다.

#### 형식

```c
반환형 함수이름(자료형 *매개변수)
```

#### 예제

```c
#include <stdio.h>

void change(int *a) {
    *a = 100;
}

int main() {
    int x = 10;
    change(&x);
    printf("%d", x);
    return 0;
}
```

#### 실행 결과

```
100
```

---

### 값 전달 vs 포인터 전달

#### 값 전달 (Call by Value)

```c
void func(int a) {
    a = 10;
}
```

* 함수 내부에서 값 변경
* 원본 변수에는 영향 없음

#### 포인터 전달

```c
void func(int *a) {
    *a = 10;
}
```

* 주소를 통해 접근
* 원본 변수 값 변경 가능

---

### 배열과 함수

배열 이름은 함수로 전달될 때 **배열의 첫 번째 요소의 주소**로 전달된다.

따라서 배열 매개변수는 포인터와 동일하게 동작한다.

#### 형식

```c
void func(int arr[], int size)
void func(int *arr, int size)
```

#### 예제

```c
#include <stdio.h>

void printArray(int *arr, int size) {
    for(int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
}

int main() {
    int a[3] = {1, 2, 3};
    printArray(a, 3);
    return 0;
}
```
