# TIL | Python 모듈·패키지와 가상환경

## 오늘 배운 것

오늘은 Python 프로젝트에서 코드를 역할별로 나누는 **모듈과 패키지**, 외부 패키지를 설치하는 **pip**, 프로젝트마다 실행 환경을 나누는 **가상환경(.venv)**을 공부했다.

처음에는 `.venv`, `pip`, `requirements.txt` 같은 용어가 모두 비슷해 보여 헷갈렸지만, 직접 가상환경을 만들고 패키지를 설치해보면서 각각의 역할이 연결되기 시작했다.

---

## 1. 함수 → 모듈 → 패키지

프로그램이 작을 때는 하나의 파일에 여러 함수를 작성해도 괜찮다. 하지만 코드가 많아지면 원하는 기능을 찾고 수정하기 어려워진다.

```text
함수
→ 하나의 기능을 묶음

모듈
→ 관련 코드를 하나의 .py 파일로 묶음

패키지
→ 관련 모듈을 하나의 폴더로 묶음
```

예를 들어:

```text
shop/
├── price.py
└── delivery.py
```

- `shop` → 패키지
- `price.py` → 모듈
- `delivery.py` → 모듈
- 모듈 안의 `calculate_total()` → 함수

파일을 많이 만드는 것이 목적이 아니라 **코드의 역할을 나누어 찾고 수정하고 관리하기 쉽게 만드는 것**이 목적이다.

---

## 2. import

다른 모듈의 기능을 사용하려면 `import`를 사용한다.

```python
import math

print(math.sqrt(25))
```

`math.sqrt(25)`는 **math 모듈에 있는 sqrt 기능을 사용한다**고 읽을 수 있다.

### import 방법

```python
import math
```

모듈을 불러오고 `math.sqrt()`처럼 사용한다.

```python
from math import sqrt
```

`math`에서 `sqrt`만 가져오기 때문에 `sqrt()`라고 바로 사용할 수 있다.

```python
import statistics as stats
```

`statistics`를 불러오고 앞으로 `stats`라는 별명으로 사용한다.

```python
stats.mean([80, 90, 100])
```

---

## 3. 내가 만든 .py 파일도 모듈이 된다

예를 들어 `calculator.py`라는 파일을 만들었다면 다른 Python 파일에서:

```python
import calculator
```

처럼 불러올 수 있다.

즉 **직접 만든 `.py` 파일도 모듈이 될 수 있다.**

---

## 4. pip와 import의 차이

오늘 가장 중요하게 구분한 부분이다.

```text
pip install
→ 외부 패키지를 설치

import
→ 설치되어 있거나 사용할 수 있는 기능을 Python 코드에서 불러오기
```

예를 들어 `requests`를 설치할 때:

```bash
python -m pip install requests
```

Python 코드에서 사용할 때:

```python
import requests
```

`requests`는 웹이나 API 등에 요청을 보낼 때 사용할 수 있는 외부 패키지다. 오늘은 requests 사용법 자체보다 **외부 패키지를 설치하고 불러오는 과정**을 이해하기 위한 예제로 사용했다.

---

## 5. pip 명령어

```bash
python -m pip --version
```

현재 Python과 연결된 pip의 버전과 위치를 확인한다.

```bash
python -m pip list
```

현재 환경에 설치된 패키지 목록을 확인한다.

```bash
python -m pip show requests
```

특정 패키지의 설치 정보를 확인한다.

```bash
python -m pip install requests
```

패키지를 설치한다.

```text
list    → 목록 보기
show    → 특정 패키지 정보 보기
install → 설치
```

---

## 6. 가상환경이 필요한 이유

가상환경은 처음에는 어려운 말처럼 느껴졌지만, **프로젝트마다 만들어주는 전용 방**이라고 이해했다.

예를 들어:

```text
프로젝트 A → package X 버전 1 필요
프로젝트 B → package X 버전 2 필요
```

