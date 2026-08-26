# 🐍 Python TIL — 함수(Function) 기초

**2026.08.26**

오늘은 Python의 **함수(function)** 를 공부했다.  
처음에는 `def`, 매개변수, 인수, `return` 같은 용어가 한꺼번에 나와서 헷갈렸지만, 문제를 하나씩 풀면서 **함수는 하나의 역할을 묶어서 이름을 붙이고 다시 사용할 수 있게 하는 방법**이라는 흐름을 이해했다.

---

## 1. 함수는 왜 사용할까?

같은 코드를 여러 번 작성하면 수정할 곳도 많아진다.

```python
print("안녕하세요!")
print("공부를 시작합니다!")

print("안녕하세요!")
print("공부를 시작합니다!")
```

함수로 묶으면 한 번 정의한 뒤 여러 번 사용할 수 있다.

```python
def greet():
    print("안녕하세요!")
    print("공부를 시작합니다!")

greet()
greet()
```

내가 이해한 함수의 핵심은 단순히 코드를 줄이는 것이 아니라,

> **하나의 작업에 이름을 붙이는 것**

이다.

예를 들어:

```python
save_client_info()
calculate_total()
show_profile()
```

처럼 이름만 봐도 무슨 일을 하는 함수인지 예상할 수 있다.

---

## 2. 함수 정의와 호출

### 함수 정의 = 만들기

```python
def say_hello():
    print("Hello, Python!")
```

`def`는 함수를 **정의할 때 사용하는 키워드**다.

함수를 정의했다고 바로 실행되는 것은 아니다.

### 함수 호출 = 실행하기

```python
say_hello()
```

함수 이름 뒤에 `()`를 붙여 호출해야 함수 안의 코드가 실행된다.

```text
def 함수이름():  → 함수 만들기
함수이름()       → 함수 실행하기
```

⭐ 오늘 처음에 가장 헷갈렸던 부분은 `def`를 만나면 바로 함수 안의 코드가 실행된다고 생각했던 것이다.

하지만 실제로는 **정의만 해 두고, 호출했을 때 실행된다.**

---

## 3. 함수 이름은 역할이 보이게 짓기

```python
def f():
    print("학생 정보를 출력합니다.")
```

보다

```python
def show_student_info():
    print("학생 정보를 출력합니다.")
```

가 훨씬 이해하기 쉽다.

Python 함수 이름에는 보통 `snake_case`를 사용한다.

```python
show_menu()
calculate_total()
get_average()
print_profile()
```

자주 보이는 영어도 함께 기억해 두면 코드를 읽기 쉬워진다.

| 영어 | 뜻 |
|---|---|
| `show` | 보여주다 |
| `get` | 가져오다 |
| `save` | 저장하다 |
| `calculate` | 계산하다 |
| `check` | 확인하다 |
| `create` | 만들다 |
| `delete` | 삭제하다 |
| `average` | 평균 |
| `total` | 합계 |

---

## 4. 매개변수와 인수

사람마다 다른 이름으로 인사하려면 값을 함수에 전달할 수 있다.

```python
def greet(name):
    print(f"안녕하세요, {name}님!")

greet("민수")
```

여기서:

```text
name     → 매개변수(parameter)
"민수"   → 인수(argument)
```

내가 이해한 방법:

> **매개변수 = 값을 받을 자리**  
> **인수 = 실제로 넣는 값**

```python
def show_profile(name, age, city):
    print(name)
    print(age)
    print(city)

show_profile("지영", 22, "부산")
```

값은 순서대로 들어간다.

```text
name ← "지영"
age  ← 22
city ← "부산"
```

매개변수를 추가할 수도 있다.

```python
def show_profile(name, age, city, language):
    print(f"학습 언어: {language}")
```

---

## 5. return — 결과를 함수 밖으로 돌려주기

```python
def add(a, b):
    return a + b

result = add(5, 3)
```

실행 흐름:

```text
a ← 5
b ← 3
↓
5 + 3 = 8
↓
return 8
↓
result = 8
```

즉 `return`은 계산한 값을 **함수 밖으로 돌려준다.**

