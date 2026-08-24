# TIL — Python 반복문: for, while, break, continue, 중첩 반복문

## 오늘 배운 내용

오늘은 Python의 `for`, `while` 반복문과 `range()`, `break`, `continue`, 중첩 반복문, 누적 변수에 대해 공부했다.

처음에는 반복문이 복잡해 보였지만, 코드를 볼 때 다음 네 가지를 확인하면 조금씩 읽을 수 있다는 것을 배웠다.

1. 무엇을 반복하는가?
2. 몇 번 반복하는가?
3. 반복할 때 변수는 어떻게 바뀌는가?
4. 언제 반복이 끝나는가?

---

## 1. for 반복문

```python
for i in range(3):
    print(i)
```

`range(3)`은 `0, 1, 2`를 만든다. `i`에 숫자가 하나씩 들어가고 `print(i)`가 총 3번 실행된다.

```text
0
1
2
```

`for`문을 읽을 때는 들여쓰기 된 부분을 보고 무엇을 반복하는지 확인한다.

---

## 2. range() 사용하기

### `range(5)`

`range(5)`는 `0, 1, 2, 3, 4`를 만든다. 끝 숫자인 `5`는 포함되지 않는다.

### `range(1, 6)`

`1`부터 시작하고 `6`이 되기 전에 멈추기 때문에 `1, 2, 3, 4, 5`가 만들어진다.

### `range(2, 7, 2)`

```python
for i in range(2, 7, 2):
    print(i)
```

- `2`에서 시작한다.
- `7`이 되기 전에 멈춘다.
- 숫자가 2씩 증가한다.

실행 결과:

```text
2
4
6
```

---

## 3. while 반복문

```python
count = 1

while count <= 3:
    print(f"현재 count: {count}")
    count += 1

print("종료")
```

`count`가 3 이하인 동안 반복한다. `count`가 `1 → 2 → 3 → 4`로 바뀌고, 4가 되면 `4 <= 3`이 거짓이므로 반복이 끝난다.

```text
현재 count: 1
현재 count: 2
현재 count: 3
종료
```

`count += 1`은 현재 `count`에 1을 더해서 다시 저장한다는 뜻이다. 이 코드가 없으면 `count`가 계속 1이어서 무한 반복될 수 있다.

---

## 4. break와 continue

### break

`break`는 반복문을 완전히 끝낸다.

```python
for number in range(1, 6):
    if number == 3:
        break
    print(number)
```

`number`가 3이 되면 출력하기 전에 반복문이 끝난다.

```text
1
2
```

### continue

`continue`는 반복문 전체를 끝내지 않고 이번 차례만 건너뛴다.

```python
for number in range(1, 6):
    if number == 3:
        continue
    print(number)
```

숫자 3만 출력하지 않고 다음 숫자로 넘어간다.

```text
1
2
4
5
```

```text
break    = 반복문을 완전히 끝내기
continue = 이번 차례만 건너뛰기
```

---

## 5. 중첩 반복문

반복문 안에 다른 반복문이 들어갈 수 있다.

```python
for row in range(3):
    for column in range(4):
        print("*", end="")
    print()
```

- `row`는 줄을 3번 만든다.
- `column`은 각 줄에 별을 4개 출력한다.
- `end=""`는 별을 출력한 뒤 줄을 바꾸지 않고 옆에 붙인다.
- 내용이 없는 `print()`는 다음 줄로 이동한다.

```text
****
****
****
```

중첩 반복문에서는 바깥쪽 변수 하나가 유지되는 동안 안쪽 반복문이 처음부터 끝까지 실행된다.

```python
for row in range(1, 3):
    for column in range(1, 4):
        print(f"row={row}, column={column}")
```

```text
row=1, column=1
row=1, column=2
row=1, column=3
row=2, column=1
row=2, column=2
row=2, column=3
```

---

## 6. 누적 변수

누적 변수는 값을 계속 모으는 변수다.

```python
total = 0

for number in range(1, 4):
    total += number

print(total)
```

`total`의 변화:

```text
처음: total = 0
number = 1 → total = 1
number = 2 → total = 3
number = 3 → total = 6
```

실행 결과는 `6`이다. 실제 프로그램에서는 같은 원리로 매출 합계, 장바구니 총금액, 점수 합계 등을 계산할 수 있다.

---

## 오늘 발생한 오류

### 콜론 누락

```python
for row in range(3)
```

끝에 콜론 `:`이 빠져 `SyntaxError: expected ':'` 오류가 발생했다.

```python
for row in range(3):
```

### 잘못된 폴더 이름 입력

실제 폴더는 `chapter10`인데 다음과 같이 입력했다.

```powershell
python chapter20/02.py
```

존재하지 않는 폴더를 입력해 파일을 찾을 수 없었다. 올바른 명령어는 다음과 같다.

```powershell
python chapter10/02.py
```

---

## 오늘의 핵심 정리

반복문을 볼 때는 다음 네 가지를 먼저 확인한다.

```text
1. 무엇을 반복하는가?
2. 몇 번 반복하는가?
3. 변수는 어떻게 바뀌는가?
4. 언제 반복이 끝나는가?
```

아직 중첩 반복문과 `continue`는 조금 더 연습해야 하지만, 코드를 무작정 외우지 않고 실행 순서를 한 줄씩 따라가는 방법을 배웠다.
---

## 조건문 복습에서 새롭게 이해한 점

조건문을 잘 작성한다는 것은 `if` 문법을 외우는 것만을 뜻하지 않는다.

실제 상황을 어떤 기준으로 나눌지 정하고, 기준과 정확히 같은 값도 올바르게 처리되는지 확인해야 한다.

예를 들어 예약금이 30,000원 이상일 때 예약을 확정한다면:

```python
if deposit >= 30000:
    print("예약 확정")
else:
    print("예약금 부족")
```

다음 세 가지 값으로 확인할 수 있다.

- 29,999원 → 예약금 부족
- 30,000원 → 예약 확정
- 30,001원 → 예약 확정

이처럼 기준 바로 아래, 기준과 같은 값, 기준 바로 위를 확인하는 것을 **경계값 테스트**라고 한다.

또한 오류를 검증한다는 것은 오류를 처음부터 혼자 맞히는 것이 아니다.

오류 메시지와 줄 번호를 확인하고, 원인을 하나 예상해 수정한 뒤 다시 실행해서 예상한 결과가 나오는지 확인하는 과정이라는 것을 배웠다.
