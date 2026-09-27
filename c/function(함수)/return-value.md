---
layout: wiki
title: 반환값
wiki_name: c
parent: c/function(함수)
order: 4
---

## 반환값

함수는 작업을 수행한 뒤 그 결과를 **반환값**으로 함수 호출한 위치에 전달할 수 있다.

반환값은 `return` 키워드를 사용하여 반환하며, **함수의 자료형과 동일한 타입의 값**만 반환할 수 있다.

```c
int add(int a, int b) {
    return a + b;
}
```

위 함수는 두 정수를 더한 결과를 반환하며, 함수 호출 시 반환값은 다음과 같이 사용된다.

```c
int result = add(3, 5);  // result = 8
```

---

### 반환값의 특징

1. **반환값은 하나만 가능하다**

함수는 한 번에 하나의 값만 반환할 수 있다.

```c
return a;        // 가능
return a, b;     // 불가능
```

여러 개의 값을 반환해야 할 경우 포인터나 구조체를 사용한다.

---

2. **반환값의 타입은 함수의 자료형과 같아야 한다**

```c
int func() {
    return 10;     // 정상
}

double func2() {
    return 3.14;   // 정상
}
```

반면, 반환값이 없는 함수는 `void` 자료형을 사용한다.

```c
void print() {
    printf("Hello");
}
```

`void` 함수에서는 `return 값;` 형태를 사용할 수 없다.

---

3. **return을 만나면 함수는 즉시 종료된다**

```c
int test(int x) {
    if (x < 0)
        return -1;

    return x;
}
```

`return` 이후의 코드는 실행되지 않는다.

---

### 반환값과 매개변수의 차이

* **매개변수**: 함수 외부에서 내부로 전달되는 값 (입력)
* **반환값**: 함수 내부에서 외부로 전달되는 값 (출력)

```c
int square(int x) {   // 매개변수
    return x * x;     // 반환값
}
```

---

### 반환값이 없는 함수

반환값이 필요 없는 경우 `void` 함수를 사용하며, 주로 출력, 상태 변경, 데이터 처리 등에 사용된다.

```c
void printNumber(int n) {
    printf("%d\n", n);
}
```
