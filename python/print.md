
**(1) print(" ");**

`print()` 함수는 괄호 안에 문자나 변수를 넣어 화면에 출력한다.

문자열과 변수를 함께 출력할 수 있으며  
쉼표(`,`)를 사용하면 자동으로 공백이 추가된다.

문자열 안에 `\n`을 넣어 줄바꿈을 할 수 있다.

```python
print("Hello, World!")
````

```python
a = 10
print("값:", a)
```

---

**(2) print()와 줄바꿈**

`print()`는 기본적으로 실행 후 자동으로 줄바꿈을 한다.

줄바꿈을 하지 않고 출력하고 싶을 경우
`end` 옵션을 사용한다.

```python
print("Hello", end=" ")
print("World")
```

출력:

```text
Hello World
```

---

**(3) 문자열 포맷팅 (f-string)**

문자열 앞에 `f`를 붙여
문자열 안에 변수 값을 직접 삽입할 수 있다.

```python
a = 3
print(f"출력 {a}")
```

줄바꿈은 `print()`가 자동으로 처리한다.

---

**(4) format() 함수**

`format()` 함수를 사용해 형식화된 문자열을 만들 수 있다.

```python
a = 3
b = 3.14
print("a = {}".format(a))
print("b = {}".format(b))
```

참고:

fomat()함수 보다 (f-string)이 최근에 나왔고 속도도 (f-string)가 더 빠르다

---

**(5) 출력 지시자 (포맷 지정)**

`format()` 또는 f-string에서 출력 형식을 지정할 수 있다.

정수: `d`
실수: `f`
문자열: `s`

```python
a = 3
b = 3.14
str = "안녕"

print(f"a = {a:d}")
print(f"b = {b:f}")
print(f"나는 {str:s}")
```


---

**(6) 실수 자릿수 지정**

소수점 자릿수를 지정해 출력할 수 있다.

```python
pi = 3.141592
print(f"{pi:.2f}")
```

출력:

```text
3.14
```

---

※ 파이썬에는 `printf()` 함수가 없으며
문자열 포맷팅 기능을 사용해 동일한 역할을 수행한다.
