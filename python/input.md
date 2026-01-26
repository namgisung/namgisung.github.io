

먼저 파이썬에서는 입력을 받기 위해 별도의 import가 필요 없다.

입력을 받기 위해 `input()` 함수를 사용한다.
```python
input()
````

그리고 입력받은 값을 저장할 변수를 선언해 준다.

```python
user_input = input()
```

`input()`으로 받은 값은 **항상 문자열(str)** 형태로 저장된다.

```python
text = input()
print(text)
```

---

정수로 입력을 받고 싶을 경우 `int()`를 사용해 형 변환을 해준다.

```python
num = int(input())
print(num)
```

실수로 입력을 받을 경우 `float()`를 사용한다.

```python
value = float(input())
print(value)
```

---

문자열을 먼저 선언한 뒤 입력을 받아 저장하는 것도 가능하다.

```python
data = None
data = input()
print(data)
```

---

출력을 할 때는 `print()` 함수를 사용한다.

```python
print("출력 예시")
print(user_input)
```

---

한 줄에 여러 개의 값을 입력받을 경우
`split()`을 사용해 공백 기준으로 나눈 후 형 변환을 해준다.

```python
a, b = input().split()
print(a, b)
```

정수로 사용하려면 `map()`을 이용한다.

```python
a, b = map(int, input().split())
print(a, b)
```

```text
5 5   // 입력
5 5   // 출력
```

※ 파이썬에는 `nextInt()`, `nextLine()` 같은 구분된 입력 함수가 없으며
`input()` 하나로 모든 입력을 처리한다.
 

어느 걸로 갈까?
```
