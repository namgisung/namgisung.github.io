---
layout: wiki
title: finally
wiki_name: python
parent: python/예외처리
order: 5
---

## **finally**

finally는 예외 발생 여부와 관계없이 항상 실행되는 블록이다.

주로 파일 닫기, 데이터베이스 연결 종료 등 반드시 수행해야 하는 작업에 사용한다.

---

### **(1) 기본 구조**

```python
try:
    실행문

except 예외:
    예외 처리

finally:
    실행문
```

finally 블록은 항상 실행된다.

---

### **(2) 예외가 발생한 경우**

```python
try:
    print(10 / 0)

except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")

finally:
    print("finally 실행")
```

결과:

```text
0으로 나눌 수 없습니다.
finally 실행
```

예외가 발생해도 finally는 실행된다.

---

### **(3) 예외가 발생하지 않은 경우**

```python
try:
    print(10 / 2)

except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")

finally:
    print("finally 실행")
```

결과:

```text
5.0
finally 실행
```

예외가 없어도 finally는 실행된다.

---

### **(4) else와 함께 사용**

```python
try:
    print(10 / 2)

except ZeroDivisionError:
    print("오류 발생")

else:
    print("정상 실행")

finally:
    print("프로그램 종료")
```

결과:

```text
5.0
정상 실행
프로그램 종료
```

---

### **(5) 실행 순서**

```python
try:
    실행문

except:
    예외 처리

else:
    실행문

finally:
    실행문
```

예외 발생

```text
try → except → finally
```

예외 없음

```text
try → else → finally
```

---

### **(6) 파일 처리 예시**

```python
f = open("test.txt", "r")

try:
    data = f.read()

finally:
    f.close()
```

finally를 사용하면 예외가 발생하더라도 파일을 닫을 수 있다.

---

### 정리

- finally는 항상 실행된다.
- 예외 발생 여부와 관계없이 실행된다.
- 주로 자원 정리에 사용한다.
- try, except, else와 함께 사용할 수 있다.
