---
layout: wiki
title: realloc
wiki_name: c
parent: c/동적-메모리-할당
order: 3
---

## realloc

`realloc`은 **이미 할당된 동적 메모리의 크기를 변경**하는 함수이다.

* 기존 힙(Heap) 메모리를 **확장 또는 축소**
* 기존 데이터는 **가능한 범위까지 유지**
* 배열 크기를 **동적으로 바꾸고 싶을 때** 사용

“처음에 malloc / calloc으로 만들었는데

→ 크기가 부족하거나 남을 때”

---

### realloc 기본 형식

```c
포인터 = (자료형*)realloc(기존포인터, 새로운크기);
```

* `기존포인터` : 이미 malloc/calloc으로 할당한 포인터
* `새로운크기` : **바이트 단위 크기**

---

### realloc 사용 예제 (배열 크기 확장)

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* arr = (int*)malloc(3 * sizeof(int));

    arr[0] = 10;
    arr[1] = 20;
    arr[2] = 30;

    // 크기 확장 (3 → 5)
    arr = (int*)realloc(arr, 5 * sizeof(int));

    arr[3] = 40;
    arr[4] = 50;

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }

    free(arr);
    return 0;
}
```

#### 출력 결과

```text
10 20 30 40 50
```

기존 값(10,20,30)은 유지됨

---

### 예제: 입력이 늘어나면 배열 확장하기

양수를 입력받아 저장하다가, 공간이 가득 차면 5개씩 늘린다.

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int* pi;         // 할당한 저장 공간을 연결할 포인터
    int size = 5;    // 한 번에 할당할 저장 공간의 크기, int형 변수 5개씩
    int count = 0;   // 현재 입력된 양수 개수
    int num;         // 양수를 입력할 변수
    int i;           // 반복 제어 변수

    pi = (int*)calloc(size, sizeof(int));    // 먼저 5개의 저장 공간 할당
    if (pi == NULL) return 1;
    while (1)
    {
        printf("양수만 입력하세요 = > ");
        scanf("%d", &num);                   // 데이터 입력
        if (num <= 0) break;                 // 0 또는 음수이면 종료
        if (count == size)                   // 저장 공간을 모두 사용하면
        {
            int* temp;
            size += 5;                       // 크기를 늘려서 재할당
            temp = (int*)realloc(pi, size * sizeof(int));
            if (temp == NULL)                // 실패하면 기존 공간을 반납하고 종료
            {
                free(pi);
                return 1;
            }
            pi = temp;
        }
        pi[count++] = num;
    }
    for (i = 0; i < count; i++)
    {
        printf("%5d", pi[i]);                // 입력한 데이터 출력
    }
    free(pi);                                // 동적 할당 저장 공간 반납

    return 0;
}
```

실행 예 (10 20 30 40 50 60을 입력하고 0으로 종료)

```
   10   20   30   40   50   60
```

* 처음에 `calloc`으로 5개를 할당하고, 6번째 값을 넣을 때 `realloc`으로 10개로 늘린다
* 기존 데이터는 **그대로 유지**된다
* 교재 예제는 `pi = realloc(pi, ...)`로 바로 덮어쓰지만, 실패하면 기존 주소를 잃으므로 위 코드는 **`temp`에 먼저 받아서 확인**한다

---

### realloc 내부 동작 방식

`realloc`은 상황에 따라 다르게 동작한다.

#### (1) 뒤 공간이 비어 있는 경우

→ **같은 주소에서 크기만 확장**

#### (2) 뒤 공간이 없는 경우

→ **새 공간 할당 + 데이터 복사 + 기존 메모리 해제**

이 과정은 **자동으로 처리됨**

---

### realloc으로 크기 줄이기

```c
int* arr = (int*)malloc(5 * sizeof(int));
arr = (int*)realloc(arr, 3 * sizeof(int));
```

* 앞의 3개 데이터만 유지
* 나머지는 접근 불가

---

### realloc 실패 처리 (중요)

아래 코드는 위험

```c
arr = realloc(arr, newSize);
```

realloc 실패 시 `NULL` 반환

→ 기존 포인터 주소를 잃어버림 → 메모리 누수

✔ 안전한 방식

```c
int* temp = realloc(arr, newSize);

if (temp == NULL) {
    printf("메모리 재할당 실패\n");
    free(arr);
    return 1;
}

arr = temp;
```

---

### realloc + NULL 포인터

```c
int* arr = NULL;
arr = realloc(arr, 10 * sizeof(int));
```

이 경우 `malloc`처럼 동작함

---

### realloc + 크기 0

```c
realloc(arr, 0);
```

* 구현에 따라 `free(arr)`와 동일
* 반환값은 `NULL` 또는 다른 값

  → 사용하지 말 것

---

### malloc / calloc / realloc 비교

| 함수      | 역할      | 초기화 |
| ------- | ------- | --- |
| malloc  | 메모리 할당  | ❌  |
| calloc  | 여러 개 할당 | ⭕ 0 |
| realloc | 크기 변경   | 유지  |

---

### realloc 사용 시 주의점

* 반환값 NULL 체크 필수
* 기존 포인터 바로 덮어쓰지 말 것
* 재할당 후 배열 인덱스 다시 관리

---

### realloc 요약

* 힙 메모리 크기 변경
* 기존 데이터 유지
* 확장·축소 가능
* 실패 처리 반드시 필요
* 동적 배열에 핵심 함수
