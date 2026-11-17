---
layout: wiki
title: 이중 포인터
wiki_name: c
parent: c/포인터
order: 9
---

## 이중 포인터

**이중 포인터**는 **포인터의 주소를 저장하는 포인터**이다. 별을 두 개(`**`) 붙여 선언한다.

---

### (1) 선언과 사용

```c
int a = 10;
int *pi = &a;     // pi : a의 주소를 저장
int **ppi = &pi;  // ppi : pi의 주소를 저장

printf("%d\n", **ppi);   // 10
```

| 표현 | 의미 |
| --- | --- |
| `ppi` | `pi`의 주소 |
| `*ppi` | `pi` (a의 주소) |
| `**ppi` | `a` (값 10) |

`&(&a)`이중 주소 연산자 불가

* 최종적으로 가리키는 대상의 **자료형이 똑같아야 한다**. `int **`는 `int *`의 주소를 저장하는 포인터이다
* `&pi`는 가능하지만 `&(&pi)`는 **불가능**하다. `&pi`는 값(주소)일 뿐이고 저장 공간이 없어서 주소를 구할 수 없기 때문이다
* 삼중 포인터도 존재하지만 **잘 사용하지 않는다**

---

### (2) 이중 포인터의 활용

1. 포인터 값을 바꾸는 함수의 매개변수
2. 포인터 배열을 매개변수로 받는 함수

---

### (3) 활용 1: 포인터 값을 바꾸는 함수

함수 안에서 **포인터 자체의 값**을 바꾸려면, 그 포인터의 주소(이중 포인터)를 넘겨야 한다.

```c
#include <stdio.h>

void swap_ptr(char** ppa, char** ppb);

int main(void)
{
    char* pa = "success";
    char* pb = "failure";

    printf("pa -> %s, pb -> %s\n", pa, pb);   // 바꾸기 전에 문자열 출력
    swap_ptr(&pa, &pb);                       // 함수 호출
    printf("pa -> %s, pb -> %s\n", pa, pb);   // 바꾼 후에 문자열 출력

    return 0;
}

void swap_ptr(char** ppa, char** ppb)
{
    char* pt;

    pt = *ppa;
    *ppa = *ppb;
    *ppb = pt;
}
```

실행 결과

```
pa -> success, pb -> failure
pa -> failure, pb -> success
```

* 문자열 자체를 복사하지 않고, **`pa`와 `pb`가 가리키는 곳만 서로 바꾼다**

---

### (4) 활용 2: 포인터 배열을 받는 함수

```c
#include <stdio.h>

void print_str(char** pps, int cnt);

int main(void)
{
    char* ptr_ary[] = { "eagle", "tiger", "lion", "squirrel" };   // 초기화
    int count;                        // 배열 요소 수를 저장할 변수

    count = sizeof(ptr_ary) / sizeof(ptr_ary[0]);  // 배열 요소의 수 계산
    print_str(ptr_ary, count);        // 배열명과 배열 요소 수를 주고 호출

    return 0;
}

void print_str(char** pps, int cnt)   // 매개변수로 이중 포인터 사용
{
    int i;

    for (i = 0; i < cnt; i++)         // 배열 요소 수만큼 반복
    {
        printf("%s\n", pps[i]);       // 이중 포인터를 배열명처럼 사용
    }
}
```

실행 결과

```
eagle
tiger
lion
squirrel
```

* 포인터 배열의 이름은 첫 요소(`char *`)의 주소이므로, **`char **`로 받는다**
* 요소 수 계산 `sizeof(ptr_ary) / sizeof(ptr_ary[0])`에서 요소 하나는 포인터이므로 **8바이트**이다. 전체 32바이트 / 8 = 4개
