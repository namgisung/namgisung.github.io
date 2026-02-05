---
layout: wiki
title: calloc
wiki_name: c
parent: c/동적-메모리-할당
order: 2
---

## calloc

### calloc이란?

`calloc`은 **여러 개의 연속된 메모리를 할당하면서, 모든 값을 0으로 초기화**해주는 동적 메모리 할당 함수이다.

* `calloc`은 **Contiguous Allocation**의 약자
* 힙(Heap) 영역에 메모리 할당
* 할당과 동시에 **0으로 초기화**
* 배열 형태의 메모리를 만들 때 자주 사용

`malloc`과 가장 큰 차이점

→ **초기화 여부**

---

### calloc 기본 형식

```c
포인터 = (자료형*)calloc(개수, 자료형의 크기);
```

---

### calloc 사용 예제 (정수 배열)

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* arr = (int*)calloc(5, sizeof(int));

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }

    free(arr);
    return 0;
}
```

#### 출력 결과

```text
0 0 0 0 0
```

`calloc`으로 할당된 메모리는 **자동으로 0으로 초기화**

---

### calloc 동작 방식 이해

```c
calloc(5, sizeof(int));
```

이 코드는 다음 의미이다.

```text
int 크기의 메모리 5개를 연속으로 할당
→ 총 크기 = 5 × sizeof(int)
→ 모든 바이트를 0으로 초기화
```

---

### malloc vs calloc 비교

| 구분    | malloc | calloc    |
| ----- | ------ | --------- |
| 초기화   | ❌ 안 됨  | ⭕ 0으로 초기화 |
| 인자 개수 | 1개     | 2개        |
| 사용 목적 | 일반 메모리 | 배열 생성     |
| 속도    | 조금 빠름  | 조금 느림     |

초기값이 필요하면 `calloc`

성능만 중요하면 `malloc`

---

### calloc으로 문자열 배열 생성 예제

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char* str = (char*)calloc(20, sizeof(char));

    printf("'%s'\n", str); // 빈 문자열

    free(str);
    return 0;
}
```

문자열은 `\0`이 중요하기 때문에

→ `calloc`이 특히 안전함

---

### calloc 실패 처리 (NULL 체크)

```c
int* arr = (int*)calloc(5, sizeof(int));

if (arr == NULL) {
    printf("메모리 할당 실패\n");
    return 1;
}
```

동적 메모리 함수는 항상 실패 가능성 있음

---

### calloc 사용 시 주의점

❌ free 하지 않으면 메모리 누수

```c
calloc(...);
// free 안 하면 힙에 메모리 계속 남음
```

반드시 `free()` 호출

---

### calloc 요약

* 힙 영역에 동적 메모리 할당
* 여러 개의 연속된 공간 생성
* 모든 값이 0으로 초기화
* 배열, 문자열에 적합
* 사용 후 `free()` 필수