반환된 값은 변수에 저장하고 다시 사용할 수 있다.

```python
def multiply(a, b):
    return a * b

price = multiply(12000, 3)
final_price = price + 5000

print(price)        # 36000
print(final_price)  # 41000
```

⭐ `return`으로 받은 값을 다음 계산에서 다시 사용할 수 있다는 점이 중요하다.

---

## 6. print()와 return의 차이

이 부분이 오늘 가장 중요했다.

### print() = 사람에게 보여주기

```python
def add_print(a, b):
    print(a + b)
```

### return = 프로그램에 결과 돌려주기

```python
def add_return(a, b):
    return a + b
```

정리하면:

```text
print() → 화면에 보여주기 👀
return  → 결과를 함수 밖으로 보내기 📤
```

예를 들어:

```python
def show_total(a, b):
    print(a + b)

result = show_total(10, 20)
print(result)
```

화면에는 먼저 `30`이 보이지만 `return`이 없기 때문에 `result`에 30이 저장되지는 않는다.

```text
30
None
```

`None`은 지금 단계에서는 **돌려받은 값이 없음**이라고 이해했다.

---

## 7. 함수는 여러 값을 반환할 수 있다

```python
def calculate(a, b):
    total = a + b
    difference = a - b
    return total, difference
```

```python
total, difference = calculate(10, 3)
```

함수가 돌려준 값은:

```text
(13, 7)
```

처럼 여러 값을 묶어 받을 수 있고, 튜플에서 배운 **언패킹**으로 나눠 저장할 수 있다.

```text
total      ← 13
difference ← 7
```

### 직접 만든 합계와 평균 함수

```python
def calculate_summary(a, b):
    total = a + b
    average = (a + b) / 2
    return total, average
```

```python
total, average = calculate_summary(80, 100)
```

결과:

```text
total = 180
average = 90.0
```

평균을 구할 때는 먼저 더한 뒤 나눠야 하므로 괄호가 중요하다.

```python
(a + b) / 2
```

---

## 8. 기본값 매개변수

값을 전달하지 않았을 때 사용할 기본값을 미리 정할 수 있다.

```python
def greet(name, message="안녕하세요"):
    print(f"{message}, {name}님!")
```

```python
greet("민수")
```

`message`를 따로 주지 않았으므로 기본값인 `"안녕하세요"`가 사용된다.

반대로:

```python
greet("민수", "반갑습니다")
```

처럼 직접 값을 전달하면 내가 전달한 값이 사용된다.

```text
값을 안 줌 → 기본값 사용
값을 직접 줌 → 전달한 값 사용
```

---

## 9. 키워드 인수

일반적으로 인수는 위치에 따라 전달된다.

```python
show_profile("민수", 20, "서울")
```

하지만 매개변수 이름을 직접 지정할 수도 있다.

```python
show_profile(
    city="부산",
    name="지영",
    age=22
)
```

이 경우 순서가 달라도 이름을 보고 값이 전달된다.

```text
city ← "부산"
name ← "지영"
age  ← 22
```

내가 이해한 키워드 인수의 장점은 **어떤 값이 어디로 들어가는지 코드만 보고 알기 쉽다는 것**이다.

---

## 10. 지역 변수

함수 안에서 만든 변수는 **지역 변수(local variable)** 라고 한다.

```python
def calculate_total(price, quantity):
    total = price * quantity
    return total

result = calculate_total(12000, 3)
```

역할을 구분하면:

```text
price, quantity → 함수가 받은 값(매개변수)
total           → 함수 안에서 만든 지역 변수
result          → 함수 밖에서 반환값을 저장한 변수
```

`total`과 `result`는 값이 같을 수 있어도 **같은 변수는 아니다.**

함수 안에서만 필요한 값은 함수 안에서 관리하고, 밖에서 필요한 결과는 `return`으로 보내는 방식이 이해하기 쉽다.

---

## 11. 함수 안에 조건문을 넣을 수 있다

```python
def get_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    else:
        return "C"
```

새로운 조건문 규칙이 생긴 것이 아니다.

