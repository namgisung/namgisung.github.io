---
layout: wiki
title: method
wiki_name: java
parent: java/method(매소드)
order: 1
---

## **method**

메소드는 함수를 만드는 것이다.

메소드의 기본 구조(선언)는 다음과 같다.
```java
public class Main{
  public static 리턴 타입(자료형 또는 void) 매소드명(){
    //실행할 코드 작성
    return; //리턴 타입이 void일 경우 return 없음
  }
}
```

### **(1) main 메소드**

main 메소드는 프로그램의 시작점 역할을 한다.

즉, main 메소드가 없는 프로그램은 별도로 동작할 수가 없다.

컴퓨터가 소스 코드를 읽을 때 main 메서그를 실행하고 거기에 정의된 로직에 따라 프로그램이 동작하게 된다.

### **(2) 메소드 리턴 타입**

메소드의 리턴 타입은 자료형 또는 void가 올 수 있다. 

자료형이 리턴 타입으로 오면 반환(return)해 주는 값(메소드 자료형과 동일한 값)이 반드시 있어야 하고

void는 반환 값이 없다.
