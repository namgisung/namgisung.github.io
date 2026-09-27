---
layout: wiki
title: 함수 호출
wiki_name: c
parent: c/function(함수)
order: 2
---

## **함수 호출**

### **(1) 호출자 / 피호출자**

* **호출자**: 함수를 부르는 쪽
* **피호출자**: 호출을 당하는 쪽 (불려지는 함수)

---

### **(2) 함수 선언(원형)을 쓰는 이유**

코드는 위에서부터 순서대로 실행되기 때문에, 함수가 `main` 함수보다 **뒤에 정의**되어 있으면 `main`에서 호출할 수 없다.
이를 해결하기 위해 **함수 선언(원형)**을 미리 작성한다.

```c
int sum(int x, int y);   // sum 함수 선언

int main(void)            // main 함수 시작
{
    int a = 10, b = 20;
    int result;

    result = sum(a, b);   // sum 함수 호출
    printf("result : %d\n", result);

    return 0;
}

int sum(int x, int y)     // sum 함수 정의 (main보다 뒤)
{
    int temp;
    temp = x + y;
    return temp;
}
```

* 함수 선언에서는 **변수명을 생략**해도 된다

```c
int sum(int, int);
```

* **선언의 이유**: 함수 호출 전에 **반환값의 형태**를 미리 알려줄 수 있음
* 함수 선언이 없다면, 함수 정의는 **항상 호출부보다 앞**에 있어야 함
