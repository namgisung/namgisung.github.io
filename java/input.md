---
layout: wiki
title: 입력
wiki_name: java
parent: java
order: 2
---

먼저 입력 받기 위해 scanner를 import해준다.
```java
import java.util.Scanner;
```
그리고 실행할 코드를 입력하는 곳에 scanner를 사용할 함수를 선언해 준다.
```java
Scanner scanner = new Scanner(System.in);
```
scanner로 입력을 받아 문자로 저장하는 변수를 선언한다.
```java
String input = scanner.nextLine();
```
(정수로 받을때는 nextInt()를 쓰면 된다)
문자를 받는 변수를 선언한 후에 입력을 받아 저장하는 것도 상관없다.
```java
String input;
input = scanner.nextLine();
//출력할때는 println을 쓰거나 printf또는 print를 쓰면 된다.
System.out.println(input);
System.out.printf(“%s”,input);
```
그리고 한 줄에 여러개를 입력받을때는 scanner를 여러번 써주면 된다.
```java
int a = input = scanner.nextInt();
int b = input = scanner.nextInt();
System.out.println(a + " " + b);
```
```java
5 5 //입력
5 5 //출력
```
