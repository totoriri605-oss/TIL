# 🐍 Python TIL — 리스트(List) 기초

**2026.08.25**

오늘은 Python의 `list`를 공부했다.  
그냥 문법만 외우기보다 **“실제 프로그램에서는 이걸 왜 쓰지?”**를 생각하면서 직접 문제를 풀어봤다.

## 1. 리스트란?

여러 개의 값을 **하나의 변수에 모아서 저장**하는 방법이다.

```python
users = ["민지", "철수", "수아"]
```

쉽게 생각하면:

```text
users라는 상자
┌──────┬──────┬──────┐
│ 민지 │ 철수 │ 수아 │
└──────┴──────┴──────┘
   0      1      2
```

여기서 `0, 1, 2`는 **index(인덱스)**다.

⭐ Python의 인덱스는 **0부터 시작한다.**

---

## 2. 데이터 추가하기

### append() — 맨 뒤에 하나 추가

```python
users = ["민지", "철수"]
users.append("수아")

print(users)
# ["민지", "철수", "수아"]
```

👉 쉽게 말하면 **“맨 뒤에 하나 넣어!”**

### insert() — 원하는 위치에 추가

```python
users.insert(1, "지민")
```

👉 **1번 자리에 지민을 넣어!**

### extend() — 여러 개 한꺼번에 추가

```python
users.extend(["수아", "지민"])
```

⭐ 오늘 기억할 것:

```text
append → 하나 추가
extend → 여러 개 추가
```

---

## 3. 데이터 삭제하기

여기가 처음에는 조금 헷갈렸다.

### remove() — 값으로 삭제

```python
users.remove("철수")
```

👉 **"철수"를 찾아서 삭제**

### pop() — 번호로 꺼내면서 삭제

```python
deleted_user = users.pop(1)
```

`1번`에 있는 데이터를 삭제하면서 가져올 수도 있다.

```python
print(deleted_user)
# 철수
```

### del — 번호로 그냥 삭제

```python
del users[1]
```

### clear() — 전부 비우기

```python
users.clear()

print(users)
# []
```

⭐ 차이 정리:

| 코드 | 내가 이해한 뜻 |
|---|---|
| `remove("철수")` | 철수라는 **값을 찾아 삭제** |
| `pop(1)` | **1번을 꺼내면서 삭제** |
| `del users[1]` | **1번을 그냥 삭제** |
| `clear()` | **전부 삭제** |

---

## 4. 데이터 찾기

### index() — 몇 번 자리에 있지?

```python
users = ["민지", "철수", "수아"]

print(users.index("수아"))
# 2
```

즉, **“수아가 몇 번 자리에 있어?”**라고 Python에게 물어보는 것.

### count() — 몇 개 있지?

```python
orders = ["라떼", "커피", "라떼", "라떼"]

print(orders.count("라떼"))
# 3
```

👉 라떼가 **3개 있다는 뜻.**

---

## 5. 정렬하기

### sort()

```python
scores = [90, 50, 100, 70]
scores.sort()

print(scores)
# [50, 70, 90, 100]
```

작은 값 → 큰 값으로 정렬된다.

### sort(reverse=True)

```python
scores.sort(reverse=True)

print(scores)
# [100, 90, 70, 50]
```

큰 값 → 작은 값으로 정렬된다.

---

## ⚠️ 내가 헷갈릴 수 있었던 부분

### `reverse()` ≠ `sort(reverse=True)`

이 둘은 이름 때문에 비슷해 보이지만 다르다.

```python
numbers = [10, 30, 20, 50]
numbers.reverse()

print(numbers)
# [50, 20, 30, 10]
```

`reverse()`는 숫자 크기를 보는 게 아니다. **그냥 현재 순서를 뒤집는다.**

```text
10 → 30 → 20 → 50

          ↓

50 → 20 → 30 → 10
```

그래서:

```text
sort()               = 정렬
sort(reverse=True)   = 큰 것 → 작은 것 정렬
reverse()            = 현재 순서 뒤집기
```

---

## 6. 개수와 숫자 계산

```python
scores = [60, 80, 100]
```

### len()

```python
len(scores)
# 3
```

👉 **몇 개야?**

### sum()

```python
sum(scores)
# 240
```

👉 **전부 더하면 얼마야?**

### min() / max()

```python
min(scores)
# 60

max(scores)
# 100
```

👉 가장 작은 값 / 가장 큰 값

---

## 7. 평균도 직접 구할 수 있다

```python
scores = [60, 80, 100]

average = sum(scores) / len(scores)

print(average)
# 80.0
```

코드를 한국말로 읽어보면:

> **점수를 전부 더한 값 ÷ 점수의 개수**

즉 평균이다.

---

## 8. `in` — 안에 있어?

```python
users = ["민지", "철수", "수아"]

print("수아" in users)
# True
```

반대로:

```python
print("지민" in users)
# False
```

나는 처음에 이 문제에서 `True`라고 생각했는데, `in`은 **“이 값이 실제로 리스트 안에 있니?”**를 물어보는 것이었다.

```python
"지민" in ["민지", "철수", "수아"]
# False
```

👉 지민은 없으므로 `False`.

---

## 💻 실제 프로그램에서는 어디에 쓸까?

예를 들어 로그인 가능한 사용자를 확인한다고 생각해보자.

```python
allowed_users = ["민지", "철수", "수아"]

if "수아" in allowed_users:
    print("입장 가능")
```

또 쇼핑몰이라면:

```python
cart.append("신발")    # 상품 추가
cart.remove("신발")    # 상품 삭제
len(cart)              # 장바구니 상품 개수
sum(prices)            # 총 주문금액
```

이렇게 오늘 배운 간단한 문법들이 **실제 웹사이트 기능의 기초가 될 수 있다.**

---

## 📝 오늘의 핵심

```text
append()   → 하나 추가
insert()   → 원하는 위치에 추가
extend()   → 여러 개 추가

remove()   → 값으로 삭제
pop()      → 꺼내면서 삭제
del        → 번호로 삭제
clear()    → 전부 삭제

index()    → 위치 찾기
count()    → 개수 세기

sort()     → 정렬
reverse()  → 순서 뒤집기

len()      → 전체 개수
sum()      → 합계
min()      → 최솟값
max()      → 최댓값

in         → 안에 있는지 확인
```

### 오늘의 한 줄 회고

**리스트는 여러 데이터를 모아두는 상자이고, 오늘은 그 상자에 데이터를 추가하고 → 삭제하고 → 찾고 → 정렬하고 → 계산하는 방법을 배웠다.**
