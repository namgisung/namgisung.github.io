---
layout: wiki
title: assert
wiki_name: python
parent: python/예외처리
order: 7
---

## **assert**

assert는 조건이 참(True)인지 검사하는 키워드이다.

조건이 거짓(False)이면 AssertionError 예외가 발생한다.

주로 디버깅이나 프로그램의 논리 검증에 사용한다.

---

### **(1) 기본 구조**

```python
assert 조건식
```

조건식이 True이면 아무 일도 발생하지 않는다.

조건식이 False이면 AssertionError가 발생한다.

---

### **(2) 조건이 참인 경우**

```python
age = 20

assert age > 0

print("정상 실행")
```

결과:

```text
정상 실행
```

조건이 참이므로 예외가 발생하지 않는다.

---

### **(3) 조건이 거짓인 경우**

```python
age = -1

assert age > 0
```

결과:

```text
AssertionError
```

조건이 거짓이므로 AssertionError가 발생한다.

---

### **(4) 오류 메시지 추가**

```python
age = -1

assert age > 0, "나이는 양수여야 합니다."
```

결과:

```text
AssertionError: 나이는 양수여야 합니다.
```

오류 메시지를 함께 출력할 수 있다.

---

### **(5) 함수에서 사용**

```python
def divide(a, b):

    assert b != 0, "0으로 나눌 수 없습니다."

    return a / b
```

함수의 입력값을 검증할 때 사용할 수 있다.

---

### **(6) raise와 비교**

| 구분 | assert | raise |
|--------|--------|--------|
| 목적 | 조건 검증 | 예외 발생 |
| 실패 시 | AssertionError 발생 | 지정한 예외 발생 |
| 사용 예 | 디버깅, 논리 검증 | 입력값 검증, 오류 처리 |

예시

```python
assert age > 0
```

```python
raise ValueError("나이는 양수여야 합니다.")
```

---

### **(7) assert의 동작**

```python
assert x > 0
```

은 내부적으로 다음과 비슷하게 동작한다.

```python
if not x > 0:
    raise AssertionError
```

---

## 정리

- assert는 조건을 검사하는 키워드이다.
- 조건이 거짓이면 AssertionError가 발생한다.
- 디버깅과 프로그램 검증에 사용된다.
- 오류 메시지를 함께 작성할 수 있다.
- 내부적으로 AssertionError를 발생시킨다.
