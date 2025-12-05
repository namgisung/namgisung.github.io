---
layout: wiki
title: "copy of array"
---

배열의 복사는 두가지 방법이 있다.

첫 번째는 for문을 활용해서 한 배열의 모든 요소에 저장된 값을 하나씩 다른 배열에 저장하는 방식이 있다,

두 번째는 System.arraycopy()를 이용한 배열의 복사가 있다.

for문은 배열의 요소 하나하나에 접근해서 복사하지만, System.arraycopy()는 지정된 값들을 한 번에 통째로 복사한다.

각 요소들이 연속적으로 저장되어 있다는 배열의 특성때문에 이렇게 처리하는 것이 가능한 것이다.

배열의 복사는 for문보다 System.arraycopy()를 사용하는 것이 효율적이다

배열의 복사에 사용된 for문을 System.arraycopy()로 바꾸면 다음과 같다.
```java
for(int i=0; i < num.length; i++); {  newNum[i] = num[i]; }
->
System.arraycopy(num, 0, newNum, 0, num.length);
```
arraycopy()를 호출할 때는 어느 배열의 몇 번째 요소에서 어느 배열로 몇 번째 요소로 몇 개의 값은 복사할 것인지 지정해줘야 하는데, 다음과 같이 생각하면 이해하기 쉽다.
```java
System.arraycopy(num, 0, newNum, 0, num.length);
->
//num[0]에서 newNum[0]으로 num.length개의 데이터를 복사
```
예시)
```java
char[] abc = { 'A', 'B', 'C', 'D'};
char[] num = { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9'};

char[] result = new char[abc.length+ num.length];
System.arraycopy(abc, 0, result, 0, abc.length);
System.arraycopy(num, 0, result,abc.length, num.length);
System.out.println(result); //ABCD0123456789
```
