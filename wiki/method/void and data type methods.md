---
layout: wiki
title: "void and data type methods"
---

void는 메소드 내에서 코드를 불러와서 실행하는 것이고 자료형은 메소드 내에서 얻은 결과를 반환해준다.

**(1) void**

void 메소드는 코드를 따로 만들고 불러와서 실행하는 방식이다.
```java
public class Main {
  public static void hello(){ // 메소드 정의
    System.out.println("Hello World!!");
  }
  public static void main(String[] args) { // main 메소드
    sum(); // 메소드 호출
    sum(); // 메소드 호출
    sum(); // 메소드 호출
  }
}
```
```java
Hello World!!
Hello World!!
Hello World!!
```
요런 식으로 코드를 불러와서 실행할 수 있다. (반복한 내용을 한번으로 줄일 수 있음)

**(2) 자료형 메소드**

자료형 메소드는 메소드 내에서 실행되고 얻은 결과를 반환하여 함수 자체가 그 값을 갖게 한다.
```java
public class Main {
  public static int div() {
    int a = 10, b = 5;
      int result = a / b;
      return result;	// 호출한 곳으로 값 반환
  }
  public static void main(String[] args) {
    System.out.println(div()); // 메소드 호출 후 리턴값 출력
  }
}
```
