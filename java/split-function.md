---
layout: wiki
title: split문
wiki_name: java
parent: java
order: 12
---

## **split문**

split함수는 문자열을 구분하여 자를 수 있다.

split 구조는 다음과 같다
```java
문자변수이름.split(구분자)
```

### **(1) 배열에 저장하여 쓰기**
첫번째 함수 사용 방법은 문자열을 구분자로 구분하여 배열에 저장하여 사용하는 것이다.
```java
String str = "서울 대전 대구 부산 인천 울산"; //"서울 대전 대구 부산 인천 울산"을 저장한 문자변수 str선언
String[] strArr = str.split(" "); //[서울,대전,대구,부산,인천,울산]
```
위 코드는 문자에 포함된 공백을 기준으로 잘라 배열에 저장한 것이다.

자른 것들을 저장하거나 사용할때는 배열에 인덱스를 사용하면 된다.
```java
String a1 = strArr[0] //서울
```

```java
System.out.print(strArr[0]); //서울
System.out.print(strArr[1]); //대전
System.out.print(strArr[2]); //대구
System.out.print(strArr[3]); //부산
System.out.print(strArr[4]); //인천
System.out.print(strArr[5]); //울산
```
이런 식으로 불러올 수 있다.


### **(2) 배열 필요없이 바로 저장하여 쓰기**

두 번째 사용 방법은 구분자로 하나씩 잘라서 배열 필요 없이 바로 저장하는 것이다.

split 구조는 다음과 같다
```java
문자변수이름.split(구분자)[인덱스]
```
ex)
```java
String str1 = "(int i=0;i<=10;i++)";
String str1_1 = str1.split(";")[0]; //(int i=0
String str1_2 = str1.split(";")[1]; //i<=10
String str1_3 = str1.split(";")[2]; //i++)

System.out.println(str1_1);
System.out.println(str1_2);
System.out.println(str1_3);
```
```java
(int i=0
i<=10
i++)
```
