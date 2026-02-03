---
layout: wiki
title: 출력
wiki_name: java
parent: java
order: 3
---

**(1) System.out.println(“”);**

“”안에 문자를 입력하거나 변수를 입력하여 출력할 수 있다.

문자와 변수를 같이 출력할때 (“”+a)식으로 덧셈 연산자로 합칠 수 있다.

“”안에 \n을 넣어 줄바꿈을 할 수 있다.

``` java
System.out.println("Hello, World!");
```

**(2) System.out.print(“”);**

println()과 기능은 비슷하나 println()는 실행 후 줄바꿈을 하지만 

print()는 실행 후 줄바꿈을 하지 않는다.

**(3) System.out.printf();**
``` java
System.out.printf(“출력%d”,a);
```
형식화된 출력이고 앞에 출력하려고 하는 문자와 변수를 입력하고 뒤에 변수들을 입력한다.

println은 출력하면 줄바꿈을 하지만 printf는 줄바꿈을 하지 않는다.



**(4) 지시자:**

| 지시자  | 의미                     |
| ---- | ---------------------- |
| '%d' |  10진수 (정수)          |
| '%f' | 10진수 (실수) |
| '%s' | 문자 (string)         |
| '%c' | 문자 (char)     |
| '%n' | 줄바꿈   |

```java
int a = 3;
int a = 3;
double b= 3.14;
String str = "안녕";
char c = 'a';
System.out.printf("a = %d%n", a);
System.out.printf("b = %f%n", b);
System.out.printf("나는 %s%n", str);
System.out.printf("a = %c", c);


```
