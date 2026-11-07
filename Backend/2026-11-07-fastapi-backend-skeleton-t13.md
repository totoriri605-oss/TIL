# FastAPI 백엔드 기본 구조 구축 — T13 개발·학습 기록

- 기록일: 2026-11-07
- 프로젝트: AI Career Platform (칸드)
- 담당: 황수아 / GitHub: totoriri605-oss
- [구현 PR #14](https://github.com/ai-career-platform/ai-career-platform/pull/14)
- [후속 패키지 추가 PR #44](https://github.com/ai-career-platform/ai-career-platform/pull/44)

## 내가 한 일

팀원들이 백엔드 기능을 추가할 수 있도록 FastAPI 기본 구조를 만들었다. 역할별로 코드를 나누고 앱 상태·버전 확인 API, 실행 설명서, smoke 테스트 7개를 작성했다. 로컬 검증 결과를 기록한 PR은 리뷰 승인 후 main에 병합됐다.

이 기록은 PR의 구현·검증 증빙과 학습 내용을 정리했다. 기록 작성 중 테스트를 다시 실행한 것은 아니다.

## 해결하려던 문제

기존 실험용 PoC와 구분되는 정식 백엔드 개발 공간이 필요했다. 여러 팀원이 기능을 추가할 때 코드 위치와 실행·테스트 방법을 알 수 있도록 공통 출발점을 마련했다. 기존 poc/staging/backend와 분리해 backend/를 신규 생성했고, T13 PR에서 기존 PoC는 변경하지 않았다.

## 역할별 구조

```text
backend/
├── app/
│   ├── main.py
│   ├── core/config.py
│   ├── routers/
│   ├── services/
│   ├── repositories/
│   └── schemas/
├── tests/test_smoke.py
├── requirements.txt
├── requirements-dev.txt
├── pytest.ini
└── README.md
```

| 계층 | 역할 | 쉬운 설명 |
|---|---|---|
| Router | 요청을 받고 서비스로 연결 | 안내 데스크 |
| Service | 업무 규칙에 따라 처리 | 실제 일을 하는 작업실 |
| Repository | DB 조회·저장·수정·삭제 코드 | 창고에 접근하는 담당자 |
| Schema | 데이터 항목과 자료형 정의 | 주고받는 정보의 양식 |

역할별로 나누면 필요한 코드를 찾고 수정하기 쉽다. DB는 데이터를 보관하는 공간이고 Repository는 DB에 접근하는 코드다. T13에서는 Repository 공간을 마련했고 실제 DB 연결은 T14 범위로 남겼다.

## 구현한 기능

- create_app(): FastAPI 앱 생성 함수
- lifespan: 앱 시작·종료 처리 구조
- Settings: APP_ENV·APP_VERSION 환경변수 기반 설정
- GET /health: 기본 앱 상태 응답
- GET /version: 실행 환경·버전 응답
- /docs·/openapi.json: Swagger UI와 OpenAPI 명세
- /api/v1: 후속 기능 라우터를 연결할 빈 진입점

### /health 요청 흐름

요청 → Router → Service가 응답 데이터 생성 → Schema에 맞춰 응답 반환

```json
{"status":"ok","service":"ai-career-backend"}
```

기본 앱 상태 확인용이다. DB 연결이나 전체 기능의 정상 여부까지 검사하는 것은 아니다. 인증·인가 역시 T13에서 구현한 범위가 아니다.

## 실행 방법과 패키지

README에 설치·실행·테스트·기능 추가 방법을 작성했다. T13 시점 requirements.txt에는 FastAPI 0.115.12와 Uvicorn 0.34.2, requirements-dev.txt에는 실행 의존성과 pytest 8.3.5·httpx 0.28.1을 기록했다.

당시 PR의 Windows 11 PowerShell·Python 3.12 재현 명령이다. 저장소 루트에서 시작한다.

```powershell
Set-Location backend
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-dev.txt
.\.venv\Scripts\python.exe -m pytest -q
.\.venv\Scripts\python.exe -m uvicorn app.main:app --host 127.0.0.1 --port 8000
```

## 테스트·실행 증빙

- 테스트 파일: backend/tests/test_smoke.py
- PR에 기록된 로컬 결과: **7 passed**
- 테스트 SHA: cfc93fb37c2c402cfcaf04f7e2a3b300292fff2c

| 검사 | 확인 내용 |
|---|---|
| 시작·종료 | lifespan에 따른 앱 상태 변경 |
| /health | 200과 예상 응답 |
| /version | 환경변수 반영 |
| /openapi.json | 명세와 시스템 API 경로 |
| /docs | Swagger UI 제공 |
| 미구현 주소 | /api/v1/me 요청에 404 |
| 기본 설정 | 환경변수가 없을 때 기본값 적용 |

실제 Uvicorn 기동과 /health·/version·/docs 확인 및 Swagger 캡처도 PR에 기록했다. 없는 기능에 404가 나오는 것도 예상한 정상 동작이다. 테스트 7개 통과는 전체 서비스 완성을 뜻하지 않는다.

## 리뷰·병합과 검증 한계

PR #14는 승인 후 2026-11-06 main에 병합됐다. 리뷰 의견은 “고생하셨습니다. 다음 작업 진행해주세요.”였다.

**구현·리뷰·병합은 완료됐지만 당시 PR의 상태는 T13_STATUS=PARTIAL이다.** 당시 CI는 README·automation 테스트를 확인했으며 backend pytest는 실행하지 않았다. 로컬 통과를 CI의 백엔드 검증 통과로 확대 해석하지 않았다. 이후 CI 보완 여부는 이 기록에서 확인하지 않았다.

- 로컬 실행·테스트: PR에 통과 증빙 기록
- 리뷰·main 병합: 완료
- CI의 backend 테스트: 당시 미검증
- DB 스키마·Seed·공유 Staging 변경: 없음

## 후속 작업과 구분하기

DB 연결·세션 수명주기·/health/db는 T14, 인증·인가 및 서비스 API는 후속 기능 일감, 개인정보 동의·탈퇴 요청은 T31 범위다. 오류 응답 형식과 CORS도 당시 별도 후속 항목으로 기록했다.

별도 PR #44에서는 팀이 같은 버전을 설치하도록 backend/requirements.txt에 SQLAlchemy==2.0.57과 pydantic==2.14.3을 추가했다. 해당 PR에는 Python 3.12에서 pip check 충돌 없음과 기존 테스트 7개 통과가 기록됐으며 승인·병합됐다. 의존성 준비 작업이지 T31 기능 구현 완료는 아니다.

## 배운 점

1. 기능 추가에 앞서 구조와 실행 방법을 마련하는 것도 개발이다.
2. Router는 연결, Service는 업무 처리, Repository는 DB 접근, Schema는 데이터 형식을 담당한다.
3. 정상 응답뿐 아니라 예상한 예외 응답도 테스트해야 한다.
4. 로컬 테스트·CI 검증·PR 승인·병합은 각각 다른 확인 단계다.
5. 구현 범위와 검증 한계를 정확하게 기록해야 한다.

## 면접에서 설명하기

“팀 프로젝트에서 FastAPI 백엔드 기본 구조를 구축했습니다. 기존 PoC와 분리된 backend 디렉터리를 만들고 Router·Service·Repository·Schema 계층을 나눴습니다. 앱 상태·버전 API, 환경변수 설정, 시작·종료 처리 구조를 구현했으며 README와 smoke 테스트 7개를 작성했습니다. 로컬 검증 증빙을 포함한 PR은 리뷰 후 main에 병합됐습니다. 당시 CI가 백엔드 테스트를 실행하지 않는 검증 한계도 PR에 명시했습니다.”

## 다음 학습

- [ ] 후속 CI에서 backend 테스트가 자동 실행되는지 확인하기
- [ ] /health 요청이 이동하는 코드 경로를 직접 설명하기
- [ ] 후속 기능을 기존 계층에 연결하는 방법 이해하기
