---
layout: wiki
title: 문자열 처리
wiki_name: c
parent: c
order: 11
---

# 문자열 처리

C언어에서 문자열은 **문자(char)의 배열**로 표현된다.

따라서 문자열을 다루기 위해서는 문자열 전용 함수들이 필요하며,

이 함수들은 `<string.h>` 헤더 파일에 정의되어 있다.

---

## #include <string.h>

```c
#include <string.h>
```

`<string.h>`는 **문자열 처리에 필요한 함수들을 모아둔 헤더 파일**이다.

문자열의 길이, 복사, 비교, 분리(split) 등과 같은 작업을 할 때 반드시 필요하다.

---

## <string.h>에 포함된 대표적인 함수들

| 함수         | 설명                |
| ---------- | ----------------- |
| `strlen()` | 문자열 길이 반환         |
| `strcpy()` | 문자열 복사            |
| `strcmp()` | 문자열 비교            |
| `strcat()` | 문자열 연결            |
| `strtok()` | 문자열 분리 (split 역할) |

---

## 문자열 분리 (split)

자바에는 `String.split()` 메소드가 존재하지만,
**C언어에는 split 전용 함수가 존재하지 않는다.**

대신 `<string.h>`에 포함된 `strtok()` 함수를 이용해 문자열을 분리한다.

---

### strtok() 함수

```c
char *strtok(char *str, const char *delim);
```

* `str` : 분리할 문자열 (첫 호출에서만 전달)
* `delim` : 구분자
* 반환값 : 분리된 문자열의 시작 주소

---

### strtok() 사용 예제

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "apple,banana,orange";
    char *token;

    token = strtok(str, ",");   // 첫 호출
    while (token != NULL) {
        printf("%s\n", token);
        token = strtok(NULL, ","); // 이후 호출
    }

    return 0;
}
```

#### 실행 결과

```
apple
banana
orange
```

---

### strtok()의 특징

* 구분자를 기준으로 문자열을 나눈다
* **원본 문자열을 변경한다**
* 내부적으로 포인터를 사용한다
* 반복 호출을 통해 다음 토큰을 가져온다

---

## 자바 split()과 C 문자열 처리 비교

| 자바               | C언어           |
| ---------------- | ------------- |
| `String.split()` | `strtok()`    |
| 문자열 객체           | char 배열       |
| 원본 유지            | 원본 변경         |
| 사용 쉬움            | 메모리/포인터 이해 필요 |

---

## 문자열 처리와 포인터의 관계

문자열은 `char` 배열이며,
함수에서 문자열을 다룬다는 것은 **주소(포인터)를 다루는 것**과 같다.
