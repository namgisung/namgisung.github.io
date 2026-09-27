---
layout: wiki
title: 반환값
wiki_name: c
parent: c/function(함수)
order: 4
---

## **반환값**

### **(1) return**

`return`은 **"함수가 끝났으니 호출했던 곳으로 되돌아가자"** 는 의미다.

```c
return;      // 반환값이 없을 때
return temp; // 반환값이 있을 때
```

* 함수를 호출할 때, **컴파일러는 반환값을 저장할 공간을 미리 준비**해둔다
* 함수 중간에 돌아가야 하는 상황이라면, **`return`은 함수 어디에서든 사용 가능**

---

### **(2) 반환값이 없는 함수**

```c
void print_char(char ch, int count);
```

* 선언과 정의 모두에 `void` 사용
