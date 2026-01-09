---
layout: wiki
title: break문
wiki_name: java
parent: java
order: 8
---


break문은 현재 위치에서 가장 가까운 sxitch문이나 반복문을 빠져나온다

```java
int sum = 0;
int i = 1;

while(true){
  if(sum > 100){
    break;
  }
  sum += 1;
  i++
}
```
위 코드는 sum이 100보다 커지면 break문이 실행되어 즉시 반복문을 빠져나온다
