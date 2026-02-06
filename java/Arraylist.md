---
layout: wiki
title: arraylist
wiki_name: java
parent: java
order: 11
---

## **arraylist**

Arraylist는 배열과 비슷한 리스트를 사용한다.

배열은 배열의 길이를 정해주고 그곳에 저장하는 방면 리스트는 길이를 계속 추가한다.

먼저 Arraylist를 사용하기 위해 import를 해줘야 한다.
```java
import java.util.ArrayList;
```

### **(1) 선언**
```java
ArrayList<변수타입> arrayList = new ArrayList<>();
```
배열과 비슷하지만 변수 이름 앞에 ArryList<변수타입>을 넣는게 특징이다.
```java
ArrayList<String> arrayList = new ArrayList<>();
ArrayList<Integer> arrayList1 = new ArrayList<>();
```

### **(2) 데이터 추가**
```java
arrayList.add(0);
arrayList.add(1);
```
배열에서는 append()이지만 arraylist에서는 add(추가할 데이터)이다.

저장은 마지막에 저장된 위치 바로 다음에 저장한다.

출력
```java
for(int i: arrayList)

{

    System.out.println("값 :"+i);

}
```

### **(3) 데이터 제거**
```java
arrayList.remove(1); //원하는 인덱스 데이터 삭제.
```
뒤에 remove(인덱스값)을 이용하여 데이터를 삭제한다.

**(4) 길이**
```java
arrayList.size()
```
배열에서는 length()였지만 arraylist는 size()이다.

배열과 달리 배열은 저장할 수 있는 길이이지만 arrayList는 저장한 곳까지의 길이이다.

### **(5) 출력**

1. 해당 객체 명으로 출력
```java
System.out.println(Arrays.deepToString(arrayList.toArray()));
```
2. get() 메소드 활용
```java
for (int i=0; i<arrayList.size(); i++) {
  System.oet.println(i + "번째 요소: " + arrayList.get(1));
}
```
```java
arraylist.get(인덱스);
```
이런 방식으로 get(인덱스) 메소드로 지정한 인덱스 위치에 값을 불러온다.
