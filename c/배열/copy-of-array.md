---
layout: wiki
title: 배열의 복사
wiki_name: c
parent: c/배열
order: 6
---


## 배열의 복사
C 언어에서 배열의 복사 역시 **두 가지 방법**이 있다.

---

###  C 배열 복사의 핵심 특징

* 배열은 **연속된 메모리 공간**
* 기본적으로 **for문 복사**
* 함수로는 `memcpy()` 사용
* 배열 크기를 **직접 관리**해야 함

---

## (1) for문을 이용한 배열 복사

첫 번째 방법은 for문을 활용해서

한 배열의 모든 요소를 하나씩 다른 배열에 복사하는 방식이다.

```c
#include <stdio.h>

int main() {
    int num[5] = {1, 2, 3, 4, 5};
    int newNum[5];

    for(int i = 0; i < 5; i++) {
        newNum[i] = num[i];
    }

    return 0;
}
```

이 방법은 배열의 **각 요소에 직접 접근**하여 복사한다.

---

## (2) memcpy()를 이용한 배열 복사

C 언어에서는 `System.arraycopy()`와 비슷한 역할을 하는 함수로

**`memcpy()`**가 있다.

`memcpy()`는 배열의 요소를 하나씩 복사하는 것이 아니라

**지정된 메모리 영역을 한 번에 통째로 복사**한다.

배열의 요소들이 **연속적으로 저장되어 있다는 특성** 때문에 가능한 방식이다.

```c
#include <stdio.h>
#include <string.h>

int main() {
    int num[5] = {1, 2, 3, 4, 5};
    int newNum[5];

    memcpy(newNum, num, sizeof(num));

    return 0;
}
```

---

### memcpy() 구조 이해하기

```c
memcpy(복사될_배열, 원본_배열, 복사할_바이트_수);
```

자바의 `System.arraycopy()`와 비교하면 다음과 같다.

```java
System.arraycopy(num, 0, newNum, 0, num.length);
```

```c
memcpy(newNum, num, sizeof(num));
```

`sizeof(num)`
→ num 배열 전체의 **메모리 크기(byte)**

---

## (3) 예제: 두 배열을 하나로 복사하기

자바 예제와 동일한 구조의 C 코드이다.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char abc[] = {'A', 'B', 'C', 'D'};
    char num[] = {'0','1','2','3','4','5','6','7','8','9'};

    char result[sizeof(abc) + sizeof(num)];

    memcpy(result, abc, sizeof(abc));
    memcpy(result + sizeof(abc), num, sizeof(num));

    for(int i = 0; i < sizeof(result); i++) {
        printf("%c", result[i]);
    }

    printf("\n"); // ABCD0123456789

    return 0;
}
```

---

## Java vs C 배열 복사 차이 

| 구분    | Java               | C                |
| ----- | ------------------ | ---------------- |
| 기본 복사 | for문               | for문             |
| 빠른 복사 | System.arraycopy() | memcpy()         |
| 단위    | 요소 개수              | 바이트 크기           |
| 배열 길이 | 자동 제공              | 직접 계산 (`sizeof`) |
| 안전성   | 높음                 | 낮음 (크기 실수 시 위험)  |

---

* Java: **배열 = 객체**
* C: **배열 = 메모리 덩어리**
* 그래서 C는 `memcpy()`처럼 **메모리 단위 복사**가 가능함
