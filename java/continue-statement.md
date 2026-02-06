---
layout: wiki
title: continue문
wiki_name: java
parent: java
order: 9
---
## **continue문**

continue문은 반복문 내만 사용될 수 있으며, 반복이 진행 중에 continue문을 만나게 되면 반복문의 끝으로 이동하여 다음 반복으로 넘어간다.
```java
for(imt i=0; i<= 10; i++) {
  if(i%3 == 0) {
  continue;
  }
  System.out.println(i);
}
```
위 코드는 i가 3의 배수를 제외하고 출력하는 코드이다.
