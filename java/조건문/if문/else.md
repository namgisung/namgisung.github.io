---
layout: wiki
title: else
wiki_name: java
parent: java/조건문/if문
order: 2
---


만일 조건이 거짓이라면 중괄호 안에 있는 실행문은 동작하지 않고 if문을 빠져나간다.

거짓일때 다르게 샐행 시키려면 else를 쓰면 된다.

**(1) 기본 구조**
```java
if (조건식) {
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
else {
  system.out.println("false");
}
```
