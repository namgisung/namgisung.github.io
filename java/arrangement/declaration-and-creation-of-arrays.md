---
layout: wiki
title: "Declaration and creation of arrays"
---

선언방법: 타입[] 변수이름:
선언 예: int[] score:, String[] name:
배열의 생성: 변수이름 = new 타입[길이];
코드로 하면
```java
타입[] 변수이름;             //배열을 선언 (배열을 다루기 위한 참조변수 선언)
변수이름 = new 타입[길이];   //배열을 생성 (실제 저장공간을 생성)
```

아래의 코드는 '길이가 5인 int배열'을 생성한다.
```java
int[] score;
score = new int[5];
```

다음과 같이 배열의 선언과 생성을 동시에 하면 간략히 한 줄로  할 수 있다
```java
타입[] 변수이름 = new 타입[길이];
int[] score = new int[5];
```
