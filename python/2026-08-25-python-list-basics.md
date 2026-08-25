# 2026-08-25 Python TIL - 리스트 기초

오늘은 Python의 **리스트(list)** 를 직접 문제로 풀어보면서 기본 사용법을 연습했다.

## 1. 리스트에 값 추가하기

```python
menu = ["커피", "말차"]

menu.append("주스")          # 맨 뒤에 하나 추가
menu.insert(1, "라떼")      # 원하는 위치에 추가
menu.extend(["차", "우유"]) # 여러 개를 한꺼번에 추가
```

- `append()` : 하나 추가
- `insert()` : 원하는 위치에 추가
- `extend()` : 여러 개 추가

## 2. 리스트에서 값 삭제하기

```python
menu = ["커피", "말차", "라떼", "주스"]

menu.remove("말차")  # 값(이름)을 찾아서 삭제
menu.pop(1)          # 해당 인덱스의 값을 꺼내면서 삭제
del menu[0]          # 해당 인덱스의 값을 그냥 삭제
menu.clear()         # 리스트 내용 전체 삭제
```

### remove와 pop의 차이

```python
menu.remove("말차") # '말차'라는 값을 찾아 삭제
menu.pop(1)         # 1번 위치의 값을 꺼내면서 삭제
```

`pop()`은 삭제한 값을 변수에 저장할 수도 있다.

```python
users = ["민지", "철수", "수아"]
deleted_user = users.pop(1)

print(deleted_user)  # 철수
print(users)         # ['민지', '수아']
```

## 3. index와 count

```python
users = ["민지", "철수", "수아"]
print(users.index("수아"))  # 2
```

- `index()` : 이 값이 몇 번 위치에 있는지 찾기

```python
orders = ["라떼", "커피", "라떼", "말차", "라떼"]
print(orders.count("라떼"))  # 3
```

- `count()` : 같은 값이 몇 개 있는지 세기

## 4. 정렬과 뒤집기

```python
scores = [90, 50, 100, 70]
scores.sort()
print(scores)
# [50, 70, 90, 100]
```

```python
scores.sort(reverse=True)
print(scores)
# [100, 90, 70, 50]
```

- `sort()` : 작은 값부터 큰 값 순서로 정렬
- `sort(reverse=True)` : 큰 값부터 작은 값 순서로 정렬

`reverse()`는 정렬이 아니라 **현재 순서를 그대로 뒤집는다.**

```python
a = [10, 30, 20, 50]
a.reverse()
print(a)
# [50, 20, 30, 10]
```

## 5. len, sum, min, max

```python
scores = [60, 80, 100]

print(len(scores))  # 3
print(sum(scores))  # 240
print(min(scores))  # 60
print(max(scores))  # 100
```

- `len()` : 몇 개 있는지
- `sum()` : 전부 더하기
- `min()` : 가장 작은 값
- `max()` : 가장 큰 값

### 평균 구하기

```python
scores = [60, 80, 100]
average = sum(scores) / len(scores)

print(average)
# 80.0
```

평균은 **전체 합계 / 데이터 개수**로 구할 수 있다.

## 6. in으로 값이 있는지 확인하기

```python
users = ["민지", "철수", "수아"]

print("수아" in users)  # True
print("지민" in users)  # False
```

`in`은 쉽게 말하면 **"이 값이 안에 있어?"** 라고 확인하는 것이다.

실제 프로그램에서는 조건문과 함께 사용할 수 있다.

```python
allowed_users = ["민지", "철수", "수아"]

if "수아" in allowed_users:
    print("입장 가능")
```

## 오늘의 핵심 정리

| 코드 | 의미 |
|---|---|
| `append()` | 맨 뒤에 하나 추가 |
| `insert()` | 원하는 위치에 추가 |
| `extend()` | 여러 개 추가 |
| `remove()` | 값으로 삭제 |
| `pop()` | 인덱스로 꺼내면서 삭제 |
| `del` | 인덱스로 삭제 |
| `clear()` | 전체 비우기 |
| `index()` | 값의 위치 찾기 |
| `count()` | 값의 개수 세기 |
| `sort()` | 정렬하기 |
| `reverse()` | 현재 순서 뒤집기 |
| `len()` | 전체 개수 |
| `sum()` | 숫자 합계 |
| `min()` | 최솟값 |
| `max()` | 최댓값 |
| `in` | 값이 포함되어 있는지 확인 |

## 오늘 헷갈렸던 포인트

### 인덱스와 개수는 다르다

```python
cart = ["신발", "모자", "가방", "양말"]
```

인덱스는 `0, 1, 2, 3`이지만 `len(cart)`의 결과는 `4`이다.

### reverse()와 sort(reverse=True)는 다르다

- `reverse()` : 현재 순서를 그냥 뒤집는다.
- `sort(reverse=True)` : 값을 큰 것부터 작은 것 순서로 정렬한다.

## 한 줄 회고

리스트는 여러 데이터를 한곳에 저장하고 **추가 → 삭제 → 검색 → 정렬 → 계산 → 포함 여부 확인**을 할 수 있는 자료구조라는 것을 배웠다.
