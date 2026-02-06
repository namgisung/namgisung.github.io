---
layout: wiki
title: malloc
wiki_name: c
parent: c/동적-메모리-할당
order: 1
---

## malloc

`malloc`은 **프로그램 실행 중(Runtime)에 필요한 만큼 메모리를 힙(Heap) 영역에 할당**해주는 함수이다.

* `malloc`은 **Memory Allocation**의 약자
* 필요한 메모리 크기를 **바이트(byte)** 단위로 지정
* 할당된 메모리의 **시작 주소를 반환**
* 반환 타입은 `void*` 이므로 **형 변환이 필요**

동적 메모리 할당이란

→ **컴파일 시점이 아니라 실행 중에 메모리를 확보하는 방식**

---

### malloc 기본 형식

```c
포인터 = (자료형*)malloc(메모리크기);
```

---

### malloc 사용 예제 (정수 1개)

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* p = (int*)malloc(sizeof(int));

    *p = 10;
    printf("%d\n", *p);

    free(p);
    return 0;
}
```

#### 설명

* `sizeof(int)` → int 하나 크기만큼 메모리 요청
* `malloc` → 힙 영역에 메모리 할당
* `p` → 할당된 메모리의 시작 주소
* `*p` → 해당 메모리에 값 저장

---

### 배열처럼 malloc 사용하기

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* arr = (int*)malloc(sizeof(int) * 5);

    for (int i = 0; i < 5; i++) {
        arr[i] = i + 1;
    }

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }

    free(arr);
    return 0;
}
```

동적 배열 생성

→ **배열 크기를 실행 중에 결정 가능**

---

### malloc의 특징

* 힙(Heap) 영역에 메모리 할당
* 크기를 직접 지정해야 함
* 초기값이 **정해져 있지 않음** (쓰레기 값)
* 사용 후 반드시 `free()`로 해제해야 함

---

### malloc 실패 시 (NULL 반환)

메모리가 부족하면 `malloc`은 `NULL`을 반환한다.

```c
int* p = (int*)malloc(sizeof(int));

if (p == NULL) {
    printf("메모리 할당 실패\n");
    return 1;
}
```

**NULL 체크는 필수 습관**

---

### malloc과 sizeof의 관계

```c
int* p = (int*)malloc(sizeof(int) * 10);
```

이 코드는 다음 의미이다.

```c
// int 10개를 저장할 수 있는 메모리 공간 확보
```

---

### malloc 사용 시 주의점

초기화되지 않는다

```c
int* p = (int*)malloc(sizeof(int));
printf("%d\n", *p); // 쓰레기 값
```

반드시 값 할당 후 사용

---

free 하지 않으면 메모리 누수 발생

```c
malloc(...);
// free 안 하면 힙에 메모리 남음
```

사용 후 `free()` 필수

---

### malloc 요약

* 실행 중 메모리 할당
* 힙 영역 사용
* 크기는 바이트 단위
* 초기값 없음
* free로 직접 해제 필요