하나의 환경을 같이 사용하면 서로 영향을 줄 수 있다. 그래서 프로젝트마다 필요한 Python과 패키지를 따로 관리한다.

```text
프로젝트 A
└── 전용 가상환경
    └── package X 버전 1

프로젝트 B
└── 전용 가상환경
    └── package X 버전 2
```

> **가상환경 = 프로젝트마다 Python과 패키지를 따로 관리하기 위한 전용 환경**

---

## 7. .venv 만들기

Windows에서 프로젝트 폴더의 터미널에서 실행했다.

```bash
py -m venv .venv
```

그러면 프로젝트 안에 `.venv` 폴더가 생성된다.

```text
python-basics/
├── .venv/
└── ...
```

`.venv`는 Python 소스 코드 파일이 아니라 **프로젝트 전용 실행 환경을 담은 폴더**다.

---

## 8. 가상환경 활성화

PowerShell에서는:

```powershell
.venv\Scripts\Activate.ps1
```

을 실행한다.

이 명령을 경로처럼 읽으면:

```text
.venv
→ 가상환경 폴더

Scripts
→ 그 안의 Scripts 폴더

Activate.ps1
→ 가상환경을 활성화하는 PowerShell 파일
```

활성화되면 터미널 앞에 보통 `(.venv)`가 표시된다.

```text
py -m venv .venv
→ 가상환경 만들기

.venv\Scripts\Activate.ps1
→ 가상환경 활성화

deactivate
→ 가상환경에서 나오기
```

---

## 9. 현재 어떤 Python을 사용하고 있는지 확인

`(.venv)` 표시만 믿지 않고 실제 Python 경로를 확인할 수 있다.

```bash
python -c "import sys; print(sys.executable)"
```

오늘 직접 확인했을 때 `.venv\Scripts\python.exe` 경로가 나타나 현재 프로젝트의 가상환경 Python을 사용하고 있다는 것을 확인했다.

pip도 확인했다.

```bash
python -m pip --version
```

Python과 pip가 모두 같은 `.venv`를 가리키는지 확인하는 것이 중요하다.

### 핵심

**패키지를 설치한 Python과 실제 코드를 실행하는 Python이 같아야 한다.**

예를 들어 Python A에 `requests`를 설치했는데 VS Code가 Python B로 코드를 실행한다면 `requests`를 찾지 못할 수 있다.

---

## 10. VS Code Interpreter

컴퓨터에는 여러 Python 환경이 있을 수 있다.

VS Code에서는:

```text
Ctrl + Shift + P
→ Python: Select Interpreter
```

를 이용해 현재 프로젝트를 어떤 Python으로 실행할지 선택한다.

내가 이해한 Interpreter는:

> **내 Python 코드를 실제로 실행해주는 Python**

가상환경을 만들었다면 VS Code에서도 프로젝트의 `.venv` Python이 선택되어 있는지 확인해야 한다.

---

## 11. requirements.txt

`.venv` 폴더에는 실제 설치된 패키지와 많은 파일이 들어 있다. 이 폴더 전체를 GitHub에 올리는 대신 **어떤 패키지가 필요한지 목록을 기록한다.**

현재 설치된 패키지를 확인한다.

```bash
python -m pip freeze
```

파일로 저장한다.

```bash
python -m pip freeze > requirements.txt
```

`>`는 앞 명령의 결과를 파일에 저장한다고 이해했다.

`requirements.txt`에는 다음처럼 패키지와 버전이 기록된다.

```text
certifi==...
charset-normalizer==...
idna==...
requests==...
urllib3==...
```

다른 사람이 프로젝트를 받으면 새 가상환경을 만든 뒤:

```bash
python -m pip install -r requirements.txt
```

로 필요한 패키지를 다시 설치할 수 있다.

```text
.venv
→ 실제 물건이 들어 있는 내 방

requirements.txt
→ 그 방을 다시 만들기 위한 장보기 목록
```

