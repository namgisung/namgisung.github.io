---
layout: wiki
title: ArrayList
wiki_name: java
parent: java
order: 11
---

## **ArrayList**

ArrayList는 배열과 비슷한 리스트를 사용한다.

배열은 길이를 먼저 정해두고 저장하지만, 리스트는 길이를 계속 늘려가며 추가할 수 있다.

먼저 ArrayList를 사용하기 위해 import를 해줘야 한다.
```java
import java.util.ArrayList;
```

---

### **(1) 선언**
```java
ArrayList<변수타입> arrayList = new ArrayList<>();
```
배열과 비슷하지만 변수 이름 앞에 ArrayList<변수타입>을 넣는 것이 특징이다.
```java
ArrayList<String> arrayList = new ArrayList<>();
ArrayList<Integer> arrayList1 = new ArrayList<>();
```

---

### **(2) 데이터 추가**
```java
arrayList.add(0);
arrayList.add(1);
```
배열에서는 append()를 쓰지만 ArrayList에서는 add(추가할 데이터)이다.

저장은 마지막에 저장된 위치 바로 다음에 저장한다.

출력
```java
for (int i : arrayList) {
    System.out.println("값 :" + i);
}
```

---

### **(3) 데이터 제거**
```java
arrayList.remove(1); // 원하는 인덱스 데이터 삭제
```
뒤에 remove(인덱스값)을 이용하여 데이터를 삭제한다.

---

### **(4) 길이**
```java
arrayList.size();
```
배열에서는 length를 사용하지만 ArrayList는 size()이다.

배열과 달리 ArrayList의 size()는 현재 저장된 요소 개수를 의미한다.

---

### **(5) 출력**

1. 해당 객체 명으로 출력
```java
System.out.println(Arrays.deepToString(arrayList.toArray()));
```
2. get() 메소드 활용
```java
for (int i = 0; i < arrayList.size(); i++) {
  System.out.println(i + "번째 요소: " + arrayList.get(i));
}
```
```java
arrayList.get(인덱스);
```
이런 방식으로 get(인덱스) 메소드로 지정한 인덱스 위치의 값을 불러온다.
