---
layout: wiki
title: void 포인터
wiki_name: c
parent: c/포인터
order: 12
---

## void 포인터

**void 포인터**는 **가리키는 자료형을 정하지 않은 포인터**이다.
일종의 두루뭉실한 포인터로, **다양한 자료형의 변수 주소를 받을 수 있다.**

---

### (1) 선언과 사용

```c
#include <stdio.h>

int main(void)
{
    int a = 10;                           // int형 변수
    double b = 3.5;                       // double형 변수
    void* vp;                             // void 포인터

    vp = &a;                              // int형 변수의 주소 저장
    printf("a : %d\n", *(int*)vp);

    vp = &b;                              // double형 변수의 주소 저장
    printf("b : %.1lf\n", *(double*)vp);

    return 0;
}
```

실행 결과

```
a : 10
b : 3.5
```

---

### (2) 사용할 때 주의

* `void *`는 가리키는 대상의 크기를 모르므로 **그대로는 `*`로 값을 읽을 수 없다**
* 값을 읽으려면 **원래 자료형의 포인터로 형변환**해야 한다 (`*(int*)vp`)
* 어떤 자료형의 주소든 저장할 수 있지만, **무엇을 저장했는지는 프로그래머가 기억**해야 한다
* 동적 메모리 할당 함수(`malloc` 등)가 반환하는 자료형도 `void *`이다
