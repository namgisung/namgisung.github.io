---
layout: wiki
title: free
wiki_name: c
parent: c/동적-메모리-할당
order: 4
---

## free

### free란?

`free`는 **동적 메모리 할당으로 확보한 힙(Heap) 메모리를 해제**하는 함수이다.

* `malloc`, `calloc`, `realloc`으로 할당한 메모리는

  **사용이 끝나면 반드시 free로 반납해야 한다**
* 해제하지 않으면 **메모리 누수(memory leak)** 발생

C언어는 **자동 메모리 관리가 없음**

→ 개발자가 직접 책임짐

---

### free 기본 형식

```c
free(포인터);
```

* 인자로 전달한 포인터가 가리키는 힙 메모리를 해제
* 반환값 없음

---

### free 사용 예제

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* arr = (int*)malloc(5 * sizeof(int));

    for (int i = 0; i < 5; i++) {
        arr[i] = i * 10;
    }

    free(arr);   // 메모리 해제
    return 0;
}
```

`arr`이 가리키던 힙 메모리는 운영체제로 반환됨

---

### free 이후 포인터 상태 (중요 ❗)

```c
free(arr);
```

* 메모리는 해제되었지만
* `arr` 포인터 변수 자체는 남아 있음
* **쓰레기 주소를 가리키는 상태 (댕글링 포인터)**

위험한 코드

```c
free(arr);
printf("%d", arr[0]); // ❌ 접근하면 안 됨
```

안전한 습관

```c
free(arr);
arr = NULL;
```

---

### NULL 포인터에 free 사용

```c
int* p = NULL;
free(p);
```

문제 없음

아무 동작도 하지 않음

→ **안전한 코드**

---

### free는 몇 번 호출해야 할까?

```c
int* p = malloc(sizeof(int));
free(p);
```

✔ 1번만

두 번 호출하면?

```c
free(p);
free(p); // ❌ undefined behavior
```

→ 프로그램이 터질 수도 있음

---

### free와 배열

```c
int* arr = malloc(10 * sizeof(int));
free(arr);
```

배열이든 단일 변수든

**malloc으로 할당했으면 free는 한 번만**

---

### free와 realloc 관계

```c
int* arr = malloc(3 * sizeof(int));
arr = realloc(arr, 5 * sizeof(int));
free(arr);
```

* realloc 이후에는 **새 포인터만 free**
* 기존 메모리는 realloc이 알아서 처리

---

### 메모리 누수 예시

```c
void func() {
    int* p = malloc(sizeof(int));
    *p = 10;
    // free 없음 ❌
}
```

함수 종료돼도 힙 메모리는 남아 있음

→ 반복되면 메모리 계속 새는 중

---

### free 요약

* 힙 메모리 해제 함수
* malloc / calloc / realloc과 한 세트
* free 후 접근 ❌
* free 후 NULL 대입 권장
* 한 번만 free