이전에 배운 `if / elif / else`를 **점수에 따라 등급을 구하는 하나의 역할**로 함수 안에 묶은 것이다.

```python
print(get_grade(95))  # A
print(get_grade(85))  # B
print(get_grade(70))  # C
```

---

## 12. 함수 안에 반복문과 리스트도 넣을 수 있다

```python
def calculate_total(scores):
    total = 0

    for score in scores:
        total += score

    return total
```

```python
scores = [80, 90, 100]
result = calculate_total(scores)
print(result)
```

여기서도 새로운 반복 규칙이 생긴 것이 아니다.

> **리스트 + 반복문 + return을 하나의 역할로 묶은 것**

이라고 이해했다.

### 리스트 평균 함수 구조

```python
def calculate_average(scores):
    total = sum(scores)
    average = total / len(scores)
    return average
```

여기서는:

```text
입력   → scores
처리   → 합계 ÷ 개수
반환   → average
```

처럼 **입력 → 처리 → 반환**으로 생각하면 함수의 흐름을 읽기 쉬워진다.

---

## 13. 긴 코드는 역할별로 함수로 나눌 수 있다

예를 들어 주문 프로그램이라면:

```python
def calculate_product_total(price, quantity):
    return price * quantity


def calculate_discount(total, rate):
    return total * rate


def show_result(total):
    print(f"최종 금액: {total}원")
```

이렇게 역할을 나눌 수 있다.

하지만 **모든 한 줄을 함수로 만들 필요는 없다.**

함수를 만드는 기준은:

- 같은 작업이 반복될 때
- 하나의 역할로 묶으면 이해하기 쉬울 때
- 긴 코드를 역할별로 나누면 읽기 쉬워질 때

이라고 이해했다.

---

## 14. 함수 오류를 확인하는 순서

함수가 예상대로 동작하지 않으면 무작정 여러 줄을 고치기보다 흐름을 따라 확인한다.

```text
1. 함수가 실제로 호출되었는가?
2. 전달한 인수의 개수와 순서는 맞는가?
3. 매개변수에는 어떤 값이 들어갔는가?
4. 지역 변수를 함수 밖에서 사용하지 않았는가?
5. 필요한 결과를 return하고 있는가?
6. return된 값을 어디에 저장했는가?
```

### 자주 생길 수 있는 실수

```python
greet
```

함수 이름만 적으면 실행되지 않는다.

```python
greet()
```

처럼 호출해야 한다.

또:

```python
def add(a, b):
    return a + b

add(10)
```

처럼 매개변수는 두 개인데 인수를 하나만 주면 문제가 생긴다.

그리고:

```python
def add(a, b):
    a + b
```

계산만 하고 `return`하지 않으면 계산 결과를 함수 밖에서 받을 수 없다.

---

## 15. 오늘 배운 내용을 하나로 연결하기

함수는 결국 다음 흐름으로 생각할 수 있다.

```text
인수 전달 📥
   ↓
매개변수가 값 받기
   ↓
함수 안에서 처리
조건문 / 반복문 / 리스트 등 사용 가능
   ↓
return으로 결과 반환 📤
   ↓
함수 밖 변수에 저장
   ↓
다른 코드에서 다시 사용
```

---

## 📝 오늘의 핵심

```text
def       → 함수 정의하기
함수이름() → 함수 호출하기

매개변수   → 값을 받을 자리
인수       → 실제 전달하는 값

print()   → 화면에 보여주기
return    → 결과를 함수 밖으로 돌려주기

기본값 매개변수 → 값을 안 줬을 때 사용할 값
키워드 인수     → 매개변수 이름을 지정해 값 전달
지역 변수       → 함수 안에서 만든 변수

함수 안에는
조건문 / 반복문 / 리스트 등
기존에 배운 문법을 함께 사용할 수 있다.
```

### 오늘의 한 줄 회고

**함수는 어려운 새 문법을 따로 만드는 것이 아니라, 지금까지 배운 코드를 하나의 역할로 묶고 이름을 붙여 다시 사용할 수 있게 만드는 방법이라는 것을 배웠다.**
