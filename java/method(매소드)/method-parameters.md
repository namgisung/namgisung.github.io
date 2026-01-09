---
layout: wiki
title: 매소드 매개변수
wiki_name: java
parent: java/method(매소드)
order: 3
---

메소드의 매개변수란 외부로부터 입력 값을 받기 위해 메소드의 괄호 안에 선언하는 변수라고 생각하면 된다.

main메소드에서 다른 메소드를 호출할 때 값을 전달하여 전달된 값에 따라 처리될 수 있도록 하는 기능이다.

매개변수를 정의(선언 및 호출)하는 방법은 아래와 같다
```java
public static 리턴 타입(자료형 또는 void) 메소드명( 자료형 변수명) {

}
public static void main (String[] args) {
  메소드명(깂);
}
```
메소드명 괄호 안에 int a 와 같이 넣을 수 있으며 여기서 선언한 변수는 해당 메소드 안에서만 사용할 수 있다.

입력할 값이 많을 경우 ,(따옴표)를 써서 할 수 있다.
```java
public class Main {
	public static void sum(int a) { // int a 매개변수
		int sum = 0;
		for (int i = 0; i <= a; i++) { // a = 15
			sum += i;
		}
		System.out.println(sum);
	}

	public static void sum(int a, int b) { // int a, b 매개변수 / 메소드 오버로딩
		int sum = 0;
		for (int i = a; i <= b; i++) { // a = 5, b = 20
			sum += i;
		}
		System.out.println(sum);
	}

	public static void main(String[] args) {
		sum(15); // sum(int a); 호출 및 값 전달
		sum(5, 20); // sum(int a, b); 호출 및 값 전달
	}
}
```
지역변수는 다음 내용에서 알아보자.
