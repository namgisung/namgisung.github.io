---
layout: wiki
title: 문자열 + 함수 정리
wiki_name: python
parent: python
order: 13
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

---

### **문자열의 슬라이싱**

문자열의 일부를 잘라낼 수 있다.

```python
s = "hello"

print(s[1:4])  # ell

```

시작 인덱스 포함, 끝 인덱스 미포함

---

## ** 중요: 문자열은 이뮤터블(Immutable)이다**

파이썬에서 문자열은 Immutable(변경 불가능한 자료형)이다. 한 번 생성된 문자열 객체는 내부 값을 직접 수정할 수 없다.

따라서 뒤에 나오는 `replace()`, `upper()`, `strip()` 등의 함수들은 **원본을 수정하는 것이 아니라, 가공된 "새로운 문자열"을 만들어서 반환**한다.

```python
s = "hello"
s.replace("h", "x")  # 새로운 문자열 "xello"를 반환함

print(s)  # 결과: hello (원본은 바뀌지 않음!)

# 바뀐 값을 적용하려면 변수에 다시 대입(재할당)해야 한다.
s = s.replace("h", "x")
print(s)  # 결과: xello

```

---

## **주요 문자열 함수 정리**

---

### **(1) split() : 문자열 나누기**

문자열을 특정 기준으로 나누어 **리스트**로 반환한다. (기본값은 공백 기준)

```python
s = "apple banana cherry"
result = s.split()

print(result)     # ['apple', 'banana', 'cherry']
print(result[0])  # apple (인덱스로 접근 가능)

```

구분자를 직접 지정할 수도 있으며, `input().split()` 형태로 입력과 동시에 리스트로 쪼갤 때 자주 쓰인다.

---

### **(2) find() : 위치 찾기**

문자열 내에서 특정 문자가 처음 시작하는 **인덱스 번호**를 반환한다.

```python
s = "hello"
print(s.find("e"))  # 1
print(s.find("z"))  # -1 (찾는 문자가 없으면 -1 반환)

```

---

### **(3) count() : 개수 세기**

문자열 내에서 특정 문자가 몇 번 등장하는지 개수를 센다.

```python
s = "apple"
print(s.count("p"))  # 2

```

---

### **(4) strip(), lstrip(), rstrip() : 공백 제거**

문자열 양쪽, 왼쪽, 오른쪽의 공백(줄바꿈, 탭 포함)을 제거한 새 문자열을 반환한다.

```python
s = "  hello  "

print(s.lstrip())  # "hello  " (왼쪽 공백 제거)
print(s.rstrip())  # "  hello" (오른쪽 공백 제거)
print(s.strip())   # "hello"   (양쪽 공백 제거)

```

---

### **(5) replace() : 문자열 바꾸기**

첫 번째 인자의 문자열을 두 번째 인자의 문자열로 치환하여 반환한다.

```python
s = "hello python"
result = s.replace("python", "world")

print(result)  # hello world

```

---

### **(6) upper(), lower() : 대소문자 변환**

문자열을 모두 대문자 또는 소문자로 변환하여 반환한다.

```python
s = "Python"

print(s.upper())  # PYTHON
print(s.lower())  # python

```

---

### **(7) format() : 문자열 포매팅**

문자열 내부에 중괄호 `{}`를 사용해 원하는 변수나 값을 동적으로 삽입한다.

```python
s = "I am {} years old."
print(s.format(20))  # I am 20 years old.

# 여러 개 사용 및 이름 지정 가능
s2 = "{name} likes {food}."
print(s2.format(name="Gisung", food="pizza"))  # Gisung likes pizza.

```

---

### **(8) 문자열 구성 검사 함수들**

문자열의 내용물이 어떤 타입으로 구성되어 있는지 확인하여 `True` 또는 `False`를 반환한다.

```python
print("apple".isalpha())    # True  (모두 알파벳/한글 문자인가?)
print("12345".isnumeric())  # True  (모두 숫자인가?)
print("a123".isalnum())     # True  (모두 알파벳+숫자 조합인가?)

```

---

## **문자열 함수 동작 원리**

이뮤터블 특성에 따른 내부 메모리 처리 방식의 시각화이다.

```text
[ replace() 실행 시 내부 상황 ]

  s ───> [ 메모리 주소 A : "hello" ] (원본 유지)
                │
                ▼ s.replace("h", "x") 실행
         [ 메모리 주소 B : "xello" ] (새로운 객체 생성됨)
                │
                ▼ s = s.replace("h", "x") 대입 시
  s ───> [ 메모리 주소 B : "xello" ] (방향 전환)

```

---

### 정리

- 문자열은 인덱싱과 슬라이싱을 통해 부분 추출이 가능하다.
- 문자열은 이뮤터블(Immutable)이므로, 모든 가공 함수는 원본을 바꾸지 않고 **새 문자열을 반환**한다.
- `split()`은 문자열을 리스트로 쪼개주며, `replace()`는 특정 단어를 치환한다.
- `isalpha()`, `isnumeric()`, `isalnum()`을 통해 문자열의 데이터 성격을 검사할 수 있습니다.
