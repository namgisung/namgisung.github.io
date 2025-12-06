---
layout: wiki
title: "output of array"
---

**(1) for문 활용**

배열을 초기화 할때 for문을 사용하듯이, 배열을 저장에 저장된 값을 확인할 때도 다음과 같이 for문을 사용하면 된다.
```java
int[] iArr = {100, 95, 80, 70, 60

for(int i = 0 ; i < iArr.length; i++){
  System.out.println(iArr[i]);
}
```
println매서드는 출력 후에 줄 바꿈을 하므로, 여러 줄에 걸쳐 출력되어 보기 불편할 때가 있다. 그럴때는 다음과 같이 출력 후에 줄 바꿈하지 않는 print매서드를 사용하는 것이 좋다.
```java
int[] iArr = {100, 95, 80, 70, 60};

for(int i = 0 ; i < iArr.length; i++){
  System.out.print(iArr[i]);
}
System.out.println(); //다음 출력이 바로 이어지지 않도록 줄 바꿈을 한다.
```

**(2) Arrays.toString(배열이름)**

더 간단한 방법은 'Arrays.toString(배열이름)'메서드를 사용하는 것이다.

이 메서드는 배열의 모든 요소를'[첫번째 요소,두번째요소, ...]'와 같은 형식의 문자열로 만들어서 반환한다.
```java
int[] iArr = {100, 95, 80, 70, 60};

System.out.println(Arrays.toString(iArr)); // [100, 95, 80, 70, 60]
```
**(3) char**

char배열은 println메서드로 출력하면 각 요소가 구분자없이 그대로 출력되는데 이것은 println메서드가 char배열일 때만 이렇게 동작하도록 작성되었기 때문이다.
```java
char[] chArr = { 'a', 'b', 'c', 'd' };
System.out.println(chArr); //abcd가 출력됨.
```
