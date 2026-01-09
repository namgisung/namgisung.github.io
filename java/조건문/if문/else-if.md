---
layout: wiki
title: else if
wiki_name: java
parent: java/조건문/if문
order: 3
---

그리고 2개 이상의 조건식이 있다면 else if를 써서 "만약 ~면 ~를 실행하고 그 조건이 아니라 ~라면 ~를 실행한다" 를 표현할수 있다.

**(1) 기본 구조**
```java
if (조건식) {
   //실행문
}
else if (조건식) {
   //실행문
}
else {
  //실행문
}
```
```java
int c = 0;
if (c == 0) {
  system.out.println(c);
}
else if (c == 1) {
  systme.out.println("2");
  }
else {
  system.out.println("3");
}
```
코드에서 else if문으로 c가 0이 아니라 1이면 2를 출력한다를 표현한 것이다.