---

## 12. .venv는 Git에 올리지 않는다

`.venv`는 다시 만들 수 있고 파일도 많기 때문에 보통 Git에 올리지 않는다.

`.gitignore`에:

```gitignore
.venv/
```

를 추가한다.

대신 Git에는 **소스 코드 + requirements.txt**를 남긴다.

---

## 13. ModuleNotFoundError가 발생하면

예전 같으면 패키지를 다시 설치하는 것부터 생각했을 것 같다. 하지만 오늘은 오류가 발생했을 때 확인 순서가 있다는 것을 배웠다.

```text
1. import 이름이 맞는가?
2. 직접 만든 모듈이라면 파일 위치가 맞는가?
3. 외부 패키지가 현재 환경에 설치되어 있는가?
4. 현재 실행 중인 Python은 어느 경로인가?
5. VS Code가 같은 Python Interpreter를 선택했는가?
```

특히 기억할 것:

> **“패키지가 설치되어 있는가?”와 “현재 실행 중인 Python에 설치되어 있는가?”는 다른 질문이다.**

---

## 14. AI를 오류 해결에 사용하는 방법

오류가 발생했을 때 AI에게 바로 `고쳐줘`라고 하기보다 현재 환경을 하나씩 확인하도록 요청하는 것이 더 좋다.

예:

```text
ModuleNotFoundError가 발생했다.

정답 명령부터 알려주지 말고
1. 모듈 이름
2. 파일 위치
3. 현재 Python 경로
4. pip 설치 위치
5. VS Code Interpreter
순서로 하나씩 확인할 수 있게 도와줘.
```

AI가 명령어만 대신 알려주는 것보다 **현재 환경이 어떤 상태인지 읽고 오류 원인을 찾는 능력**이 중요하다는 것을 배웠다.

---

## 15. 패키지를 이용해 코드 역할 나누기

예를 들어:

```text
order_project/
├── .venv/
├── main.py
└── shop/
    ├── __init__.py
    ├── price.py
    └── delivery.py
```

각 파일의 역할은 다음과 같다.

```text
shop/
→ 관련 기능을 모아놓은 패키지

price.py
→ 가격 계산 모듈

delivery.py
→ 배송 관련 모듈

main.py
→ 필요한 기능을 가져와 전체 프로그램 실행
```

예를 들어:

```python
from shop.price import apply_discount
```

는 다음처럼 읽을 수 있다.

> **shop 패키지 안의 price 모듈에서 apply_discount 함수를 가져온다.**

```text
패키지
└── 모듈
    └── 함수
```

코드를 여러 파일로 나누는 이유는 Python이 무조건 여러 파일을 요구해서가 아니라 **각 코드의 역할을 나누어 찾고 수정하고 관리하기 쉽게 하기 위해서**다.

---

## 오늘의 핵심 정리

```text
함수
→ 하나의 기능

모듈
→ .py 파일

패키지
→ 관련 모듈을 묶은 폴더

pip install
→ 외부 패키지 설치

import
→ 코드에서 기능 불러오기

.venv
→ 프로젝트 전용 Python 환경

requirements.txt
→ 필요한 패키지와 버전 목록

Python: Select Interpreter
→ VS Code에서 사용할 Python 선택
```

## 오늘 가장 기억하고 싶은 것

예전에는 `.venv`나 `requirements.txt`를 프로젝트를 만들 때 그냥 입력해야 하는 명령이라고 생각했다.

오늘 직접 가상환경을 만들고 `requests`를 설치한 뒤 Python과 pip의 경로를 확인하고 `requirements.txt`까지 만들어보면서 각각 왜 필요한지 조금씩 연결됐다.

특히 오류가 발생했을 때 무조건 다시 설치하는 것이 아니라 **현재 어떤 Python을 사용하고 있고, 패키지가 어느 환경에 설치되어 있는지를 먼저 확인해야 한다는 점**을 기억하고 싶다.
