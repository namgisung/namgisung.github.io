---
layout: wiki
title: 문자열 + split
wiki_name: python
parent: python
order: 12
---

## **문자열**

문자열은 문자들의 집합으로, 텍스트 데이터를 저장하는 자료형이다.

문자열은 작은따옴표('') 또는 큰따옴표("")로 표현한다.
```python
str1 = "hello"
str2 = 'python'
```

---

### **문자열의 인덱싱**

문자열은 인덱스를 이용하여 각 문자에 접근할 수 있다.
```python
s = "hello"

print(s[0])  # h
print(s[1])  # e
```

인덱스는 0부터 시작한다.

----

### **문자열의 슬라이싱**

문자열의 일부를 잘라낼 수 있다.
```python
s = "hello"

print(s[1:4])  # ell
```
시작 포함, 끝 미포함

---

## **split() 함수**

split() 함수는 문자열을 특정 기준으로 나누어 리스트로 반환한다.

---

### **(1) 기본 사용**
```python
s = "a b c"
result = s.split()

print(result)
```
출력:
```python
['a', 'b', 'c']
```
공백을 기준으로 나눈다.

----

### **(2) 구분자 지정**
```python
s = "a,b,c"
result = s.split(",")

print(result)
```
출력:
```python
['a', 'b', 'c']
```

원하는 기준으로 나눌 수 있다.

----

## **split() 결과 활용**

split()의 결과는 리스트이므로 인덱스를 이용해 원하는 값에 접근할 수 있다.

----

### **(1) 인덱스로 접근**
```python
a = "apple banana cherry"

print(a.split()[0])
```
출력:
```python
apple
```
split()으로 나눈 뒤 첫 번째 요소에 접근

---

### **(2) 여러 값 사용**
```python
a = "10 20 30"

x = a.split()

print(x[0])  # 10
print(x[1])  # 20
print(x[2])  # 30
```

----

### **(3) 입력과 함께 사용**
```python
a = input().split()

print(a[0])
```
사용자 입력을 공백 기준으로 나눠서 사용
