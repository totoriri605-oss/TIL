# TIL — Python 조건문 이해하기

## 오늘 배운 내용

오늘은 조건에 따라 다른 코드를 실행하는 `if`, `else`, `elif`와 논리 연산자 `and`, `or`, `not`을 배웠다.

코드를 외우기보다 조건을 사람 말로 바꾸고, 실행 전에 `True`인지 `False`인지 먼저 예상해 보면서 실습했다.

---

## 1. 비교 결과는 True 또는 False

```python
score = 59
print(score >= 60)
```

결과:

```text
False
```

`score >= 60`은 "score가 60보다 크거나 같은가?"라는 뜻이다.

### 경계값 확인

`>= 60`과 `> 60`은 다르다.

```text
score >= 60  → 60 포함
score > 60   → 60 포함하지 않음
```

조건을 테스트할 때는 아무 숫자만 넣기보다 경계값 바로 아래, 경계값, 바로 위를 확인하면 좋다.

```text
59 → 바로 아래
60 → 경계값
61 → 바로 위
```

---

## 2. if — 조건이 맞으면 실행

```python
score = 80

if score >= 60:
    print("통과입니다.")
```

사람 말로 읽으면:

> 만약(if) 점수가 60 이상이라면 "통과입니다."를 출력한다.

### 콜론과 들여쓰기

```python
if score >= 60:
    print("통과입니다.")
```

`if` 조건식 끝에는 `:`을 붙인다.

그리고 `print()` 앞의 빈칸은 단순히 보기 좋게 만드는 것이 아니라 파이썬 문법인 **들여쓰기**이다.

쉽게 생각하면:

```text
if 조건:
    조건이 맞으면 할 일
```

---

## 3. else — 위 조건이 아니면 실행

```python
temperature = int(input("온도 : "))

if temperature >= 30:
    print("더워요!")
else:
    print("신선해요!")
```

`else`는 "그게 아니면"이라고 이해했다.

### 내가 헷갈렸던 부분

처음에는 다음처럼 조건을 또 붙였다.

```python
else temperature > 30:  # 잘못된 문법
```

하지만 `else` 자체가 이미 "위 조건이 아니면"이라는 뜻이므로 조건을 붙이지 않는다.

```python
else:
    print("신선해요!")
```

기본 구조:

```text
if 조건:
    참이면 할 일
else:
    거짓이면 할 일
```

---

## 4. elif — 다른 조건을 이어서 확인

```python
score = 85

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("D")
```

`elif`는 "그게 아니면 이 조건은 어때?"라고 이해했다.

파이썬은 위에서부터 조건을 확인한다.

```text
85 >= 90 → False
85 >= 80 → True
→ B 출력
```

85는 70 이상이기도 하지만, `if / elif / else`에서는 위에서부터 확인하다가 처음으로 `True`가 된 곳을 실행하고 끝난다.

쉽게 기억하면:

```text
if   → 만약 이거면?
elif → 아니면 이거는?
elif → 그것도 아니면 이거는?
else → 다 아니면?
```

---

## 5. 논리 연산자 and / or / not

오늘은 여러 조건을 함께 판단하는 방법도 배웠다.

```text
and = 모두 만족해야 True
or  = 하나라도 만족하면 True
not = True와 False를 반대로
```

### and

```python
age = 25

if age >= 20 and age < 30:
    print("20대입니다.")
```

두 조건이 모두 맞아야 실행된다.

```text
True and True  → True
True and False → False
```

### or

```python
day = "토요일"

if day == "토요일" or day == "일요일":
    print("주말입니다.")
```

둘 중 하나라도 맞으면 `True`가 된다.

### not

```python
is_closed = False

if not is_closed:
    print("현재 이용할 수 있습니다.")
```

`not`은 결과를 반대로 바꾼다고 이해했다.

```text
not False → True
not True  → False
```

---

## 6. 직접 실습한 무료배송 문제

```python
order_amount = 48000
is_member = True

if order_amount >= 50000 or is_member:
    print("무료배송입니다.")
else:
    print("배송비가 있습니다.")
```

조건을 하나씩 보면:

```text
48000 >= 50000 → False
is_member       → True

False or True → True
```

`or`는 둘 중 하나라도 `True`이면 전체가 `True`이므로 결과는 다음과 같다.

```text
무료배송입니다.
```

---

## 7. 내가 틀렸던 or 문제

이번에는 다음과 같은 값이었다.

```python
order_amount = 48000
is_member = False
```

처음에는 무료배송이라고 예상했지만 다시 조건을 나누어 보니:

```text
48000 >= 50000 → False
is_member       → False

False or False → False
```

둘 다 `False`이기 때문에 실제 결과는:

```text
배송비가 있습니다.
```

여기서 `or`는 **하나라도 True여야 True**라는 것을 다시 확인했다.

---

## 8. 실습 중 만난 오류 — true와 True

처음에는 다음처럼 작성했다.

```python
is_member = true
```

그러자 `NameError`가 발생했다.

파이썬의 참/거짓 값은 다음처럼 첫 글자를 대문자로 작성해야 한다.

```python
is_member = True
is_member = False
```

```text
true  → 잘못된 작성
True  → 올바른 작성
false → 잘못된 작성
False → 올바른 작성
```

---

## 9. 이전 내용 복습 — f-string은 문장을 외우는 것이 아니다

이전 실습에서 사용했던 코드:

```python
print(f"{first_num} 더하기 {second_num}은 {result} 입니다.")
```

처음에는 이 문장 전체를 외워야 하는 줄 알았지만, 중요한 것은 f-string의 구조였다.

```python
f"문장 {변수} 문장"
```

`{ }` 안에 변수를 넣으면 그 변수에 저장된 값이 문장 안에 들어간다.

예:

```python
name = "정민"
print(f"안녕하세요. {name}님!")
```

즉 출력 문장은 상황에 따라 자유롭게 바꿀 수 있고, `f"...{변수}..."`라는 구조를 이해하는 것이 중요하다.

---

## 오늘의 정리

- 비교식의 결과는 `True` 또는 `False`이다.
- `if`는 조건이 `True`일 때 실행한다.
- `else`는 위 조건이 `False`일 때 실행한다.
- `else`에는 새로운 조건을 붙이지 않는다.
- 여러 조건을 순서대로 확인하려면 `elif`를 사용한다.
- `if / elif / else`는 위에서부터 확인하고 처음 만족한 곳을 실행한다.
- `:`과 들여쓰기도 파이썬의 중요한 문법이다.
- `and`는 모두 만족해야 한다.
- `or`는 하나라도 만족하면 된다.
- `not`은 참과 거짓을 반대로 바꾼다.
- 파이썬에서는 `true`가 아니라 `True`, `false`가 아니라 `False`라고 작성한다.
- 조건의 경계값 바로 아래, 경계값, 바로 위를 테스트하는 습관을 들이면 좋다.

## 오늘의 한 줄

> 조건문은 파이썬에게 "이 조건이 맞으면 이 일을 하고, 아니면 다른 일을 해"라고 선택 방법을 알려주는 문법이다.

코드를 바로 실행하기 전에 조건이 `True`인지 `False`인지 먼저 예상하고, 직접 실행한 뒤 예상과 다른 이유를 찾아보는 방식으로 연습했다.
