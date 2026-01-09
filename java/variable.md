---
layout: wiki
title: 변수
wiki: true
wiki_name: java
parent: java
order: 4
---
**(1) 기본 구조**

```java
int a;
```
이런 식으로 정수형인 변수 a를 선언한다

```java
int a = 10;
```
이런식으로 변수를 선언함과 동시에 값을 초기화시켜준다

**(2) 최종 변수 선언**

그리고 처음 변수를 선언하고 최종일 경우 앞에 final을 붙여 준다.
```java
final int a = 0;
```

**(3) 강제 형 변환**

만약 변수 타입을 바꾸고 싶으면 변수를 초기화할때는 강제 형 변환을 하면 된다.

변수 앞에 변환하고자하는 타입을 괄호와 함께 붙여주면 된다.

(타입)피연산자

```java
double input = 3.14; //변수 타입이 실수형으로 초기화됨
int intValue = (int)input //실수형 input변수를 정수형으로 바꿔 정수인 3만 초기화됨
System.out.println(intValue);
```

**(4) 변수 기본형 종류**

논리형: boolean (true나 false 중 하나의 값을 가지며, 조건식과 논리적 계산에 사용한다)

문자형: char, string

정수형: int

실수형: float, double

(char은 한 문자만 저장할수 있으면 저장할때 문자 양쪽에 '를 붙여줘야 한다. string은 문자나 문자열을 저장할수 있으며 저장할때 양쪽에 "를 붙여줘야 한다)
