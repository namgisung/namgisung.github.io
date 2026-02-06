---
layout: wiki
title: 힙(Heap)
wiki_name: c
parent: c/메모리
order: 3
---

# 힙(Heap)

힙(Heap)은 프로그램 실행 중(Runtime)에 **프로그래머의 요청에 의해 동적으로 할당되는 메모리 영역**이다.
주로 실행 중 크기가 결정되거나, 함수 호출 범위를 넘어 오래 유지되어야 하는 데이터를 저장하는 데 사용된다.

---

## 기본 개념

C 언어에서 힙 메모리는 운영체제가 관리하며, 프로그램은 표준 라이브러리 함수를 통해 힙 메모리를 요청하거나 반환한다.

* 프로그램 시작 시 크기가 고정되지 않음
* 실행 중 필요할 때마다 할당 가능
* 명시적으로 해제하지 않으면 메모리가 계속 유지됨

힙 메모리는 함수가 종료되어도 자동으로 사라지지 않으며, **프로그래머가 직접 수명(lifetime)을 관리**해야 한다.

---

## 힙 메모리 할당 함수

### malloc

```c
void *malloc(size_t size);
```

* 지정한 바이트 수만큼 메모리를 할당
* 할당된 메모리의 초기값은 **정의되지 않음(쓰레기 값)**
* 실패 시 `NULL` 반환

```c
int *p = (int *)malloc(sizeof(int));
```

---

### calloc

```c
void *calloc(size_t nmemb, size_t size);
```

* `nmemb × size` 만큼 메모리 할당
* 모든 비트를 0으로 초기화

```c
int *arr = (int *)calloc(10, sizeof(int));
```

---

### realloc

```c
void *realloc(void *ptr, size_t size);
```

* 기존에 할당된 메모리 크기를 변경
* 주소가 바뀔 수도 있음

```c
arr = realloc(arr, 20 * sizeof(int));
```

---

## 힙 메모리 해제

힙 메모리는 자동으로 반환되지 않으므로, 사용이 끝나면 반드시 `free`를 호출해야 한다.

```c
void free(void *ptr);
```

```c
free(p);
p = NULL;
```

* 해제 후 포인터를 `NULL`로 초기화하는 것이 안전함

---

## 힙 메모리의 특징

### 장점

* 큰 메모리 할당 가능
* 실행 중 크기 변경 가능
* 함수 호출 범위를 넘어 데이터 유지 가능

### 단점

* 할당/해제 속도가 느림
* 메모리 관리가 어려움
* 오류 발생 시 디버깅 난이도 높음

---

##  힙 관련 주요 오류

### 메모리 누수 (Memory Leak)

* 할당한 메모리를 `free`하지 않은 경우
* 프로그램 종료 전까지 메모리가 반환되지 않음

```c
int *p = malloc(sizeof(int));
// free(p); 누락
```

---

### 5.2 이중 해제 (Double Free)

```c
free(p);
free(p); // 오류
```

* 정의되지 않은 동작 발생
* 프로그램이 즉시 종료될 수 있음

---

### 댕글링 포인터 (Dangling Pointer)

```c
free(p);
*p = 10; // 이미 해제된 메모리 접근
```

* 매우 위험한 오류
* 예측 불가능한 결과 초래

---

## 스택(Stack)과 힙(Heap) 비교

| 구분    | 스택(Stack) | 힙(Heap)       |
| ----- | --------- | ------------- |
| 할당 방식 | 자동        | 수동 (`malloc`) |
| 해제 방식 | 자동        | 수동 (`free`)   |
| 속도    | 빠름        | 느림            |
| 크기    | 작음        | 큼             |
| 수명 관리 | 컴파일러      | 프로그래머         |

---

## 힙 사용 예시

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n;
    scanf("%d", &n);

    int *arr = malloc(n * sizeof(int));

    for (int i = 0; i < n; i++) {
        arr[i] = i * 2;
    }

    free(arr);
    return 0;
}
```

---

## 정리

힙은 유연하지만 위험한 메모리 영역이다.
C 언어에서 힙을 제대로 사용하려면 **할당과 해제를 항상 짝으로 관리하는 습관**이 필수적이다.
