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

### 정적 할당과 동적 할당

변수의 저장 공간을 확보하는 방법은 두 가지이다.

| 구분 | 정적 할당 | 동적 할당 |
| --- | --- | --- |
| 크기 결정 | 컴파일할 때 정해짐 | 프로그램 실행 중에 정함 |
| 공간 확보 | 프로그램(또는 블록)이 시작될 때 미리 확보 | 필요할 때 확보 |
| 반납 | 끝나면 자동으로 해제 | `free`로 직접 반납 |
| 대표 예 | 일반 변수, 배열 | `malloc`, `calloc`, `realloc` |
| 저장 영역 | 스택, 데이터 영역 | 힙 |

* 프로그램 실행 중에 메모리를 동적 할당할 때는 `malloc` 함수를, 반환할 때는 `free` 함수를 사용한다
* `malloc`, `free`는 `stdlib.h`에 선언되어 있어서 `#include <stdlib.h>`가 필요하다

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

### int와 double을 함께 할당하기 (NULL 검사 포함)

```c
#include <stdio.h>
#include <stdlib.h>       // malloc, free 함수 사용을 위한 헤더 파일

int main(void)
{
    int* pi;              // 동적 할당 영역을 연결할 포인터 선언
    double* pd;

    pi = (int*)malloc(sizeof(int));        // 메모리 동적 할당 후 포인터 연결
    if (pi == NULL)                        // 동적 할당에 실패하면 NULL 포인터 반환
    {
        printf("# 메모리가 부족합니다.\n");  // 예외 상황 메시지 출력
        exit(1);                           // 프로그램 종료
    }
    pd = (double*)malloc(sizeof(double));

    *pi = 10;                              // 포인터로 동적 할당 영역 사용
    *pd = 3.4;

    printf("정수형으로 사용 : %d\n", *pi);   // 동적 할당 영역에 저장된 값 출력
    printf("실수형으로 사용 : %.1lf\n", *pd);

    free(pi);                              // 동적 할당 영역 반환
    free(pd);

    return 0;
}
```

실행 결과

```
정수형으로 사용 : 10
실수형으로 사용 : 3.4
```

* `exit(1)`은 프로그램을 **즉시 종료**한다. 괄호 안의 값은 종료 상태이며, 0이 아니면 비정상 종료를 뜻한다
* 같은 동적 할당 영역도 연결한 포인터의 자료형에 따라 **정수형으로도, 실수형으로도** 사용할 수 있다

---

### 배열처럼 malloc 사용하기

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* arr = (int*)malloc(sizeof(int) * 5);  // 저장 공간 20바이트(int 5개) 할당

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
* 할당한 공간은 `arr[0]`~`arr[4]`처럼 **배열처럼 사용**할 수 있다

동적 배열 생성

→ **배열 크기를 실행 중에 결정 가능**

---

### malloc의 특징

* 힙(Heap) 영역에 메모리 할당
* 크기를 직접 지정해야 함
* 초기값이 **정해져 있지 않음** (쓰레기 값)
* 사용 후 반드시 `free()`로 해제해야 함
* 힙의 크기는 **요청 내용에 따라 달라지는 가변 크기**이다


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

> `malloc`은 메모리 할당에 실패하면 `NULL`을 반환한다.
> 여기서 `NULL`은 유효한 메모리 주소를 가리키지 않는 널 포인터를 나타낸다.

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

### 활용: 입력한 길이에 맞게 문자열 저장하기

문자열을 입력받을 때마다 **그 길이에 딱 맞는 공간**을 동적 할당하고, 포인터 배열로 연결한다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void print_str(char** ps);     // 동적 할당 영역의 문자열을 출력하는 함수

int main(void)
{
    char temp[80];             // 임시 char 배열
    char* str[21] = { 0 };     // 문자열을 연결할 포인터 배열, 널 포인터로 초기화
    int i = 0;                 // 반복 제어 변수

    while (i < 20)             // 최대 20개까지 입력
    {
        printf("문자열을 입력하세요 : ");
        if (fgets(temp, sizeof(temp), stdin) == NULL) break;   // 문자열 입력
        temp[strcspn(temp, "\n")] = '\0';                      // 끝의 개행 문자 제거

        if (strcmp(temp, "end") == 0) break;       // end가 입력되면 반복 종료
        str[i] = (char*)malloc(strlen(temp) + 1);  // 문자열 저장 공간 할당 (\0 자리 포함)
        if (str[i] == NULL) break;                 // 할당에 실패하면 입력 중단
        strcpy(str[i], temp);                      // 동적 할당 영역에 문자열 복사
        i++;
    }
    print_str(str);                                // 입력한 문자열 출력

    for (i = 0; str[i] != NULL; i++)               // str에 연결된 문자열이 없을 때까지
    {
        free(str[i]);                              // 동적 할당 영역 반환
    }

    return 0;
}

void print_str(char** ps)      // 이중 포인터 선언
{
    while (*ps != NULL)        // 포인터 배열의 값이 널 포인터가 아닌 동안 반복
    {
        printf("%s\n", *ps);   // ps가 가리키는 것은 포인터 배열의 요소
        ps++;                  // ps가 다음 배열 요소를 가리킨다
    }
}
```

실행 예

```
문자열을 입력하세요 : apple
문자열을 입력하세요 : banana
문자열을 입력하세요 : end
apple
banana
```

* `strlen(temp) + 1`에서 **`+ 1`은 널 문자(`\0`) 자리**이다
* `str[21]`을 모두 `NULL`로 초기화해두면 **마지막 칸이 항상 `NULL`**이라서, 출력과 `free` 반복문이 `NULL`을 만날 때까지 돌면 된다
* 포인터 배열을 함수로 넘기므로 **매개변수는 이중 포인터(`char**`)** 이다
* `gets` 대신 `fgets`를 쓰면 입력 길이를 제한할 수 있다. `fgets`는 개행 문자도 저장하므로 `strcspn`으로 지운다 (`strcspn`은 `string.h`에 있다)

---

### malloc 요약

* 실행 중 메모리 할당
* 힙 영역 사용
* 크기는 바이트 단위
* 초기값 없음
* free로 직접 해제 필요
